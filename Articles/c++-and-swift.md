-----

date: 25-05-14

-----

# Swift & C++

> Started learning C++ mixed with a bit of Swift

This all started when I got an email about a job interview, but the interview 
and the position would be in C and C++. These are two languages I have touched,
but wouldn’t consider myself a strong programmer in. So to prep for the 
interview, I did a few things to get myself excited about C++ and begin 
learning it.

The first of which was just relearning how to compile the files and fumbling 
together a project. I started with just manually invoking `clang` and then 
running the executable after, worked my way up to multiple files, and then got 
distracted by getting Swift and C++ compiling together with 
[cmake](https://github.com/apple/swift-cmake-examples). I thought this was 
cool, since I saw it get released, but for some reason, I decided to avoid C++ 
til now. I think I am a much stronger programmer than I was 2 years ago when I 
first touched C++, and that helped me have less to learn when learning the 
language, also not having the restrictions that school imposes on you when you 
learn new things. I could use any version of C++ I wanted, any project. I was 
actually having fun.

## [Two’s Compliment](https://www.twoscomplement.org)

Two’s Complement is a podcast that I stumbled into and listen to 
semi-regularly. The most recent podcast they published was about 
[C++ and Rust](https://www.twoscomplement.org/#podcast/c-and-rust-different-tools-for-the-job)
 Talk about the strengths and weaknesses of both. I was more excited about this
topic as it was an indirect way to learn more about C++. He mentioned a few 
other talks he did, one about 
[C++ style](https://www.youtube.com/watch?v=HG6c4Kwbv4I), which I would love to
see from other languages. The other previous talk he mentions is 
[Correct by Construction](https://www.youtube.com/watch?v=nLSm3Haxz0I) talks 
about building API’s that the compiler aids you in using correctly. C++ 
building on top of C inherited a bunch of ways to shoot yourself in the foot. 
It has to be this way so that the C code from the 70s can compile and run 
today. If you break that, it’s no longer C and C++, it’s something new, and if 
you’re going to do something new, you should break or remove as many of the bad
ways of doing something as you can.

### Swift

This is why I think Apple is building Swift and building it the way they are. 
At the surface level, Swift is kinda bad language or at least no better than 
Java, Go, Python, for any specific use case. I think the goal with Swift is to 
be the programming language for building distributed systems, user interface 
down to Systems programming. I think a large part of the complexity in our 
world is just gluing different languages and systems together.

Every language is designed to solve a problem, and Swift is being built to 
replace as much, if not all, of Apple’s source code and also do so 
incrementally. You can’t rewrite large systems and not expect something to 
break. Sure, you can calculate the loss in some way, but is the new language 
worth the risk, cost slow down to build on top of what you have? Apple doesn’t 
really get much credit for it, but it effectively replaced Objective-C. I think
even the Objective-C runtime is written in Swift now, which is pretty funny. 
Now they are working on C++ and projects they depend on, like LLVM, Foundation 
DB, and I’m sure many internal repositories.

### Swift & C++

Circling back to the Correct by Construction video, a lot if not all the points
made are defined away in Swift. This is recent with Swift getting what it calls
Not Copyable (`~Copyable`) types meaning you either have the thing or you gave 
it to someone else. One of three things happens with data when programming: two
parts of your code have a reference to something like a resource. Two parts 
both have their own copy or one part hands the resource off to another part, 
giving up its ability to access or mutate the data anymore. This last part 
isn’t common or at least not commonly used, I guess C++11 had the beginnings of
this. Rust is the most well-known language for enforcing this idea of not 
sharing data.

Apple is currently adding a bunch of syntax and features to Swift to have its 
own approach to what’s referred to as ownership and lifetimes. This is needed 
to express many of the things in C++ that they are trying to migrate away from,
as well as to do low-level resource-constrained programming.

## Learning from C++

Anyway, finally sitting down and spending some time learning C++ and working on
the [Ray tracing in one weekend](https://raytracing.github.io) book as well as 
Doing some Leetcode puzzles in C++, it’s been really funny to see how much 
Swift borrows from C++, and I also understand why so much of the world is 
written in C++ now. The language has pretty much been the live Beta for 
programming languages yes, there is Haskell and the functional and Lisp side of
programming langues, but Swift also steals from those languages with its 
protocols and value types.

Something kinda demonic but kinda fun is my leetcode 
[solutions](https://github.com/zaneenders/leetcode) are in C++, but I wrote the
tests and ran the project in Swift. So no CMake or other C++ build systems just
letting `swiftc` and internally `clang` take care of that, which allows me to 
leverage Swift for what it’s really good at right now, high-level abstraction 
programming. This is kinda a fun medium to move between, you have a high level 
of concurrency safe language and the ability to drop down to low level control 
with various degrees of safety. Swift is, in a way, gradually typing the 
computers that we are stuck with.

## Wrap up

Anyway, this was more about me having a bit of fun learning C++, appreciating. 
What Swift is trying to do, and also where it came from.

Thanks for reading, Zane.

[Source](https://github.com/zaneenders/Content/edit/main/Articles/c++-and-swift.md)