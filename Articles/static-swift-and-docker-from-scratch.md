-----

date: 24-10-17

-----

# Static Swift and Docker from scratch

So [Swift 6.0](https://www.swift.org/blog/announcing-swift-6/) was released 
recently and the feature I was most excited for besides 
[strict concurrency](https://www.swift.org/blog/announcing-swift-6/#language-and-standard-library)
 was static cross compilation to Linux. Which to me is very exciting as I can 
start cross-compiling my programs to Linux and slowly migrate to Linux 
full-time and get one step closer to fixing my biggest pet peeve in software; 
slow, buggy, and inconsistent UI/UX across my OS.

## Swift cross-compilation overview

The 
[article](https://www.swift.org/documentation/articles/static-linux-getting-started.html)
 talking about this is a little too wordy (in my opinion) to learn how it uses 
it and what you are getting. Swift has a pretty big runtime so statically 
compiling programs this way has a bit of a cost at first but the trade-off is 
after you have included the runtime and all its benefits. So that cost in 
proportion to the rest of code you write will be running shrinks as the 
complexity and capabilities increase as the software grows. If you are careful 
about dependencies and what abstractions you are using, you get a somewhat 
portable binary in that this binary includes the 
[MUSL](https://www.musl-libc.org) `libc` implementation so for my understanding
the OS you are running this on doesn’t have to provide a `libc` or can have a 
different implementation. So I can use an x86 binary on any `x86` Linux kernel 
and similar for `arm` binaries and systems. Which I think is pretty neat for a 
safe memory-managed language like Swift.

## Basic naive workflow

Right now I compiling the program (a web server in this case) targeting an x86 
Linux machine. Then copy that binary into a “Staging” directory with a 
Dockerfile shown below, building the image and deploying that image.

Setting up Swift to do this isn’t too hard. First, make sure to install an 
open-source version of the  
[Swift compiler](https://www.swift.org/install/linux/ubuntu/#versions) and a 
[Static Linux SDK](https://www.swift.org/documentation/articles/static-linux-getting-started.html)
 that matches the compiler you have. Then we can compile a 
[Swift Package](https://www.swift.org/documentation/package-manager/) using the
following command.

```sh
# You can omit `xcrun --toolchain swift` prefix if you're not on MacOS.
xcrun --toolchain swift swift build -c release --swift-sdk x86_64-swift-linux-musl
```

Note for MacOS users the pre-installed one on MacOS does not work for 
cross-compilation at this time. So once you have installed the open source one 
you need to select it in Xcode or using Command Line Tools.

After we have built the binary, copy it into a staging directory. Command 
probably looks something like this.

```sh
cp .build/x86_64-swift-linux-musl/release/Website Staging/Website
```

Then start up Docker move into your Staging directory and create the following 
Dockerfile. Then build the image or deploy the image to wherever you wanna use 
it. A [SwiftNIO](https://github.com/apple/swift-nio) based web server I am 
tinkering with currently compiles down to a ~248mb binary which nets an ~80mb 
Docker image, which I am running in a 256mb cloud container so not too bad and 
pretty cheap for a blog.

## Docker File

I understand it is not safe to run a web server as root.

```dockerfile
FROM scratch

COPY . .

EXPOSE 8080

ENTRYPOINT ["./Website"]
CMD ["0.0.0.0", "8080"]
```

## Additional Notes

There is also this 
[Swift Package](https://github.com/apple/swift-container-plugin) which is doing
a similar thing but using the `swift:slim` Dockerfile instead of a `scratch` 
one. I also couldn’t get authorization with it to work with the cloud provided 
I am currently using and I learned a bit more about Docker doing it this way.


This is also exciting to me as I saw this 
[PR](https://github.com/swiftlang/swift-evolution/blob/7f9488e0a41576139510dcb6e87f5b3d87359aed/visions/memory-safety.md)
 about a “Strict Memory Safety” mode for Swift. This is pretty exciting in 
conjunction with Swift getting better at expressing low-level control over 
memory with 
[lifetimes](https://github.com/swiftlang/swift-evolution/blob/9ba7a574d1557eefb4bc3cce1d07efee51861f21/proposals/NNNN-lifetime-dependency.md)
 , and

[static sized arrays](https://github.com/swiftlang/swift-evolution/blob/873bc06b6d85b5b063989fe0581faff3ee0ba8b6/proposals/nnnn-vector.md)
 making their way into the language. Not to mention a stories for 
[Embedded Swift](https://www.swift.org/blog/embedded-swift-examples/), 
[WASM](https://github.com/swiftlang/swift-evolution/blob/a88c667196d4ea390d0ecfb71963a55a5c8a5d12/visions/webassembly.md)
 and 
[ABI](https://github.com/swiftlang/swift-evolution/blob/a349525e855f17be68fcba83155e1fb27ea0143c/visions/abi-stability.md)
 stability for Windows and Linux. Getting ahead of myself a bit but still 
exciting.

Something I think is interesting because Apple deprecates it’s hardware and 
operating systems over time they can actually iterate on there ABI with Swift 
being included in the OS’s.

Thanks for reading,

Zane

[Leave Feedback](https://github.com/zaneenders/articles/blob/main/static-swift-and-docker-from-scratch.md)