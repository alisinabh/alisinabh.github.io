---
layout: post
title: Old code backfires!
---

As a daily programmer who lives by programming as a profession, Sometimes projects are not cool and they don't cheer you up.

Specially if they are you `OLD CODES` -__-

Your old projects can kill you when they are still in use. Every day you learn more and they that code makes less sense. But sometimes things go wrong when you realize that the code is bad an unreliable AT THE SAME TIME!


For instance let me tell you my story about one.

I've developed an Asterisk AGI server with .net and AsterNET. AsterNET doesn't use the async feature of .net and uses a Thread Pool.

So if you need 500 calls, you'll need 500 threads!


We've been migrated our new projects to a new server in the last two years but our old projects are still running on AsterNET server. The problem with that server is it will crash from time to time. Because of StackOverflow exceptions. The old projects are not valuable enough to fix and not so useless to just go on.

So, I came up with a fairly good solution. Using a process supervisor (AKA Safe process runner).

It will simply run the process and wait for it to exit. If so, SafeProcess will re-run the process.


It's not the perfect solution but it will buy me time and because this exception happens rarely (once or twice a month on average traffic) we can ignore it.


SafePorcess is available to use for everyone under no license:
https://github.com/alisinabh/SafeProcess