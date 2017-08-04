---
layout: post
title: Avoid Conditionals in Elixir
category: elixir
published: false
---

I used to love conditionals. I think everybody does. It gave us the ability to
decide what the system should do depending on many factors. It was a silver
bullet. Not until I started writing in Elixir.

Elixir has introduced a fairly new concept to my head called *Pattern Matching*.
It is somewhat similar to regular expressions but is different in many ways. We
can use the power of pattern matching to avoid conditionals and thus write a
clear and understandable code without the *if* and *else* statements.

Here's a basic example.

```elixir
[a, b, c] = [1, 2, 3]
a # 1
b # 2
c # 3

[ head | tail ] = [1, 2, 3, 4, 5, 6, 7]
head # 1
tail # [2, 3, 4, 5, 6, 7]
```

Elixir tries to match the expression on the right with the expression on
the left.

We can even use it on functions.

```elixir
defmodule MyFile do
  def read_file({:ok, file}) do
    "the file exists"
  end

  def read_file({:error, reason}) do
    "the files DOES NOT exist"
  end
end
```

And we can use the above module like so:

```elixir
result = MyFile.read_file(File.open("does not exist.txt"))
IO.puts(result) # the files DOES NOT exist
```

As you can see with the above example, we just avoided the possibility of adding 
a conditional logic. This is how we may
