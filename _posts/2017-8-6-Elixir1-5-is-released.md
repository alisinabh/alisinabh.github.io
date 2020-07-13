1502048221661
Elixir 1.5
Recently Elixir 1.5 has been released. [Release Notes](https://github.com/elixir-lang/elixir/releases/tag/v1.5.0) [About 1.5](https://elixir-lang.org/blog/2017/07/25/elixir-v1-5-0-released/)

After a quick look on release notes you will notice that these updates, improvements and bugfixes are not major, Meaning
Elixir is getting mature.

The most major change in my opinion is the Calendar module. Most of the callbacks to calendar module is changed. The reason to this change is because the Calendar conversion was impossible in Elixir <1.5

So to tackle this issue community decided (This is really pleasing for me to say that "Elixir community decided") to use Ratta die algorithm for Calendar conversions. And that is a nice move because conversions of different chronologies in Elixir are now super accurate.

If you are interested in reading more about these changes you can visit Elixir docs. [Link]()

Other than this the majority of changes in this release are "IEx Improvements", "@impl for callbacks" and ability to set breakpoints on functions and modules (which is in favor of OTP/20)

I'm really excited about the future of Elixir and Erlang in our concurrent world.

Thank you for reading this.

T{:okT, :lets_party_یوتی_اف8}T

Wait! Did i forgot to mention UTF-8 atoms? :O 