# Discover Ruby!

If you have Ruby installed on your computer, open a terminal window and type `irb`.
A special session will start that allows you to type any Ruby code you want and
see the results immediately!

If you don't have Ruby installed or aren't yet comfortable with the command line,
check out [REPL.it](http://repl.it/languages/Ruby)
which lets you type Ruby code in the left window and see the results on the right.
Be warned, repl.it uses an old version of Ruby, so not all the newest tricks
will work, but everything in this guide will be fine.

## Start Exploring

So, whichever way you've chosen to try Ruby, there's a blank screen staring back
at you, waiting for you to give it instructions. What sorts of instructions are
there? The rest of this post gives you things to try out in Ruby, grouped by
tasks and ideas you might have, like "lists" and "transforming" and the
difference between a recipe and a meal.

Feel free to try things. It's completely safe: you can't break your computer.
Exploring is the best way to learn. It's also a lot of fun!

## Buckets with labels (aka "variables")
```
his_name   = "Bob"
her_name   = "Jane"
a_number   = 1
some_words = "three blind mice"
an_array   = [ 1, 2, 3 ] # see "Arrays", below
```
Variables are buckets with labels that carry around whatever you put to the right of
the equal sign. You'll see below that when we use the variable name (the "label"),
we get back whatever we put inside it. *Ask for the bucket, you get what's in it.*

## Display (aka "output")
```
puts "Hello World!" # displays "Hello World!" on the screen on its own line
print "the" # displays "the"
puts "ater" # displays "theater", because previous print didn't finish with a linebreak
puts "His name is: #{his_name}" # displays "His name is: Bob"
puts "#{his_name} is friends with #{her_name}" # displays "Bob is friends with Jane"
```

In this guide, we show you the result of the code snippets by magic, but to see
anything in your terminal, you need to display it somehow. `puts` (short for
  "put string") is the most common, but `print` and `p` have their uses, as well.
  Try them out and see how they differ. (Hint: maybe on an array?)

The weird ```#{his_name}``` thing is a way to say "put the contents of this
bucket here in my output", so the output will contain "Bob" or "Jane".

## Choices (aka [conditionals](http://ruby-doc.com/docs/ProgrammingRuby/html/tut_expressions.html#UH))

```
if (a == 1)
  "one"
elsif (a < 5)
  "a few"
else
  "lots"
end

a = 1  # => "one"
a = 2  # => "a few"
a = 10 # => "lots"
```

We don't always know in advance what the program will need to do, so we use
"conditionals" to handle multiple possibilities. The important detail is that
the first conditional that matches the situation "wins" and its code will run.
Nothing afterward will be run. If nothing matches, the program does nothing and
continues on as if nothing happened. The `else` clause catches everything, so
make sure you put it last. ;-)

Note that ```a == 1``` has a *pair* of equal signs. One equal sign means "put
this in the bucket" but a pair says "compare what's in the bucket to what's on
the right side".

## Lists (aka [Arrays](http://www.ruby-doc.org/core-2.1.1/Array.html))

```
ary = [ "one", "two", "three" ]

ary[0]    # => "one"
ary[1]    # => "two"
ary.first # => "one"
ary.last  # => "three"
ary << "four"
ary       # => [ "one", "two", "three", "four" ]
```

**Fun Fact:** we get the first item in the list with the number zero because
arrays need to know *how far from the beginning of the list* your item is.
The first item is *zero* items away from the beginning of the array. The
second is *one* element from the beginning. Weird, I know, but virtually all
programming languages do it this way, so we can't complain **too** loud. ;-)

## Named Groups (aka [Hashes](http://www.ruby-doc.org/core-2.1.1/Hash.html))

```
bob = { "name" => "Big Bob", "address" => "123 Elm St." }
jane = { "name" => "Lady Jane" }
bob["name"] # => "Big Bob"
bob["address"] = "123 Elm St."
bob.keys # => [ "name", "address" ]
bob.values # => [ "Big Bob", "123 Elm St." ]

friends = [ bob, jane ]
friends[0]["name"] # => "Big Bob"
friends.last["name"] # => "Lady Jane"
```

Hashes are great when we have data we need to look up, like
finding someone's phone number when all you know is their name. We don't care
who's first or last, so an array can't help us. These "name-value pairs"
can be really handy for making things like phone books or dictionaries, as
shown below.

```
phone_book = { "bob" => "616-555-1212", "jane" => "616-555-1234" }
dictionary = {
  "Ruby" => "Ruby is an awesome programming language",
  "Python" => "Python is an excellent choice, too"
}
phone_book["bob"] # => "616-555-1212"
```

