---
layout: post
title: 'Introduction: JavaScript Event Loop'
category: javascript
published: false
---

Today I want to talk a bit about the **Event Loop**. If you want to get deeper
with JavaScript, it is very essential to understand the internals. For this
article, I want you to at least keep these terms in mind.

1. Call Stack
2. Event Table
3. Event Queue
4. Event Loop

Let's get started.

### How It Works

JavaScript executes a program differently. Unlike with other programming languages the actual skeleton of execution is not explicitly obvious.

JavaScript behaves differently when it comes to handling asynchronous
messages.

Let's use **Ruby** to demonstrate this case.

```ruby
# let's assume that this is an asynchronous call to some API
sleep 5000

puts "We're done here"
```

If you are someone who is familiar with **Ruby**, then the above code is not
difficult to absorb. To put simply, the process waits for `5000 ms` or an equivalent of `5 seconds` before actually printing the message `We're done here` in the console.

#### Output:
```markdown
# this message shows after 5 seconds
We're done here
```

Nothing unusual, right? After all, it is intuitive that a program executes each line starting from top to bottom.

However, **JavaScript is different.** Let's check how the above program behaves if we use
JavaScript.

```javascript
// async call
setTimeout(function () {
  console.log('I am async')
}, 5000)

console.log('hello world')
```

#### Output:

```markdown
hello world

# shows up after 5 seconds
I am async
```

As you have noticed, `hello world` showed up immediately and after some time has
passed, `I am async` then shows up.

When an asynchronous function is called in JavaScript, the program still continues going down the path of execution until it finishes.

### Going Deeper