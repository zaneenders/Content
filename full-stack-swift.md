# How it's built

A oh 👋, Welcome to my website this article will give a little insight into how it's built, and what some of my plans are for it. To start things off I built the entire thing with the Swift programming language as it's my favorite language and the language I am most proficient at.

## Swift

Why am I building my website in Swift as opposed to any other language or framework? The simplest answer here is it's my website and I wanted to do something different and try and push the limit on the language I enjoy. I have some more technical reasons and in the long term, I hope to factor something out as a Web and/or UI framework.

### Syntax highlighting and markdown

To get started I am writing this blog post in Markdown and then transforming it into HTML using two packages, [Markdown](https://github.com/swiftlang/swift-markdown) and [SwiftSyntax](https://github.com/swiftlang/swift-syntax). The markdown package is pretty neat in my opinion as it parses the markdown file and gives a copy on write abstract syntax tree or AST for short. With this AST you can either transform the markdown into something else like HTML and CSS or perform manipulations to the markdown like formatting and writing the changes back to disk. The other package is SwiftSyntax, which I am using to parse the Swift source code using AST it produces to do the syntax highlighting for the Swift code blocks. This didn't end up working as cleanly as I was hoping as the AST you are given doesn't cleanly separate white space from syntax as I would have expected. In particular, keeping a couple of extra newlines attached to the tokens. This is probably fine for the Swift compiler and most use cases of the Swift AST but how I was using it to get the context for syntax highlighting ended up being kinda annoying and I ended up passing the output to an additional lexer to then apply the context-sensitive color appropriately. Depending on when you read this you may notice some inconsistencies in the syntax highlighting if you are used to how Swift is usually highlighted. I have gone through all this trouble as one of my projects I would like to complete or at least get to a working state so I can dog feed it is a text editor. Seeing that Swift is my primary language for personal projects I want to have good syntax highlighting for it and figured I could kill two birds with one stone and start figuring out the AST for Swift now. I also plan to build the editor in Swift so I think this will be cool in a sort of self-recursive way.  This also triples up as an introduction and starting point to learning how the Swift compiler works.

### Embedded Domain Specific languages (DSLs) and Macros

Below is a clip of the starting Swift code to build an embedded DSL.

```swift
@resultBuilder
public enum DOMBuilder {

    public static func buildBlock<Component: HTML>(_ component: Component)
        -> Component
    {
        component
    }
}
```

[Result builder](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/advancedoperators/#Result-Builders)s as they are called in Swift is one of the language features that initially captivated me in 2019 and motivated me to go back to school to learn how it works as well as how to build my own DSL's with it. I thought it was so cool to be able to embed your language within a host language and create your own abstractions for the computer. I believe Swift does a semi-unique job here as when you build these it still has to abide by the rules of the type system which is a little confusing and annoying depending on how comfortable you are with the generics system. This is one of the main features that Swift has that allowed for the development of API's like SwiftUI for Apple. However, the language features are not locked to Apple's platforms like SwiftUI is. Well, my own embedded languages aren't as powerful as SwiftUI I can make them more portable which I like. A similar result is achieved in other languages with a macro system and technically the `@resultBuilder` is the same syntax for a macro. So in a different world or future implementations of Swift, this could be done with just a macro system. Result builders is a feature I have spent more time on than I probably should have, but I really wanted to build my own abstraction for how to interact with the screen, as I find our current abstractions inconsistent, always changing, and very repetitive to use. So I was pretty heart-set on understanding how this work and how to use it. 

Now I have built a few DSL's with Swift which mostly failed as I was in way over my head for most of the time but I kept pushing and now I feel pretty confident with them. In addition to the HTML and CSS DSL that I am using for this website I also built a package called [ChromaShell](https://github.com/zaneenders/chroma-shell) which aims to make building declarative Terminal application for myself and hopefully others when it's more polished.

One thing I like about Swift's results builders in combination with Swift's type system is it allows you to build Type-safe abstraction for pretty much none-sense in terms of Math or the computer is used to but very much how we describe most things in computers. Which I think is really nice as now there is a type-system enforcing some consistency in the abstraction you are building. Granted there are many escape hatches but it's better than strings and untyped functions. This also reminds me of a phrase I have been hearing more and more as I meet people. Paraphrasing a bit "You can use any hack you want as long as it's consistent" and the more you learn how computers actually work not just understanding how to use the abstractions we built on top of them, the more true this expression becomes. This means if I want to describe the UI of a terminal in terms of an abstraction I call Block's I can as long as I can write a program to interpret and disambiguate that abstraction in terms of Swift and eventually machine code. Well, I have learned the hard way that starting with an opaque abstraction like that isn't usually the best way to build something, and have started calling this "pre-mature generalization" as a sort of rift on premature optimization. As I have learned it's best to hack the idea together write a bunch of bad hacky code to get the idea to work then refactor or simply restart with the knowledge of what you hacked together. 
Below is a sample of the HTML, and CSS DSL I am hacking together for this project. It's incomplete and honestly, I plan to change or experiment with how it works after Swift 6.0 comes out as there are a few new features that I wanna try out before making this public. I also would like to ship a higher-level abstraction than HTML and leave that as an implementation detail and adjust that with theming.


```swift
let doc = BasePage(path: "/full-stack-swift", title: title) {
        H1(
            .style(
                .color(.hex("#cecece")),
                .text_align(.center),
                .font_family("YellowTail"))
        ) {
            A(
                .href("/"),
                .style(
                    .text_decoration(.none), .color(.hex("#F05138")),
                    .display(.block))
            ) {
                title
            }
        }
        markDownToHTML(Document(parsing: fullStackSwiftArticle))
    }
```

Another note on result builders I think being able to experiment with languages and API's in this fashion is very cool as you can very quickly get an AST for the language and interpreter or compile that AST into something else. This is nice as you don't have to write a lexer and parser for every language idea you have, which just saves a ton of time. This does have its limitations as you are bounded by Swift's syntax and type system but I think this will be more than flexible enough for a lot of use cases. Now Swift's type system may not be the best for those who are exploring the area of type theory but in my opinion, it and the companion of Swift's emesis on what it calls value semantics makes things extremely easy to refactor and push code around. Which I think is very underrated as when you are trying to figure something out the last thing you wanna do is deal with type errors and bugs from refactoring. Move fast break things as they say just don't break what you working on unless that's your intention.

### Concurrency Model

The concurrency model in Swift might be hands down my favorite part as it feels unique from other languages I have used in that it's familiar but subtly different and its safety is backed by the type system which has allows for static data race checks in Swift 6 or if you enable those features now in your `Package.Swift` file with the following swift settings.

```swift
// Swift 6 settings
let swift6Settings: [SwiftSetting] = [
    .enableUpcomingFeature("BareSlashRegexLiterals"),
    .enableUpcomingFeature("ConciseMagicFile"),
    .enableUpcomingFeature("ExistentialAny"),
    .enableUpcomingFeature("ForwardTrailingClosures"),
    .enableUpcomingFeature("ImplicitOpenExistentials"),
    .enableUpcomingFeature("StrictConcurrency"),
    .unsafeFlags([
        "-warn-concurrency", "-enable-actor-data-race-checks",
    ]),
]
```

Below is a snippet of something unique to Swift which is a built-in `actor` model which is built into the language not just bolted on as an external library. The `actor` keyword adds a synchronization mechanism to isolate their state. Meaning that no two `Task` (Swift's concurrent units of work) may perform actions on that type at the same time. Well, this makes no guarantees about the order in which concurrent `Task` accesses the actor. I think this is nice, especially as someone who is relatively new at programming so being able to experiment with concurrent code with the type system behind me to throw errors when I program incorrectly is really powerful in my opinion. 
There is a cost to this abstraction, actors and classes in Swift are located on the heap and are atomically reference counted  (ARC) so those have their predictable cost, but the compiler team is currently working on adding the idea of ownership with the `~Copyable` protocol to allow reducing the ARC traffic in a program. 
Below is an example of initializing an actor and in this case with an async initializer to load a file from disk before the actor is ready for use. This probably isn't the best example as I really think Swift is a language you have to use to get a feel of how it behaves and feels to program not something you can read syntax and think "Awe yes I know how this works" again words have meaning but often the details behind it are different. The devil is in the details.

```swift
actor TodoStorage {
    init() async {
        // load data from disk
    }
}
```

Concurrency is a natural part of the digital world with multiple programs running on one system, delays from reading and writing to disk, and networking with other computers. Because of this fact almost every language has a way of doing concurrent programming but Swift's is built into the language and type system. This allows the compiler to give compile time errors about incorrect concurrent access to global mutable state unless the compiler can prove that that access is safe. This is done with a type called `Sendable` which I will leave you to read more about. But in short, Swift has the idea of value semantics which means when you have a variable containing a value type like an array or dictionary you don't have a pointer or reference to that type you appear to have the value it's self which means you can treat things more like Math or the widely loved but not so popular functional programming. 
The type system can pass these `Sendable` types around concurrently and provide guarantees about it's safety and correctness. Now like most languages, there are ways to opt out of this safety. For example, you can take a class which is traditionally a reference type stored on the heap, and add checks to make it behave as a value you type. This is great for large types that are expensive to copy around and don't change very much. This is how Swift's `String`, array and many other types in the Standard library are implemented. In addition to creating types that behave as values, you can also opt for types to be concurrently safe with`@unchecked Sendable` keywords. This tells the compiler to trust that you did it correctly with locks or mutex. This is common in the SwiftNIO library and I have some experience with the previous two versions of my website.

The last thing I wanted to mention is `distrusted actor`s even though I am not currently using them in this project but something I am very excited about experimenting more with them with this project and hopefully many more. As distrusted systems are something I find fascinating and think Swift will be a very good language for building them. You can append the `distributed` keyword in front of an `actor` type and the compiler enforces a few more guarantees as well as allows you to define `distributed func`tions which can make remote calls to other `distributed actors` on the system or across network boundaries. These local or remote calls are done with an `ActorSystem` which handles serialization and deserialization of `Sendable` types to send over the network using TCP, UDP, IPC, or any transport you like. Though at the time of writing this, I have only gotten a basic client-server implementation of the `ActorSystem` working. So expect more updates around this part of Swift.

### Dependencies

Here is a recap of all the current dependencies of the project. I like to keep this short as I think dependencies are something to be carefully considered as "everything temporary is permanent".
#### [Linux](https://github.com/torvalds/linux)
Linux might sound like a silly thing to mention but I still view it as a large piece of software that I depend on to work correctly. I am very much looking forward to Swift being able to cross-compile to Linux as it will be nice to build binaries and send them to other computers and will make moving to Linux a little bit easier. I also plan to shit my personal workflow over to Linux so knowing that most of the code I write works there is nice.

#### [Swift](https://www.swift.org)
Well, to build anything significant you need a programming language. I have decided to to Swift. Amongst the features I have listed in this project. There are so many little details that I like about it. One reason I have invested so much in Swift is its ability to talk to languages like C and C++ through having Clang built into the Swift compiler. C is the easiest to set up and use and I have built a basic `epoll` server using this traditionally known FFI, though Swift is different here and feels as if it speaks C natively. The C++ bidirectional interop I have not had a chance to play with. But I think this will be the reason Swift will gain in popularity. There is a lot of C++ code in the world, and that code is infamously hard to write or at least easy to get wrong, and there simply is not that much-skilled labor in the world especially to keep up with the rate we are writing not deleting code.

#### [SwiftNIO](https://github.com/apple/swift-nio)
As I mentioned I built a small toy server using `epoll` just because I wanted to get a sense of how it works and well I could have kept going with that server and learned about how to correctly do networking at that layer. However, I am primarily using MacOS right now as I found there is a lot of friction when using Linux in everyday life and there were enough annoyances with keyboard bindings and not wanting to spend time just yet to deep dive into how to fix all these annoyances I have opted to start using SwiftNIO learning how to use its abstractions for networking that I could develop for MacOS and Linux simultaneously. This has helped productivity a noticeable amount.

#### [HummingBird](https://github.com/hummingbird-project/hummingbird)
Keeping on the idea of productivity, meet HummingBird an HTTP server package to help make HTTP servers a little bit easier. And wow I should have started using this early. So little syntax to get going and start playing with an async HTTP web server. This also let me skip a lot of nitty-gritty details about how HTTP, TCP, and learning how to build a router. These are details I would like to come back to but for now, I am focusing on shipping what I am more excited to work on as well as writing about it here to be more focused on what I work on in my free time.

#### [AsyncHTTPClient](https://github.com/AsyncHttpClient/async-http-client)
This really hasn't been mentioned yet in this article as I haven't talked about how I have set myself up to make HTTP calls to other services like GitHub which I am using to link to some of my projects public on GitHub and dynamically update that information here on my website. As of writing this, I have only pulled the public repo names, but after finishing this article that is the next area of this site I plan to improve.

#### [Markdown](https://github.com/swiftlang/swift-markdown)
The markdown package I am using I have already talked a fair bit about, the only thing I would like to add is this also allows me to add my syntax and extend markdown for my own needs on this website. I like this method of transforming from an AST.

#### [SwiftSyntax](https://github.com/swiftlang/swift-syntax)
SwiftSyntax has been a fun learning experience as it is my first taste of the Swift compiler's code base. Well, I am a long way away from making any big contributions to the compiler but I think building the syntax highlighting for Swift is a great place to get a sense of Swift's AST.

## Future Plans

Let me take a brief minute to talk about my plans for this project.

### Open source

I plan to open-source this project as a package others can use to build websites for themselves with a focus on the content of the site but allowing them to dive deeper into control as they like. I think I have a lot working albeit mostly piping and plumbing things together right now but it's a good start. I wanna try and build something different intended for new people and maybe even those that program but don't wanna spend to too much time on a website.  Helping others get a personal space on the web for which they control and show them the power a little understanding of how a computer works gives you in this world.

### Personal API and Platforms

I don't really have a way of showing this as it's really just for personal use but I have a private endpoint on this server that I am accessing from my phone via an iOS app as well as the terminal on my computers via a terminal program. Well, it doesn't do much being able to have one language to cover all the devices I currently use and cover the ones I hope to move towards I think this is nice as I won't have to spend time in the future trying to port code with fragile hacks. 
Currently, Swift is best supported on Apple's devices, getting very good on the server as Swift is implemented in Swift making it easier for platforms to share implementations meaning more consistent API's across platforms. Also compiling to WASM is shortly on the horizon which I am very excited to experiment with in the browser as this makes Swift very portable. You can also use Swift on Windows and Android though I haven't experimented with this yet as I don't own either of those operating systems. However, I would keep expectations low here as this is pretty new and mostly community additions Apple wants Swift to be adopted as a replacement for C++ it cares more about shipping stuff to sell on its platforms so this has led to a rocky road for Swift outside of Apple's devices. Though as more of Swift gets implemented in Swift and mentions ABI stability on Windows and Linux I think think might achieve or at the very least come close to achieving this goal long term.

### Databases and Distributed Systems

I talked about `distributed actor`s and distributed systems a little bit but this is one of the areas of software I really hope to push on with Swift as I think Apple designed Swift to help solve its large-scale distributed system over a billion embedded devices. 
I think the starting point for me will be a database for the private API I mentioned above. Right now it just writes the data to disk and that works well enough but as soon as I redeploy the server or the docker instance restarts for some reason I lose all the data so I need something a little more robust and useful. Many of you are probably thinking of setting up Postgres and you're done and that is very doable but I want to experiment with this a bit before I add other dependencies to my list. I am taking a distributed system class in the fall where I will learn how to build a distributed key-value store using the RAFT algorithm and I think it would be cool to apply that learning to this project. I also think leveraging Swift's concurrency system hear will make re re-implementing that project in Swift much easier and the first time doing anything is the hardest.

### Personal Services and Automation

This is an area I'm probably most excited to explore and why I have built all this scaffolding to just ship a simple article. Is the idea that I have a server that can talk to other computers. Now this sounds obvious but being able to abstract away the networking details with the ActorSystem mentioned above I think opens the doors to experiment with a distributed system as building services for myself. A few examples off the top of my head are checking and making parking reservations either via a public API or as hacky as just sending the right headers to the right endpoint. Building web scrappers to poll information for me and then notify me when something changes via the iOS app that I have started alongside this. Well getting that to work I'm sure will be mostly battling Apple's API's and security at least I'm not also trying to do this in JavaScript or Rust so removes one layer of indirection. I also have the luxury of being the only one using this so I can break and change things as I need. Extending on this idea I find a lot of apps I use don't always give me the information or notifications I want and cloud the information they do send me with other noise to support their business. Most apps have notifications off more than me as I don't think that many businesses or services deserve to be able to interact with me at any point in the day. So moving some of this logic to a personal server and programmatically creating the filters and notifications myself I think will be pretty neat. Granted a bunch of work but the first one is the hardest, the second a little bit easier and eventually generalize it into a framework for myself. I think many people fall for the trap of taking on a dependency to try and solve something as soon as possible and then down the road spend more time fighting the dependency than if they would have just solved their problem the best way for them. Dependencies help build things but also add indirection and complexity to the problem. Most of that complexity is hidden away at first but as with most languages, you don't see there cracks on the first use of them. I also think this will be a nice way to get customized notifications about the world like housing, the stock market, and whatever information I think is worth keeping up on.

## Recap

As of writing this article this project is a little over 3,000 lines of Swift code. Well granted right now it's mostly scaffolding and plumbing to get these few high-level long-term goals in place I am pretty proud of what I have achieved so far in just 3,0000 lines of code considering I have type-safe DSL for HTML and CSS, transforming Markdown to HTML, and CSS, a fully concurrent HTTP server that is plenty fast for my use cases and free to run as it only needs less than 60mb of ram to run, and a web server for which I can experiment with other lots of different aspects of Swift like distributed system in there various forms. Giving my self a platform to solve my problems one by one. Thanks so much for reading about how I built my little space on the web.

[Leave Feedback](https://github.com/zaneenders/articles/blob/main/full-stack-swift.md)