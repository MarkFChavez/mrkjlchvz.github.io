---
layout: post
title: The Hidden Complexity of Ruby
---

Ruby's simplicity has reached a whole new level. It has given developers a new approach to writing code. For me, coding
should be fun and that's what Ruby has always been. This feature has enabled us not to think about code too much but focus
more on the business side.

Why am I saying this?

Because once a developer has focused on the business, it keeps our clients happy and we get to keep our jobs. More value means success.

Let me show you a block of `ruby` code.

```ruby
list_of_characters = Character.all

list_of_characters.each do |character|
  puts character.name
  puts "List of weapons:"

  character.weapons.each do |weapon|
    puts weapon.name
  end
end
```

The above code is simple, and easy to understand. But this is something that has a hidden cost. In the context of Rails,
we call this the `N+1` problem. This article is not going to discuss the `N+1` problem but conceptually, it means more
unnecessary database calls and performance issues.

What I am trying to say is that developers new to Ruby or Rails may have abused the simplicity that `ruby` offers. This is just one of the many problems that `ruby` developers has to be aware of.

No wonder that there are a lot of `Ruby on Rails is dead.` and `Ruby on Rails does not scale.` articles showing up on the web and it really creeps me up.

It's about time to step up and stop blaming `ruby` for whatever problems that we have. Because it is a language that scales and performs very well just like any other languages and we just need to be aware of it.

Understand how Ruby's GC works.

Learn how to benchmark effectively.  

Know when and when not to use `ActiveRecord` for your queries.

And lastly, make it simple.
