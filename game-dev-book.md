# Table of Contents
##  1. Intro and Setup
##  2. Lua
##  3. More Lua
##  4. Love2D and a Snake
##  5. Tiles
##  6. Turn Based Rules
##  7. RPG
##  8. Physics
##  9. A platformer
## 10. Animation
## 11. Particle Systems and Advanced Graphics
## 12. File IO
## 13. Distribution and Release

# 1. Intro and Setup
TODO

# 2. Lua
## Hello world!
Great! You've just finish setting up your IDE and you're ready to make Call of Doots 3D Multiplayer MMORPG. Whoa! Hold your horses.

We're actually going to start off with something much more manageable that's easy to completely understand.

Pop open the `main.lua` file and enter:

    -- My first program!
    print("Hello, world!")

Then hit run. You've just written your first program.

`print` is a function that accepts an argument (that part in the double quotes). That argument is a string containing the text "Hello, world!". Strings are defined by a bunch of characters (other than `\` and `"` - you'll learn why later) between two double quotes. Here are some more strings:

    "SOMETHING FUNNY HERE"
    "123"
    "KIIIITTTYYYYYYYY!!!!"
    "totallynotapassword!@#$!@#!@#!@"

> Fiddle a bit with that code to see what else you can make it print.

And those two dashes at the start of the first line? Those tell Lua that the rest of the line is a comment that Lua can ignore (it's just a way for programmers to document code - for other developers and themselves in the future).

## Variables
Say you want to print a string out twice:

    print("Hello, world!")
    print("Hello, world!")

Look at that duplication! I have to either type that same string twice, or copy and paste it. As a good lazy programmer, lets make this simpler:

    message = "Hello, world!"
    print(message)
    print(message)

Much better. We've assigned that string to a variable named `message` and an can print it whenever we want to. If we want to change that string, we can easily access it in one place.

Variables can contain any value in Lua and can be named with alphanumeric characters and underscores (you'll see more possible values later on):

    a_cool_string = "my cool string"
    my_super_number = 1231231
    print(a_cool_string)
    print(my_super_number)

## Numbers
In that last part, a new feature of Lua has been introduced: numbers. Computers are basically glorified calculators, so every programming language knows how to handle numeric values. They can also do basic arithmetic operations:

    print(1 + 2) -- prints 3

    a = 4
    b = 2
    print(a + b) -- prints 6

    print(3 * a) -- prints 12

    print(3 ^ 2) -- prints 9 (its an exponent operator)

## More strings
Strings can also be slapped together (or concatenated) to form longer strings. You can concatenate values with the `..` operation:

    print("Hello " .. " World!") -- not that exciting
    print("Yo a number: " .. 5) -- kinda cool

    name = "Charlie"
    print("Hi " .. name) -- Neato!

## Let's make something

Learning about random programming language concepts in a vacuum isn't very conducive to actually learning to program, so let's get started writing an actual, practical project. Since this book is primary dedicated to game development, we're going to start by writing the most primitive, but elegant type of game: a text-based adventure.

We already know how to get output to the screen, but text-based adventures are a highly interactive medium. Often, only a sentence or two of outputted before a user command is required to move the game forward. So getting input seems like the next important feature to learn:

    -- print a prompt:
    print("What do you want to do?")
    -- read input (type something, then hit enter)
    input = io.read()
    -- print it back out
    print("You wnat to " .. input)

## Conditionals

Often, you'll want to make a computer behave differently depending on a certain condition. For instance, in a text based adventure, you'll want to print out a different message depending on whether the input is a valid command or not.

Let's see how to compare values using the equality operation `==`:

    print(1 == 1) -- prints true
    print(1 == 2) -- prints false
    print("some string" == "blah") -- prints false
    print("a string!" == "a string!") -- prints true
    print(1 == "1") -- prints false (think about why)
    print("a" .. "b" == "ab") -- prints true (concatenation happens before the check)

What's this `true` and `false` business?

Well, `true` and `false` are the two possible "boolean values" (they're values like anything else, so you can do things like `a = true` - try it out). The underlying logic of computers, from very simple to very complex, is entirely based on boolean values.

You can build more better logical statements using `or`, `and`, and `not`.

    -- or results in true if one of the sides is true
    print(true or false) -- prints true
    print(true or true) -- prints true
    print(false or false) -- prints false


    -- and requires both statements to be true if it evaluates to true
    print(true and false) -- prints false
    print(true and true) -- prints true
    print(false and false) -- prints true

    -- not just inverts a statment
    print(not true) -- prints false
    print(not false) -- prints true

    -- and they can be chained together to make a larger logical statment
    -- the parentheses can change the order of conditional checks, but are ignored of they aren't changing the order
    print(not false and (not true or not false)) -- prints true

    -- bring back the equality operator
    print("a" == "b" or "b" == "b") -- prints true

    -- less than and greater than can be used on numbers
    print(1 > 2 and 2 > 3) -- prints false
    print(not (1 > 2) and 2 < 3) -- prints true

    -- and lets pull some variables into the mix
    a = true
    b = "x" == "y"

    print(b or a) -- prints true
    print((b or a) and (not b)) -- prints true

Let's actually use these conditions to control the program now. An `if` statement is used to only run a certain piece of code when a boolean evaluates to `true`:

    -- always remember to put a then after the conditional statment
    if true then
        print "hey from inside an if block!" -- this will get printed
    end -- and don't forget your `end`s!

    if false then
        print "forever alone" -- will never be printed
    end

    -- do some logic!

    str1 = "logic, baby!"
    str2 = "logic, baby!"

    if str1 == str2 then
        print(str1 .. " is equal to " .. str2)
    end

    -- ~= is shorthand for inverting equality. So this:
    if not (str1 == "some string") then
        print("they're not the same") -- this gets printed
    end

    -- is equivalent to this:

    if str1 ~= "some string" then
        print("they're not the same") -- and this does too
    end

You might be able to guess where we're going with this now. Since we can check a value and run different code depending on what it is, we can use this to validate input:

    print("Type something!")
    input = io.read()

    if input == "something" then
        print("very funny >_<")
    end

    if input ~= "something" then
        print("You entered: " .. input)
    end

This last piece of code seems a bit clunky, since we're repeating the entire condition just to check the inverse of the statement. It is clunky. That's why the `else` statement exists.

    -- just replace the if statement
    if input == "something" then
        print("very funny >_<")
    else -- in any case where input doesn't equal "something", run the following code:
        print("You entered: " .. input)
    end

## Functions
If variables can be used to store a value, how would you store a set of Lua operations in a manageable chunk?

This is where functions come in. If you've used functions in Algebra (don't worry if you haven't - function are pretty clear once you use them a bit), they're a bit like that (though algebraic functions actually map a value from one set to another - Lua functions are actually algorithms - but that's semantics). A function can be defined like this:

    function cool_hello_world()
        print("'sup, World?")
    end

If you run the code now, nothing will happen. This is because the code in the function isn't actually run *until* you call it. Now you can call the function:

    cool_hello_world()

## Function arguments

Remember how `print` takes an argument? An argument is a value that's passed into a function. If you imagine a function being a black box, an argument is like a window that you can use to drop something into it. We could pass a name to our `cool_hello_world` to make it a bit smarter:

    function cool_hello(name)
        print("'sup, " .. name .. "?")
    end

    cool_hello("world")

    n = "kitty"
    cool_hello(n)

## Scope

Variables in Lua are "global" by default. That means, once they're defined, they can be accessed anywhere within the program (the only exception is function arguments - 'cause that doesn't make a whole lot of sense - it's just a dummy value to pass something into the function). For instance:

    print(a) -- nil, which is Lua's way of saying it's empty
    function set_a(val)
        a = val
    end
    print(a) -- still nil, but watch what happens next
    set_a(5)
    print(a) -- it's now 5!

We can protect a value by prefixing its definition with `local`

    function set_secret(val)
        local a_secret = val
    end

    print(a_secret) -- nil
    set_secret("val!")
    print(a_secret) -- still nil - get rekt

It may not be clear why we'd want to do that right now, but you'll see why the `local` keyword is used later.

The important thing to remember right now is that if a global value is defined in a function, *that function must be called to set it*.

## Returning Values

If there's some way to get a value into a function, its reasonable there's a similar way to get it out. Coming back to the analogy of a black box, there's a window that we can put something into and a window that we can pull something out of. To get it out:

    function get_a_value_out()
        return "a value"
    end

    function get_three()
        return 3
    end

    v = get_a_value_out()

    print(v) -- prints "a value"
    print(get_three()) -- prints 3

## Tables

Lua's only concept of structured data is tables. A table is like a dictionary. It's a collection of keys (think the words of a dictionary) and values (the dictionary definitions). When you want to get data out, you can request the paired value by passing a key:

    my_table = {a = 1, b = "blah"}
    print(my_table) -- prints 'table' followed by a number
    print(my_table["a"]) -- prints 1
    print(my_table["b"]) -- prints blah
    print(my_table.a) -- equivalent to my_table["a"]

You can also set a table's key after its definition (kind of like adding a new definition to the dictionary):

    my_table = {a = 1, b = "blah"}
    print(my_table["c"]) -- its nil
    my_table["c"] = "a string"
    print(my_table["c"]) -- prints "a string"

If no keys are assigned to the table, the numeric position in the list (also known as the index) is used to access the value:

    my_list = {"a", "b", "c"}
    my_list[4] = "d"

    print(my_list[1]) -- prints "a"
    print(my_list[2]) -- prints "b"
    print(my_list[4]) -- prints "d"

    -- you can set any arbitrary index too
    my_list[13] = "SPARSE ARRAYS FTW"

    print(my_list[13]) -- prints "SPARSE ARRAYS FTW"

## Functions as values

Functions can be passed around and assigned like any other value (if you don't give it a name):

    a = function()
        return 3
    end

    print(a()) -- prints 3

    b = function()
        return function()
            return "woah! sub function"
        end
    end

    print(b()()) -- call a function that returns a function THEN CALL THAT

This is useful because you can set a table value to a function:

    t = {
        fun = function()
            return "some string"
        end
    }

    t["fun2"] = function()
        print("more function shtuff")
    end

    print(t.fun()) -- prints some string
    t.fun2()

It's often useful to structure code as a collection of tables with functions and attributes bound together within a table. This type of pattern is often referred to as an object.
