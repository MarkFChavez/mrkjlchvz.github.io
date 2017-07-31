---
layout: post
title: Anonymous Functions with Elixir
published: false
---

Anonymous functions are simply functions or methods that is not assigned a
name. Below are some examples.


### Basic example

```elixir
hello_world = fn -> IO.puts("Hello world") end
hello_world.() # Hello world
```

### With arguments

```elixir
multiply = fn(a, b) -> a * b end
multiply.(5, 5) # 25
```

### Combined with pattern matching

```elixir
answer = fn
  "Yes" -> "You are correct"
  "No" -> "You are wrong"
  _ -> "I cannot understand your answer"
end

answer.("Yes") # You are correct
answer.("No") # You are wrong
answer.("Maybe") # I cannot understand your answer
```

### Return a function

```elixir
outer = fn ->
  fn(x) -> "Inner function with value: #{x}" end
end

outer.().(30) # Inner function with value: 30
```
