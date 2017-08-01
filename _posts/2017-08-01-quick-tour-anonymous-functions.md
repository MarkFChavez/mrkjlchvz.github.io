---
layout: post
title: Anonymous Functions with Elixir
---

Anonymous functions are simply functions or methods that is not assigned a
name. While named functions are very much a common thing, anonymous functions
has its good uses too especially in Elixir.

### Basic example

```elixir
hello_world = fn -> IO.puts("Hello world") end
hello_world.() # Hello world
```

<!--break-->

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

### Anonymous function can also access variables outside of it

```elixir
fact = "I love Elixir"
fun = fn -> "Hey, #{fact}" end

fun.() # Hey, I love Elixir
```

### Passing a function as an argument

```elixir
fun = fn(name) -> "Hello #{name}" end

# ... inside a module ...
def accept(fun, value) do
  IO.puts fun.(value)
end

Module.accept(fun, "Elixir Programmer!") # Hello Elixir Programmer!
```

The above example basically shows how some of `Enum`'s method work.

```elixir
# Enum.map
list = [1, 2, 3, 4]
add_one = fn(number) -> number + 1 end

Enum.map list, add_one # [2, 3, 4, 5]
```

Happy reading!
