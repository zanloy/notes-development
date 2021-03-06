---
id: i53GWC2BpQBEoTNuX0hfF
title: String
desc: ''
updated: 1640743426198
created: 1640571053818
---
## Construct

A string literal can be represented using either double quotes or single quotes. The difference between these two is that anything within double quotes will have [[interpolation|#interpolation]].

```ruby
myvar = 'breakfast'
puts "I love #{myvar}!"
# output: I love breakfast!
puts 'I love #{myvar}!'
# output: I love #{myvar}!
```

## Convention

The Ruby convention is to use double quotes only when you are using [[interpolation|#interpolation]] and single quotes when it is a string literal.

```ruby
# good
myvar = 'a good person'
# also good
also_my_var = "I always try to be #{myvar}."
```

## Concatenation

Strings can be concatenated with a simple `+`, by using [[interpolation|#interpolation]], or using the [concat function](https://ruby-doc.org/core/String.html#method-i-concat).

```ruby
hour = '4'
minutes = '20'

puts hour + ':' + minutes
# output: 4:20
puts "#{hour}:#{minutes}"
# output: 4:20
puts hour.concat(':').concat(minutes)
# output: 4:20
```

## Interpolation

A variable in a string literal is defined by using `#{var}` syntax.

```ruby
myvar = 'a string'
puts "I made #{myvar}!"
# output: I made a string!
```

## Documentation

[Ruby:String](https://ruby-doc.org/core/String.html)
