cross platform continuous integration
===

After transferring all of my work from the rostrum repository to the new, more sensibly organized tadpole repository, I thought about my goals for the project and decided to set up continuous integration. I hope to one day have multiple contributors to the project, and rather than go through the pain of verifying every change on every platform, I'd prefer to just see on a dashboard whether their pull request is likely to break the build.

Luckily, Travis CI is free for open source projects, so that's what I'm using. Except for Windows -- Travis has limited Windows support so I'm using AppVeyor for that platform. I copied the AppVeyor config from libwebsockets, which does basically the same thing, but the Travis configs I had to figure out on my own.

Travis has the concept of a "parallel build matrix" which sounds unreasonably complicated to me so I just opted to construct my pipeline out of explicitly included jobs. I have some experience setting up Jenkins jobs, which I find more obtuse and difficult to write, but Travis was honestly still a tremendous pain.

You can see from my [build history](https://travis-ci.org/github/lwb4/tadpole/builds) how much agony I went through to get these things set up. Most of the 50+ commits I had to push were just tiny little changes because my assumptions about my Macbook Pro didn't hold up on Travis' linux build servers. That's the tough part about continuous integration -- your build environment is always slightly different than your local development environment.

By far the hardest platform to set up CI for was Android. C++ is a pretty well supported language on every other platform I've chosen, but writing C++ apps is a real PITA on Android. It doesn't help that I know very little about the Android operating system -- I've been an iPhone user for the last several years and I'm much more used to Appple's operating system and way of thinking.

I think there is a cool niche business opportunity in a product that makes your local dev environment, your build environment, and your prod environment the exact same machine. Maybe your prod environment is hardened more, has a stricter firewall, etc. but the point still stands. During my internship at Facebook I did most of my work on a devserver. They had this really cool system where if you wanted to contribute code to their giant, millions of LOC monorepo, you could request a VM with the repo pre-cloned into it and a fresh devserver would be ready for you within seconds. It was an incredibly slick experience. The business idea here is basically on-demand devservers for everything. I think the idea has a lot of juice if you take it to its logical extreme.
