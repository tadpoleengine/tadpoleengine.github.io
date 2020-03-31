making an sdl project for every platform
===

The first step to making rostrum a reality was to create a working C++ and SDL2 example for all six platforms. I knew this would be annoying but I failed to realize just how painful it would actually be.

Here's basically what I had to do for each platform, but multiply how much time it sounds like it took by three because documentation is light and sometimes out of date, not to mention my complete lack of ever having done anything like this before.

This whole experience taught me that you should always read the official documentation before you start typing stuff into Google. Just about every blog post about setting up SDL2 on a given platform is hopelessly out of date.

The other takeaway I have is that everything takes at least three times longer than you expect when you don't know what you're doing. I believe in the myth of the 10x engineer simply because the guy who's been working with iOS for years doesn't have to re-learn how to configure Xcode projects, what the common functions of the core libraries are, how C++/Objective C/Swift interact within an app, etc.

I estimate this part took roughly 15 hours of work, but it felt like 40. About half that time was spent waiting for files to download and install, half was spent scratching my head because things wouldn't work like I expected, and then about an hour of it was the actual work of setting up projects.

Mac OS
---

* copied the sample Xcode project from the SDL2 source directory
* downloaded the SDL2 shared library into /Library/Frameworks
* recursively codesign everything inside the shared library
* figure out how to reference source code files outside of the directory tree (weirdly difficult)
* the game loop happens before the SDL window has a chance to render, so you have to call SDL_PollEvent periodically within the loop
* proof of concept works, restructure the project into a single source folder and an individual project folder for each platform

iOS
---

* copied the sample Xcode project from the SDL2 source directory
* link a bunch of random frameworks that weren't included in the project already for some reason, like CoreBluetooth ... but the error message doesn't say "link the core bluetooth library" it says "symbols for CBCentralManager not found"
* the SDL2 window takes up a tiny portion of the screen for some reason? Couldn't figure this out, have to revisit the issue later

Windows
---

* download VirtualBox
* downloaded a Windows 10 image
* manually walk through the installation screens
* figure out how to setup shared folders between host and guest
* why aren't the Virtual Guest Additions installing?
* download the MinGW version of the SDL2 source code (there's probably a way to do this from the same code base)
* download Code::Blocks and MinGW
* after that, setting up the project itself was actually smooth sailing

Linux
---

* download an Ubuntu 18.04 LTS image
* install Ubuntu on a Virtualbox machine (installer kept freezing for some reason)
* download and build the source
* download Code::Blocks
* repeat the fiasco of installing Virtualbox's Virtual Guest Additions and figuring out shared folders (easier the second time)
* set up the project in Code::Blocks
* it doesn't work because I forgot to install X11 development libraries
* works as expected, but I'm worried I may have to recompile for different CPU architectures? Have to check this later

Browser
---

* download and install the Emscripten SDK and CLI tools
* emcc is a drop-in for gcc, so it was easy to get it to compile
* however, I did not realize that you have to set up the game loop with `emscripten_set_main_loop()`. Took me over an hour to figure out why the whole tab would freeze on startup. It's because you can't do infinite loops in the browser -- you have to give other events a chance to get scheduled

Android
---

* luckily I already had Android Studio installed from previous projects
* download and install CMake and the NDK
* try to copy several projects, look up blog posts online, nothing works
* finally discover `docs/README-android.md` -- game changer. I should have been reading these for every platform
* weird that you have to soft link project libraries in the `app/jni` folder. I know close to nothing about Java/C++ interop, and even else about Android's NDK
