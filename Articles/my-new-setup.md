-----

date: 25-04-06

-----

# My New Setup

> TLDR (Too Long; Didn’t Read):
> 
> - I’m back on Asahi Linux, always having the option to reboot to MacOS when 
>   needed.
> - I’m using Neovim again, specifically LazyVim, and I recommend giving 
>   LazyVim a try if you are curious about keyboard-based text editors like vim
>   or emacs.

## [Asahi Linux](https://asahilinux.org/)

I’ve reinstalled Asahi Linux, and it’s a noticeably better experience than the 
last time I installed it a year ago. I think I am at four attempts at running 
Asahi Linux for my daily OS now.

### Why install Linux?

I keep returning to Asahi because I have an M1 MacBook that I bought in 2020 
and for my project of building an operating system (OS), it’s best to be on 
Linux. So Asahi is the option for me right now. I will talk a bit more about 
this project and Linux in another future post. I also think being on Linux is 
helping me learn a lot about how computers work and will make me a better 
developer in the long wrong.

My primary use with this Linux installation is writing. From writing software, 
journal entries, content for my website, emails, etc….

> A random observation most jobs boil down to writing on a computer. There are 
> some more game engine-based workflows like Computer aided drawing (CAD), 
> video or photo editing, but most software we use is done through a web 
> browser these days and the information we work through is largely in text. 
> Yes there are expectations to this, but it’s a nice observation to keep in 
> your mind in my opinion.

### Experience installing and using Asahi

When setting up this Asahi Linux install the install itself was easy copy and 
paste a script from the internet, let it re-partition your disk, you know very 
safe operations. I have never had a problem with this and even when my install 
broke because of a bug in MacOS. I took it to the Apple store they reinstalled 
the firmware and I was back up and running.

> An aside, after losing a bunch of go-pro footage from a ski trip in Canada I 
> have the habit of making sure the data I care about is always saved somewhere
> else for cases if my computer gets stolen or destroyed and I regularly 
> Reinstall the OS to clean out crap piled up from third-party software putting
> files in random places, and I have this process on MacOS down to about 40 
> minutes which is mostly waiting for “Command Line Tools” to download and 
> install.

After getting booted up on the Fedora 41 Remix (Gnome) that Asahi has the 
option to install. I tried installing my current editor of choice VS Code, and 
it immediately crashed, which, honestly, didn’t surprise me.

## [VS Code](https://code.visualstudio.com/)

