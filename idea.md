what exactly is rostrum
===

rostrum is the code name for a project I'm working on. Why use a code name? Well, I don't want to burden myself with marketing concerns until I have more confidence that the project will actually materialize.

Let me introduce the problem. I have created a handful of cross-platform games in my life, and let me tell you, deploying those things is a tremendous pain in the ass. Unity actually makes developing for multiple platforms mostly ok-ish (quirks aside), but you still have to distribute the app yourself. It's time consuming and by far my least favorite part of the entire game development process.

Unity's answer to this pain is Unity Cloud Build and other services. My answer is rostrum.

rostrum is a small client that is available on every conceivable platform. I have plans to make it available on Windows, Macintosh, Linux, iOS Universal, Android, and even the browser. On startup, this client will fetch simple 2D games written in Lua from my servers. Players can browse through these games and play them at their leisure. Developers can write games with simple Lua scripts and upload them for players to enjoy.

In addition, developers can write simple Lua scripts for their backends and deploy them to my servers instantly. This allows for primitive multiplayer functionality, leaderboards, persistent accounts, and more. And it's all in the same language, using rostrum's well designed libraries.

There are still some kinks to work out, like:
- How will images work on the frontend?
- What database or other persistence services should be available on the backend?
- How will content be moderated and abuse monitored, so I don't just end up hosting porn?
- Will Apple even allow this in their app store because it runs third party code?

But I'm working those things out as I go. This is an ambitious project for me but I'm really excited about it, and at the very least it gives me some infrastructure for rapid prototyping.

In high school, I used to write games for my TI-84+ graphing calculator using an engine called Axe Parser. It was by far the easiest and simplest way to make games ever invented. You wrote an infinite loop, called a few functions to display monochrome sprites and get keyboard input, wrote some logic for the game itself and BAM you have a Mario clone or Brick Breaker clone or whatever. I miss those days. rostrum is an attempt to get that flow back in my life.
