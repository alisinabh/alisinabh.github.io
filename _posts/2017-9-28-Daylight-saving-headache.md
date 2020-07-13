---
layout: post
title: Daylight saving headache
---

How to (properly) handle daylight saving in our application and services?


Not so long ago, I've ported [jalaali calendar for Elixir](https://github.com/jalaali/elixir-jalaali). In that process i've figured out Elixir's standard Date structure is missing something to accomplish calendar conversions. So i've started a conversation in Elixir forum which you can read [here](https://elixirforum.com/t/jalaali-shamsi-calendar-for-elixir-persian-calendar/2883/4?u=alisinabh) 

My idea was to force every calendar to provide callbacks to convert specific Date to ISO date or Unix Epoch (Which I liked more at that time!)

Then... I was intruduced to Date and DateTime complexities!

Calendars were not as easy as I thought it was. I even didn't know that we have Leap seconds in some years!!! 
```
 A leap second is a one-second adjustment that is occasionally applied to Coordinated Universal Time (UTC) in order to keep its time of day close to the mean solar time, or UT1. Without such a correction, time reckoned by Earth's rotation drifts away from atomic time because of irregularities in the Earth's rate of rotation.
```

The brilliant people in elixir community, @josevalim, @kip, @Qqwy came up with a nice solution using Ratta die. It is awesome an I think Elixir has one of the best native calendar implementation.

Anyways, I didn't learn my lesson yet at that time. :(

So I begun to use epoch millisecond as time in one of enterprise projects. We needed an offline TimeTable to handle timings of events in our application. So we designed [ZigorTimeTable](https://github.com/Resaneh24/ZigorTimeTable)

Each time table entry uses a startDate::DateTime as beginning of time, A  duration::Long in milliseconds as time of availability and a cycle::Long in millisecond as how often is this entry repeated.

Everything was awesome and fine. It worked like a charm!
You understand? **Worked!**

And suddenly, Daylight saving time occurred! :((
Every time table was messed up. they were all behind by one hour.

## Reason?

because of DST+1 (Day light saving) there was one hour missing from DateTime but it wasn't missing in milliseconds!

We had to change real times from server to wrong ones so the app would work correctly.

## Conclusion

Please do not mess with calendar and calendar systems in your enterprise level projects. these methods should be tested and verified precisely over long periods of time and not by normal tests. Instead, try to use a known implementation like JodaTime via updated TZDB data.