I have been using VS Code for writing for the last 3 years because I 
appreciated being able to work on different text files and code bases in 
different languages and not needing to install a different programs 
(abstractions) for every language or context. However, VS Code is not a 
lightweight editor. Being built with [electron](https://www.electronjs.org/) 
and effectively shipping a web browser as your editor.

To Microsoft’s credit shipping cross-platform software isn’t easy. Even 
shipping an app between Windows and MacOS is hard because you are standing on 
two very different ideas of how two operating systems should work despite 
converging on similar user interface abstractions but both being stuck with 
legacy ideas from the early [MS-DOS](https://en.wikipedia.org/wiki/MS-DOS) and 
[NeXTSTEP](https://en.wikipedia.org/wiki/NeXTSTEP) days. I’m optimistic this 
will get better with solutions like [Tauri](https://v2.tauri.app/) and 
[Swift](https://www.swift.org/) getting better support for 
[WASM](https://blog.swiftwasm.org/posts/6-1-released/), 
[Windows](https://www.swift.org/install/windows/) and 
[Android](https://github.com/swiftlang/swift/blob/main/docs/Android.md). Swift 
and [Rust](https://www.rust-lang.org/) being more memory-safe solutions as 
opposed to C++.

The web browser being a pretty flexible and creative environment to develop 
against and somewhat solving the problem of putting information on the screen 
for different platforms is why almost everything ends up being a web app and 
why JavaScript is so prevalent. Web browsers are one of the more complicated 
software you use daily, and this indirection does come at a cost and is partly 
the reason why everything is buggy and slow in my opinion. If a video game can 
run at 60fps well concurrently updating a large multiplayer world why is so 
much of our software for everything else so slow.

[Here](https://www.youtube.com/watch?v=ZSRHeXYDLko) is a nice talk by Johnathan
Blow about this and said better than me.

Anyway undeterred from VS Code crashing and wanting to give Linux an honest 
try, I decided to give Neovim another try.

## [Neovim](https://neovim.io/)

> `nvim` is the executable you run, read as Neovim or N vim.

For those that don’t know what Neovim is, Neovim is a derivative or fork of an 
editor called [Vim](https://en.wikipedia.org/wiki/Vim_(text_editor)) which was 
derived from [vi](https://en.wikipedia.org/wiki/Vi_(text_editor)) and before 
that [ed](https://en.wikipedia.org/wiki/Ed_(software)). Neovim is a text editor
that at first approximation looks like horrible software from the 70s, and to 
some degree you are right but tools like Vim and 
[emacs](https://en.wikipedia.org/wiki/Emacs) is how we got to the software the 
experience we have today and is still a very popular way of editing source code
as of the 
[2024](https://survey.stackoverflow.co/2024/technology#1-integrated-development-environment)
 stack overflow survey.

I first tried Neovim in 2020 after watching a 
[theprimeagen](https://www.youtube.com/@ThePrimeagen) video, quickly deciding I
needed to learn this way of editing files as it looked so fast and efficient. I
quickly became confused, as I had limited computer knowledge and basic 
programming skills. Back then, you had to install Neovim from the source to get
Language Server Protocol (LSP) integration working.

> The [LSP](https://microsoft.github.io/language-server-protocol/) is what 
> gives changes to your `.js` JavaScript file from a plain text file to an 
> interactive document, when combined with a few other technologies like syntax
> highlighting.

I have been giving Neovim/vim a try every year or so since then. I usually last
about a month and get frustrated by something and go back to VS Code. My 
minimum goal was to edit `.swift` ([Swift](https://www.swift.org/)) and `.md` (
[Markdown](https://en.wikipedia.org/wiki/Markdown)) files, both text-based.

> Excel, PDF, and Word documents are binary formats so you need special 
> software to open and edit them. Well text based ones you can open and view 
> hundreds of different editors.

I wasn’t too worried about markdown as it has pretty simple grammar, however 
programming in an environment where your editor is hooked up to its language 
server through the LSP, and Syntax highlighting brings programming to almost a 
video game-like experience.

Remembering that Swift had posted a blog 
[post](https://www.swift.org/documentation/articles/zero-to-swift-nvim.html) 
about setting up Neovim for Swift, and thought I would start there. Following 
the guide I got the basic configuration working but a lot was left to be 
desired coming from VS Code and all the tools I had become accustomed to. I 
remembered seeing some videos on YouTube about something called LazyVim and 
started looking into using that.

## [LazyVim](https://www.lazyvim.org/)

LazyVim is a pretty configured setup for Neovim. LazyVim is a collection of 
preconfigured plugins for NeoVim that are installed and set up for you. Getting
you something close to a VS Code experience but in a vim style editor. If you 
have never used Vim or any keyboard-based editors. I recommend trying LazyVim 
it’s dead simple to install or you can even try it in docker because it’s 
terminal-based. Most languages already preconfigured setups you can install. 
This means you don’t have to spend weeks learning how to configure Vim or 
Neovim right away.

Out of the box, LazyVim didn’t support Swift out of the box. So adding a 
[few lines of Lua](https://github.com/zaneenders/nvim/blob/lazy-vim/lua/plugins/core.lua)
 to my config files to see how hard this would be to integrate. I was 
pleasantly surprised that everything started lighting up. In-line errors and 
warnings from the LSP, rename-symbol, in-lining and expanding macros, 
jump-to-definition (even into imported 
[Packages](https://www.swift.org/packages/)) all worked. I was honestly 
shocked. The only thing missing from my Vs Code experience was the test 
integration and a UI for debugging which I think I can get set up but don’t 
really feel like figuring out right now as I don’t need them right now.

I was also surprised by my markdown files having a nice flare to them and even 
linting warnings which was annoying at first but automating and fixing those 
lead to much nicer markdown files which I am happy about.

## Roses and Thorns 🌹 🌵

Here are some additional roses and thorns of the experience.

### Thorns 🌵

#### Command and Control Keys

I had to fight my muscle memory during the first week of this Linux install. 
Keyboard shortcuts that are missing or have different behavior are very 
frustrating to me. Being very accustomed to using my Mac I quickly had to fight
and break a lot of habits of how I copy and base things, switch between 
applications. My current setup isn’t perfect but it’s good enough for now. I 
did end up needing to install a program called 
[evremap](https://github.com/wez/evremap) to remap my caps lock key to control.
This was easy to install and set up but Fedora Asahi Remix I have installed 
doesn’t have a working option for this in system settings.

#### Trackpad

I appreciate Apple’s trackpad tuning as on Linux, it’s overly sensitive, and 
palm detection is annoying. I spent much time looking at how to resolve this 
yet but a quick query shows that there are some options provided they work on 
this distribution of Linux.

#### LazyVim is an abstraction over Vim

LazyVim is a significant improvement over manually configuring Vim/Neovim for 
me, but it still inherits the drawbacks of being in abstraction over Vim. Vim 
has a steep learning curve sometimes relying on mnemonics for bindings. It uses
the keys h, j, k, and l for movement which feels ergonomic and consistent. You 
quickly learn about using b, w, e, and ge (g pressed then e) to jump and move 
over words which you get used to easily enough. But at some point, you will 
miss hit a key and stumble into a mode you didn’t know existed, not sure how to
get out of it, and honestly not sure what keys you hit to search how to disable
it.

LazyVim isn’t without its bugs and using the turn it off and on again approach 
I did create a script to delete `~/.local/state/nvim`, `~/.local/share/nvim`, 
and `~/.cache/nvim` files which reset your installation. I see this as a 
positive for LazyVim as it makes it easy to set on a new system by copying my 
[`~/.config/nvim`](https://github.com/zaneenders/nvim) files over and launching
nvim.

### Roses 🌹

#### LazyVim

As I mentioned above it’s very easy to reinstall your configuration which means
you can copy it to a computer with `nvim` installed and you have your editor. 
Because Neovim is a terminal-based editor you can use it over SSH which is a 
better experience than using the VS Code SSH extension.

If you have some Vim experience of being able to move around a file edit a few 
characters of a text file, save, and quit then I very much recommend trying out
LazyVim for an hour or so. If not give 
[vim adventures](https://vim-adventures.com/) a try its a fun little game.


Lazyvim being a configuration on top of Neovim is such a positive. For me, I 
see this as an entry point experiencing things I really like and slowly turning
off things I don’t like. This in my opinion lowers the barrier to entry for Vim
keyboard-based editing.

Getting used to moving around the files system and text files with only the 
keyboard is a bit of a learning curve but being able to grep over the codebase 
(with and with git ignored files), your files system or just the files you have
open is so nice to just load the context of what you are trying to do into your
head. It’s a different flow than VS Code but it’s a positive experience.

Last thing I want to mention Lazyvim looks amazing. Your text editor is the 
user Interface you will likely spend a lot of time staring at and having it 
look nice and pleasant to the eyes is a huge positive. If you don’t like the 
default colors it’s all just Lua files so you can reconfigure it if your 
motived enough.

#### Markdown

LazyVim includes packages that enhance Markdown editing. The text prediction is
reliable, and the inline source code rendering, powered by tree-sitter, is 
excellent. I was also surprised that the jump-to-definition command works in 
markdown as well.

## Closing out

While this might seem counterproductive and making my life more complicated, 
but I am really enjoying this new writing environment. I’m on Linux which means
my environment is closer from being effected by the stock market and 
shareholders and making a lot of headway on long-held ideas. I still need to 
reboot into MacOS for a few things but I see a path to moving away from that 
dependency.

Thanks for reading, and please feel free to leave 
[feedback](https://github.com/zaneenders/Content/blob/main/Articles/my-new-setup.md)
 . - Zane