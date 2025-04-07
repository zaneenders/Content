# HTMX & Hummingbird

I have recently moved my site over to using [HTMX](https://htmx.org) combined 
with [Hummingbird](https://hummingbird.codes). So far I am really enjoying 
Hummingbird as it feels like how an async await Swift server should be. Granted
this is the first one I have used since I tried [Vapor](https://vapor.codes) 4 
years ago.

## Why

For some background, I love using the Swift programming language and have 
experimented a bit with trying to abstract frontend development with it using 
the `@resultBuilder` feature that SwiftUI uses, with projects like `Portal` 
that I may make public and talk about more in-depth in the future. In short, I 
got a SwiftUI inspired DSL working over a web socket similar to how the 
[Pheonix framework](https://www.phoenixframework.org) works. I used a minimal 
amount of Javascript to “patch” the DOM. I took a huge shortcut and replaced 
the entire body on each update. From my limited testing, this worked pretty 
well. After a few months go by I graduate with my Computer Science degree and 
decided I need to have something usable to show and work with, and that’s where
HTMX comes in.

## HTMX

I decided to take on HTMX as a dependency because I wanted some to update and 
make a responsive frontend in Swift with as minimal amount of Javascript as 
possible as I really didn’t wanna take on all the dependencies and bloat that 
comes along with front-end javascript uses. HTMX was pretty easy to add to the 
project I copied the file into my project. Added to the HTML template I already
had and incremental started adding routes and updating the DOM with HTMX. Well,
I don’t have the most responsive or interesting UI yet this did allow me to 
move on to other things well still having a way to easily update the UI as I 
add more features.

## Conclusion

Overall I’m pretty happy with the server setup I have right now. Everything is 
in Swift from generating the HTML, CSS, and limited Javascript needed to get 
the front end to work. I have some of this wrapped up in Swift types to make 
refactoring easier. I can easily add new routes as I need which has allowed me 
to start working on a campaign Apple App (iOS, iPad, MacOS) as well as a 
command line tool to interact with this server.

[Leave Feedback](https://github.com/zaneenders/articles/blob/main/htmx-hummingbird.md)