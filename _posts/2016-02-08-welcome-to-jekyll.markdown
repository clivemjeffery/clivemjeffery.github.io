---
layout: post
title:  "First Past the Fence Post"
---
In this, one of my first posts, I'm experimenting with Jekyll code blocks and syntax highlighting with [Rouge](http://rouge.jneen.net). The code blocks below are all about that.

This one is specified by liquid tags:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

This one with fenced code blocks (using backticks):

``` ruby
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
```

The have a different background.

Here's a fenced HTML one (using tildes):

~~~ html
<a href="#">Hello world</a>
~~~

Which to prefer? Backticks are easier to type (no shift) but tildes are easier to read in the plain text. Hmmm, I'll probably be inconsistent then.

and here is a an inline code snippet `pupils.for_each(|p| { printf p.name })` but I don't know how to specifiy the language for that.

This is yet another fencing style:

``` ruby
loop
  $stdout 10.to_s
end
```
