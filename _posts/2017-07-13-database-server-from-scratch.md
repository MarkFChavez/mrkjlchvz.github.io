---
layout: post
published: false
title: Building a Mock Database Server from Scratch in Elixir
---

Hello again! So I decided to build a mock database server in Elixir without
using **GenServer**. In the real world, this is probably something that we 
won't do since **GenServer** provides pretty much all the capabilities that
a server would need. 

First, I want to let you know that the working code is on my GitHub account. You
can check the repo by clicking [here](https://github.com/mrkjlchvz/mock_database_server).

### How does it work?

Basically, what this does is mock a running database server that of course, runs
in an individual long-running server process. In this context, a **long-running
server process** is just a method that does a tail recursion which means it
continuously listens for messages in its process mailbox.

### What is a process mailbox?

Every time you send a message to a process, that process then stores the
message in a mailbox. If the process is ready to receive one, it will process
the first message that happens to be inserted first similar to a FIFO queue.

### Starting the server process

Starting up the server is a trivial job.

```elixir
def start do
  spawn(&loop/0)
end
```

Calling the **start** method spawns a new process that calls **loop**.

```elixir
defp loop do
  receive do
    {:run_query, caller, query_def} ->
      send(caller, {:query_result, run_query(query_def)})
  end

  loop()
end
```

The **loop** method is the one responsible for continuously receiving
messages from its clients. I marked it as a private method because it does not
need to be called outside the module and that's fine. As you have noticed, `loop()` is
executed every time the method ends. This is called recursion and lets
the server handle continuous messages.
