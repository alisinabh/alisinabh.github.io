---
layout: post
title: NanoPi Neo as Webserver
---

What could go wrong running my blog on a NanoPi NEO?

This weekend I was really bored.
I just thought maybe its a good idea to play with the nerves-project a bit, So I went to find my raspberry pi from the closet and oh boy, It was a giant mess :|

Throw the process of finding the rpi_2 something caught my eye. **[A NanoPi NEO](http://www.friendlyarm.com/index.php?route=product/product&product_id=132)**
I bought it around a year ago to make an automatic garden keeper. but things went wrong after I sank it in mineral oil for cooling. the board went crazy and froze 10 seconds after bootup. I've wrapped it inside some paper towels and left it inside closet.

"Let's try and see if it's still broken."
I downloaded UbuntuCore with Qt-Embedded Image File for NanoPi NEO, flashed image into sd card and plugged it in.
**It worked!!**
Maybe after all time really heals some wounds ;)

Anyways, it was stable. I liked the performance of Allwinner H3 SOC and it is absolutely a charming feeling watching such a tiny computer working with fair performance. Wait a minute... Can I host this blog on it?

This single seed of idea has taken my entire weekend.
I first tried to install Erlang on it. but binaries for ``arm71`` was old. I've downloaded otp source code from github and build it on NanoPi NEO.
It took about 40 minutes to build. I was not disappointed. In fact, I was surprised because I thought it may take a couple hours.

Then I tried building Elixir from source code. It was all good until it became to ``compiling unicode``. As [@josevalim](https://github.com/josevalim) said in [issue #5856](https://github.com/elixir-lang/elixir/issues/5856) to me, compiling unicode module requires loading large amount of unicode tables and optimizing it and because I only have 512mb of RAM and no swap, OS killed the build process. He suggested using precompiled Elixir. (Why I didn't thought of that?).
And Oh boy. It worked.

Elixir 1.4.2 and OTP 19.2 were installed and working on NanoPi NEO.

Now I just needed to run my blog on it. After cloning ``mix phoenix.server`` didn't let me down.
Alisinabh.com has successfully built and run on NanoPi NEO (since I use flat files as database, I don't need anything else.)

So after all, I decided to host alisinabh.com on my NanoPi NEO. there is only a couple things I need to worry about for doing so:
 - Print a housing and get a heatsync for it.
 - Get an static IP address for my home internet connection or use DDNS (I don't like this!)

Thank you for reading.
