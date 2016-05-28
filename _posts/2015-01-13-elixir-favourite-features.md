---
layout: post
title:  "Elixir, Favourite Features"
date:   2015-01-13 18:08:00
disqus: y
categories: elixir
---
I've been playing around with [Elixir](http://elixir-lang.org) for a while now,
which is described as a "dynamic, functional language designed for building scalable
and maintainable applications" on their homepage.

Having recently stabilised at v1.0.0, with a great community, now is a great time
to check out Elixir. An excellent introduction is available via the
[Getting Started](http://elixir-lang.org/getting-started/introduction.html) guide, or if
you're interested in a more in-depth introduction I have read and can recommend
[Programming Elixir](https://pragprog.com/book/elixir/programming-elixir) by
[David Thomas](http://pragdave.me).

I'll show you a couple of my favourite features with some code examples.

---

### Guard Clauses

Here is an example implementation of [FizzBuzz](http://c2.com/cgi/wiki?FizzBuzzTest)
using guard clauses:

```elixir
defmodule FizzBuzz do
  def get(n) when rem(n, 15) == 0, do: "FizzBuzz"
  def get(n) when rem(n, 3) == 0, do: "Fizz"
  def get(n) when rem(n, 5) == 0, do: "Buzz"
  def get(n), do: to_string(n)
end
```

Trying it out with [IEx](http://elixir-lang.org/docs/master/iex/IEx.html) (Elixir's
REPL):

```elixir
iex(2)>  1..15 |> Enum.map(&(FizzBuzz.get(&1)))
["1", "2", "Fizz", "4", "Buzz", "Fizz", "7", "8",
 "Fizz", "Buzz", "11", "Fizz", "13", "14", "FizzBuzz"]
```

The do is executed for the first clause that is matched. If no clauses are
matched, an error will be raised. I think this is a very readable solution.
For example I would read the 2nd clause as "get, when n is evenly divisible by 3,
is Fizz".

### Pattern Matching

Here is the _encode function from [base58](https://github.com/jrdnull/base58)
a module I wrote to deal with Base58 encoding:

```elixir
defp _encode(0, []), do: [@alphabet |> hd] |> to_string
defp _encode(0, acc), do: acc |> to_string
defp _encode(x, acc) do
  _encode(div(x, 58), [Enum.at(@alphabet, rem(x, 58)) | acc])
end
```

This function is the private implementation (defp rather than def) for the encode
function. Having a private implementation like this allows for a nicer public
interface by excluding the accumulator from the function arguments.

Here the _encode function has multiple clauses matching on the value of the
arguments, with the base cases first. Instead of multiple return points there
are three conscise functions dealing with the different conditions of a call.

### The Pipe Operator

My absolute favourite feature of Elixir at the moment is the
[pipe operator](http://elixir-lang.org/getting-started/enumerables-and-streams.html#the-pipe-operator),
which takes the value from the left and passes it to the first argument of the
function call on the right.

Here is some example code written without the pipe operator:

```elixir
iex(1)> String.downcase(String.strip(" Hello ELIXIR  "))
"hello elixir"
```

Now with the pipe operator:

```elixir
iex(2)> " Hello ELIXIR  " |> String.strip |> String.downcase
"hello elixir"
```

The second version can be read in a more natural way from left to right, rather
than from the inside out.

---

I think Elixir will continue to gain popularity, especially with great projects
in the work such as the [Phoenix Framework](http://www.phoenixframework.org/).
I've also found the community to be very welcoming and you'll find me hanging out
in #elixir-lang on [Freenode](http://freenode.net).
