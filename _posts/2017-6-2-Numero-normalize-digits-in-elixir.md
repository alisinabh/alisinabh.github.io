---
layout: post
title: Numero: handling non-standard utf8 digits like a boss!
---

How to convert/normalize non standard UTF8 digits in elixir? How to convert arabic digits to integers in Elixir?

Recently I was so busy with my job and college so I had no time for writing here. I apologize to you.

In one of the projects we've needed an http service for some kind of software activation.

Although we did't have a decent time for that project I've decided to build that service using phoenix framework. And I decided to make it open source!

The project was a nice experiment for me on API's using elixir and phoenix in production. However I came to a simple problem that I could handle more easily with .NET

The problem was that some users entered their license number in the app using their native language keyboard and as you know, there are lots of different numbers in utf8 table.
In .NET you can simple resolve this issue using char.GetNumericValue, but in elixir I didn't found any reasonable easy solutions for that. So I've decided to make a micro library for that matter.

And oh boy! Did you know there are more than 50 numeric representations in UTF8? 59 to be exact.

Here is a list of all zeros in UTF8:
```
0٠۰߀०০੦૦୦௦౦೦൦෦๐໐༠၀႐០᠐᥆᧐᪀᪐᭐᮰᱀᱐꘠꣐꤀꧐꧰꩐꯰０𐒠𑁦𑃰𑄶𑇐𑋰𑑐𑓐𑙐𑛀𑜰𑣠𑱐𑵐𖩠𖭐𝟎𝟘𝟢𝟬𝟶𞥐
```

I've named it 'Numero' which means Number in Spanish (I don't know Spanish at all!)

With numero you can normalize number chars in a string or parse a string to number (Integer or Float). Numero is also smart on number types. if your number has fraction points in its string Numero will return you a float, otherwise it will hand you your number as Integer.

## Usage Example

```elixir
result = Numero.normalize("1۲۳۰4a۳tس")
# result = "12304a3tس"

result = Numero.normalize_as_number("1۲۳۰4۳") # Strings without fraction points return Integer
# result = {:ok, 123043}

result = Numero.normalize_as_number("1۲۳۰4۳.۴5") # Strings with fraction points return Float
# result = {:ok, 123043.45}

result = Numero.normalize_as_number!("1۲۳۰4۳.۴5") # Return number as result
# result = 123043.45
```

## Installation

You can visit numero here: [https://github.com/alisinabh/Numero](https://github.com/alisinabh/Numero) (FORK ME!)

Or install it in your projects with:

```elixir
def deps do
  [{:numero, "~> 0.1.2"}]
end
```

Thank you for reading this.