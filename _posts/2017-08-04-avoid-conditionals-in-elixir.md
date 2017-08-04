---
layout: post
title: Avoid Conditionals in Elixir
category: elixir
---

I used to love conditionals. I think everybody does. It gave us the ability to
decide what the system should do depending on many factors. It was a silver
bullet. Not until I started writing in Elixir.

Elixir has introduced a fairly new concept to my head called *Pattern Matching*.
It is somewhat similar to regular expressions but is different in many ways. We
can use the power of pattern matching to avoid conditionals and thus write a
clear and understandable code without the *if* and *else* statements.

Consider this example.

```elixir
defmodule HelloCountry do
  def for(country) do
    if language == "america" do
      "Hello"
    else if language == "japan" do
      "Kon'nichiwa"
    else if language == "china" do
      "Nǐ hǎo"
    end
  end
end
```

The above example looks typical. Coming from the ruby language, I can safely say
that this is a usual solution but not a good one though. Personally, having a
conditional logic in a function brings a bunch of complexities. 

Why?

Because it makes me think. I don't want to waste my precious time thinking (I'm sure you do too) whether the
expression returns true or false.

### The Elixir way of doing things

With Elixir, we can use pattern matching directly on functions to make sure that
we only call this function if the pattern matched. It basically looks like a
group of overloaded methods (if you came from a Java background) but their
patterns are different respectively.

You should be alarmed when you see a conditional logic in our Elixir code.

```elixir
defmodule HelloCountry do
  def for(country = "america"), do: "Hello"
  def for(country = "japan"), do: "Kon'nichiwa"
  def for(country = "china"), do: "Nǐ hǎo"
end

HelloCountry.for("america") # Hello
HelloCountry.for("japan")   # Kon'nichiwa
HelloCountry.for("china")   # Nǐ hǎo
```

Pattern matching is one of the core features that made me love this language.

Happy reading!
