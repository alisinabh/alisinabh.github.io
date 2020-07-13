---
layout: post
title: Jalaali calendar for Elixir
---

[`jalaali`](https://github.com/jalaali/elixir-jalaali) package version 0.2 is released for Elixir.

It offers a new module `Jalaali.Calendar` which is an implementation of elixir's `Calendar` module.

With the help of this module, it is possible now to convert DateTimes to each other easily by using `DateTime.convert` or `Date.convert` functions.

## Long story short

The previous version of jalaali was a mess! really.

It just provided functions to users for converting from/to ISO calendar.

The most annoying thing was it actually did not change the `calendar` property in a Date/DateTime struct.

Even if it did it wouldn't be a useful feature cause conversion was not possible throw Elixir < 1.5

So after a very long talk in the community about this which you can read [__here__](https://elixirforum.com/t/calendars-calendar-conversions/3119)
use of day number + day fraction was chosen to implement. This decision has made elixir one of rare languages with a very very very strong native calendar system.

It's been a while since elixir 1.5.x was released and I've been really excited about adapting my jalaali library with the new Calendar system in elixir.

At first, I thought it may take me several days to make that  happen, BUT surprisingly it was so easy that it only took me less than 5 hours (including tests and documentations)
and jalaali 0.2 is now published.

I really liked it and may try adapting other calendar systems for elixir as well just for fun.

BTW, I will be happy if you take a look at jalaali [github.com/jalaali/elixir-jalaali](https://github.com/jalaali/elixir-jalaali) and maybe star it?

Thank you for reading.