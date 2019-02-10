\newpage

# FizzBuzz

Of course, the first thing that your job interview for that cushy new
Crystal job will task you with is building FizzBuzz. Let's do it!

If you're not familiar, FizzBuzz is a simple programming problem:

> "Write a program that prints the numbers from 1 to 100. But for multiples of
> three print “Fizz” instead of the number and for the multiples of five print
> “Buzz”. For numbers which are multiples of both three and five print
> “FizzBuzz”."

This will give us a good excuse to go over some basics of Crystal: Looping,
tests, printing to standard output, and a host of other simple things.

First, let's create our project.

    $ crystal init app fizzbuzz

Let's write our first failing test. Open up `/spec/fizzbuz_spec.cr`

```ruby
require "./spec_helper"

describe Fizzbuzz do
  it "shouldn't divide 1 by 3" do
    div_by_three(1).should eq(false)
  end
end
```

And run it:

    $ crystal spec
    Error in ./spec/fizzbuzz_spec.cr:7: undefined method 'div_by_three'

    div_by_three(1).should eq(false)


This makes sense: We haven't defined any method yet. Let's define
one:

```ruby
require "./fizzbuzz/*"

def div_by_three(n)
  false
end
```

Akin to Ruby, the value of the last expression gets returned.

TDD means do the simplest thing! Now that we've defined our method, let's compile and run our tests:

    $  crystal spec
    .

    Finished in 0.82 milliseconds
    1 examples, 0 failures, 0 errors, 0 pending


Awesome! We pass! Let's write another test, and see what happens:

```ruby
require "./spec_helper"

describe Fizzbuzz do
  it "shouldn't divide 1 by 3" do
    div_by_three(1).should eq(false)
  end

  it "should divide 3 by 3" do
    div_by_three(3).should eq(true)
  end
end
```

Run it!

    $ crystal spec

    .F

    Failures:

      1) Fizzbuzz should divide 3 by 3
         Failure/Error: div_by_three(3).should eq(true)

           expected: true
                got: false

         # ./spec/fizzbuzz_spec.cr:9

    Finished in 0.83 milliseconds
    2 examples, 1 failures, 0 errors, 0 pending

    Failed examples:

    crystal spec ./spec/fizzbuzz_spec.cr:8 # Fizzbuzz should divide 3 by 3

We have 1 failure. Let's make this pass.

```ruby
require "./fizzbuzz/*"

def div_by_three(n)
  if n % 3 == 0
    true
  else
    false
  end
end
```

Run it.

    $ crystal spec

    ..

    Finished in 0.61 milliseconds
    2 examples, 0 failures, 0 errors, 0 pending

Awesome! This shows off how `else` work, as well. It's probably what you
expected. Go ahead and try to refactor this into a one-liner.

Done? How'd you do? Here's mine:

```ruby
def div_by_three(n)
  n % 3 == 0
end
```

Remember, the value of the last expression gets returned.

Okay, now try to TDD out the `div_by_five` and `div_by_fifteen` methods. They
should work the same way, but this will let you get practice actually
writing it out. Once you see this, you're ready to advance:

    $ crystal spec -v

    Fizzbuzz
      shouldn't divide 1 by 3
      should divide 3 by 3
      shouldn't divide 8 by 5
      should divide 5 by 5
      shouldn't divide 13 by 15
      should divide 15 by 15

    Finished in 0.61 milliseconds
    6 examples, 0 failures, 0 errors, 0 pending

Okay! Let's talk about the main program now. We've got the tools to
build FizzBuzz, let's make it work. First thing we need to do is print
out all the numbers from one to 100. It's easy!

```ruby
100.times do |num|
  puts num
end
```

Step one: print **something** 100 times. If you run this via
`crystal build src/fizzbuzz.cr && ./fizzbuzz` you should see `num` printed
100 times. Note that our tests didn't actually run. Not only are they not run,
they're actually not even in the executable:

Now we can put the two together:

```ruby
100.times do |num|
  answer = ""

  if div_by_fifteen num
    answer = "FizzBuzz"
  elsif div_by_three num
    answer = "Fizz"
  elsif div_by_five num
    answer = "Buzz"
  else
    answer = num
  end

  puts answer
end
```

Because the `if` returns a value, we could also do something like this:

```ruby
(1..100).each do |num|
  answer = if div_by_fifteen num
    "FizzBuzz"
  elsif div_by_three num
    "Fizz"
  elsif div_by_five num
    "Buzz"
  else
    num
  end

  puts answer
end
```

Notice that we also changed `100.times` to `(1..100).each`, to make `num` go from 1 to 100 instead of from 0 to 99.

Try running it.

Awesome! We've conquered FizzBuzz.
