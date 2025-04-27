# Redesigning My Website (Again)

If you're reading this, congratulations! You're viewing the latest iteration of my website. I've recently refactored and rebuilt it using [Hummingbird](https://hummingbird.codes), [HTMX](https://htmx.org), a custom [markdown](https://www.markdownguide.org/getting-started/) parser, and [Stripe](https://stripe.com). This is the first version I'm genuinely proud to share with others. I'm always looking for ways to improve, so please feel free to offer suggestions, both technical and non-technical.

## My Motivation

Here's a brief explanation of my approach to building this site.

### [Hummingbird](https://hummingbird.codes)

I chose Hummingbird for the server because I'm most comfortable with the Swift programming language and it doesn't really matter how you build your backend, however I believe Apple is developing a powerful language for distributed system and other domains of software development how ever it is still very early in it's development in my opinion.

### HTMX

Many Swift-based websites use either a frontend framework like [Vue](https://vuejs.org) or [React](https://react.dev), or generate static files to serve with tools like [Publish](https://github.com/JohnSundell/Publish), [Ignite](https://github.com/twostraws/Ignite), or [Toucan](https://toucansites.com). While I could have used one of these, I wanted to build something unique.

About two years ago, I saw a presentation on Phoenix LiveView and was inspired by the simplicity of its original base JavaScript [code](https://youtu.be/FADQAnq0RpA?feature=shared&t=629). This inspired me to create my own version with a SwiftUI-like DSL, a project I called Portal. I got the basics working with SwiftNIO sending updates via a websocket.

After graduating and starting my job search, I decided to finalize my website so that I could better share articles and my personal work. A friend suggested [HTMX](https://htmx.org), and I found it to be a perfect fit: a backend-independent, lightweight JavaScript framework. It involves simply including a JavaScript file and following its conventions for incrementally updating the DOM.

This allowed me to ship an interactive frontend experiences with not a lot of data needed to be sent over the internet working well on bad connections in my personal testing.

### Markdown Parser

This was the main reason for not using an existing website-building solution. I wanted full control over the content and how it is displayed. For the past four months, I've been using markdown files for my notes and journal, which I call the Log. I should probably write a post about it, as it's my attempt to minimize the technology needed to manage my life. It might be more complicated than necessary, but it's a learning experience.

I appreciate markdown's simple grammar, which is easy for anyone to use and straightforward to parse and manipulate programmatically. I use [swift-markdown](https://github.com/swiftlang/swift-markdown) for parsing, but I particularly like its customizability, allowing me to impose my own grammar on top of the language using a recursive descent style parser. For example, I added a metadata section at the top of each file to parse the article's date. This also allows for features like [tree-sitter](https://tree-sitter.github.io/tree-sitter/) syntax highlighting and user runnable code snippets.

This ties into why I chose HTMX over static file rendering: I wanted some level of server-side interactivity. Creative control is the underlying theme here.

### Stripe

The final component I wanted to include in this website version is a way to process online payments. I've added a "Buy me a large coffee ☕️" button. While I don't expect donations, this provided a minimal viable product (MVP) for using Stripe's API, enabling me to build e-commerce stores for others in the future.

## Closing Thoughts

Well I have made this project much harder than I needed it to be in hindsight,
I really wanted to build my own weird thing as a small step towards wanting to
have my own company writing software to make other lives easier. My personal
opinion on building software is the best way to build a good experience is to
use your own software ( 
[dogfooding](https://en.wikipedia.org/wiki/Eating_your_own_dog_food#:~:text=Eating%20your%20own%20dog%20food%20or%20%22dogfooding%22%20is%20the%20practice,usage%20using%20product%20management%20techniques.)
 ). My logic being if I don’t want to use it why should anyone else. From the
backend of building and shipping the software, to the end experience of viewing
and interacting with it I want all of that to be a pleasant experience and done
in a way that I can improve on all aspects of it and not back my self in a
corner. The later being why I made this project so hard on my self.

From social media to running an E-Commerce website for your small business of
selling and shipping bikes all over the world to just needing a place to
schedule and sell massages, haircuts. We all use computers but have so little
control over the domain as a whole layering abstraction after abstraction and
ever increasing the indirection from the core idea we are so motived to put on
the web. I don’t claim to have any solutions that I have shipped today but that
is the motivation behind why I am doing things the way I am doing them, I just
want to make our digital experience better for all so we can focus on what
really matters, our physical reality and those who we share it with.

[Leave Feedback](https://github.com/zaneenders/articles/blob/main/redesigning-my-website-again.md)