## Walking a list (aka "iteration")
```
ary = [ 1, 2, 3 ]
ary.each do |item|
  puts item
end
```

It's often handy to do something with each item in an array, so arrays have a
method called `each` to do just that. It walks through the array in order and
hands you a single item in a variable found between the "pipe" characters.
(You'll have to hunt for it on your keyboard, but it's there!)
In this case, the variable is called `item`.

This code will output the three numbers in the array, one to a line. This task
is much uglier in many other languages, so this is a popular feature in Ruby. :-)

## Transforming (aka [Mapping](http://ruby-doc.org/core-2.1.1/Enumerable.html#method-i-map), [Selecting](http://ruby-doc.org/core-2.1.1/Enumerable.html#method-i-select), [Reducing](http://ruby-doc.org/core-2.1.1/Enumerable.html#method-i-reduce))

```
nums = [ 1, 2, 3 ]
nums.map{ |num| num * 2 } # => [ 2, 4, 6 ]
names = [ "bob", "jane" ]
names.map{ |name| name.upcase } # => [ "BOB", "JANE" ]

nums.select{ |num| num > 2 } # => [ 3 ]
nums.select{ |num| num.odd? } # => [ 1, 3 ]

nums.reduce{ |sum,num| sum + num } # => 6

nums.map{ |n| n * 2 }.reduce{ |sum,n| sum + n } # => 12
```

A surprising amount of programming involves "doing something" with a bunch of
data (typically in an array), and these are the big three tasks: we can change
each piece of data with a `map`, filter to just the items we're interested in
with a `select` and/or combine them into a single thing with a `reduce`.

## Jobs (aka "methods")
```
def speak words
  puts words
end

speak("Hello World!") # displays "Hello World!" on the screen
speak("Ruby is awesome!") # displays "Ruby is awesome!" on the screen
```

Sometimes we have certain jobs we want to do again and again, maybe with small
differences each time. To keep from having to write the code again and again,
we "define" a chunk of code called a "method" using the `def` command followed
by the name of the method and a list of variables (aka "arguments")
the methods needs (if there are any) separated by commas. We put `end` after
the code so Ruby knows where to stop running the code.

In our example, we define a method called `speak` that takes one argument
called `words`. It uses `puts` to output the contents of the `words` argument
and then ends. Ruby goes back to where you called `speak` and continues
running the rest of your code.

## Recipes and Meals (aka [Classes](http://www.ruby-doc.org/core-2.1.1/Class.html) and [Objects](http://ruby-doc.com/docs/ProgrammingRuby/html/tut_classes.html#S2))

```
class Greeter
  def initialize(greeting)
    @greeting = greeting
  end

  def greet(name)
    puts "#{@greeting} #{name}"
  end
end

cowboy  = Greeter.new("howdy")
hipster = Greeter.new("yo")
cowboy.greet("Bob") # "howdy Bob"
hipster.greet("Jane") # "yo Jane"
```

You can't eat a recipe, but you can make a meal by following its instructions.
We put the instructions inside of a `class`, which gets a name (in this case,
  `Greeter`). Notice the `end` at the bottom, so Ruby knows where your recipe
ends!

We tell Ruby to "make a meal" by using the name of the class followed by `new`.
Anything we hand to `new` (in this case, "howdy" and "yo") get passed along
to the `initialize` method, which Ruby calls itself when it's done with all the
other tasks required to make a new object.

We put this new object in a bucket with a useful ("intention-revealing") name
so we can give it orders later on.

But there are **two** methods defined inside `Greeter`! The other one is `greet`
and it gets copied into every object, so all the objects we create can call it.

The other weirdness is that `@greeting = greeting` thing. Why are we assigning
the contents of greeting to itself? That `@` sign is important: that makes it
a variable that lives inside the object, invisible to the outside world. However,
the `greet` method is inside the object, so it can see `@greeting`, as we can see
on the `puts` line.

## You've begun your adventure!

There are lots of places you can go with Ruby now that you've gotten some of the
basics under your belt. May I humbly recommend
[7 Degrees of FizzBuzz](http://billgathen.com/2013/01/18/7_degrees_of_fizzbuzz.html)?
You have *almost* all the info you need to do the first few steps of the challenge,
though you'll want to investigate either [Range](http://www.ruby-doc.org/core-2.1.1/Range.html)
or [.upto](http://ruby-doc.org/core-2.1.1/Integer.html#method-i-upto) to get going.

Exploring and discovering new things on your own will be part of your daily
life as a programmer, so embrace it and find the joy in finding things out.

Best of luck. I believe in you!
