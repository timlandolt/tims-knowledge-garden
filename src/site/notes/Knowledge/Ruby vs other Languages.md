---
{"dg-publish":true,"permalink":"/knowledge/ruby-vs-other-languages/"}
---

Ruby's syntax is made for programmers and not for the computers. That means it should be readable like regular English sentences. For example:

```ruby
5.times { print "hi" }

print x unless y
```

I found that core principle to be one of the most significant differences. Other features that play into that concept are:

```ruby
# Dynamic typing 
x = "Hello"
x = 5

# Everything is a class, in java you would have to use wrapper classes
3.times { puts "Hello" } 

# Methods can be called witout parantheses
my_method "hello", 5 #=> same as my_method("hello", 5)

# 'unless' in addition to 'if'
unless x do
  puts "Hi"
end
# same as
if !x do 
  puts "Hi"
end
```