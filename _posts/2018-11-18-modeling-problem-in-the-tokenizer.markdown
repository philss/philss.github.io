---
layout: post
title:  "Modeling problem in the tokenizer"
date:   2018-11-18 17:41:48 -0300
---

I struggled a lot with a problem of modeling in the HTML tokenizer for [Floki][floki].

From one side I had performance concerns, which made me start with a more primitive approach. From
another side I wish a better modeling, which would make much easier to work inside the [tokenizer][html]
and inside the tree construction phase.

My worries about performance leaded to a poor design. I understand that now, and it's a relief to
realize it in the middle of the work. But the time I spend trying to make it faster for the first
version was costly.

## Tuples x Structs 🤓

The problem I was facing was: [tuples][tuple-doc] are ~~much~~ faster than [structs][struct-doc]/[maps][map-doc],
but they are not easy to work with when you need to update them. You may think: "but he could use pattern
matching". Yeah, you are right. But this is cucumbersome for tuples with more than 3 elements.

```
##### With input Big #####
Name                            ips        average  deviation         median         99th %
update name in tuple        10.71 M      0.0934 μs  ±3077.55%      0.0400 μs       0.130 μs
update name in struct        6.90 M       0.145 μs  ±2035.90%      0.0700 μs       0.170 μs

Comparison:
update name in tuple        10.71 M
update name in struct        6.90 M - 1.55x slower

##### With input Middle #####
Name                            ips        average  deviation         median         99th %
update name in tuple        10.43 M      0.0958 μs  ±3032.20%      0.0400 μs       0.150 μs
update name in struct        6.92 M       0.145 μs  ±2037.50%      0.0700 μs       0.160 μs

Comparison:
update name in tuple        10.43 M
update name in struct        6.92 M - 1.51x slower

##### With input Small #####
Name                            ips        average  deviation         median         99th %
update name in tuple        10.35 M      0.0967 μs  ±3082.52%      0.0400 μs       0.150 μs
update name in struct        6.92 M       0.145 μs  ±2037.05%      0.0600 μs       0.170 μs

Comparison:
update name in tuple        10.35 M
update name in struct        6.92 M - 1.50x slower
```

The benchmark can be [found here][benchmark].

## Structs for better domain modeling

Elixir has good data structures, and the one that I like a lot is the `Struct`. It is a `map` that
can have a "type", and this characteristic make structs great for modeling the system, and give
"names" to values.

Working with simple raw data structures like `tuples` can be faster and are totally recommend for
things like `Eithers` (like `{:ok, value}` or `{:error, reason}`), but are much harder to represent more
complex ideas and values. Another key point is that you can work better with protocols and strucs,
which makes the system more extensible.

In conclusion, performance can be good, but shouldn't be the most important thing when your are
starting a project.
Good modeling first will probably make your program's life longer and prosper.

Some people may argue that a HTML parser should be as fast as possible. I agree that this is ideal,
but it is not the main objective of Floki. For performance, we should offer implementations that are
[faster by default][html5ever].

[floki]: https://github.com/philss/floki
[tuple-doc]: https://hexdocs.pm/elixir/Tuple.html
[struct-doc]: https://hexdocs.pm/elixir/Kernel.html#defstruct/1
[map-doc]: https://hexdocs.pm/elixir/Map.html
[html]: https://w3c.github.io/html/syntax.html
[html5ever]: https://github.com/philss/floki#installing-html5ever
[benchmark]: https://gist.github.com/philss/58f56088db6d0334178ebed542eb422b
