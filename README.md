# Cards - Intro to Elixir App

My first Elixir application. Written along with Stephen Grider's [Elixir and Phoenix Bootcamp Course](https://www.udemy.com/the-complete-elixir-and-phoenix-bootcamp-and-tutorial/). Notes here are a combination of notes from that course, review of [The Officia Elixir Documentaion](https://elixir-lang.org/docs.html), and [The Elixir School Website](https://elixirschool.com/en/lessons/basics/collections/)

# Notes

**Modules** - most code in Elixir is organized in modules
**module** - a collection of methods or functions
**iex** - Interactive Elixir Shell

`iex -S mix` starts iex

Elixir modules have an implicit return, the last value in a function is automatically returned

Convention is to use double quotes throughout all Elixir code

##Elixir Design Patterns

Elixir code is written using the Functional Programming Paradigm
Avoid writing if statements, use pattern matching and a case statement

- by convention, cases should be one line of code

### OOP vs FP - Creating a Deck of Cards

#### OO Approach

Create a `Card` Class
card class would have suit and value properties

Create a `Deck` Class

- collection of `Card` instances
- shuffle method
- save method
- load method

In OOP, Deck methods would operate on the local instance variable of a given deck

#### FP Approach

- Cards Module - stand alone object that does not have any concept of instance variables

* Modules are collections of methods and nothing more
  - `create_deck` method would return a list of cards
  - `shuffle` would take in a deck and return a shuffled deck
  - `save` would take in a deck and return a path to the saved file
  - `load` would take in a path to the saved file and return the deck

In Elixir, there can be multiple methods that share a name. Those methods can be differentiated by a

`method_name/number_of_arguments` syntax

The number of arguments that a function accepts is called **arity**

## Basic Data Types

- `Integers`
- `Floats`
- `Booleans`
- `Atoms`
- `Strings`

Atoms vs Strings -

- Strings are info that will be passed to user
- Atoms are used to differentiate error messages for devs

## Collections

- `Lists` - simple collections of values which may include multiple types
  - represented with `["square", "brackets]`
  - can be broken up into Head`hd` and Tail`tl`
  - Head is the first element, Tail is remaining elements
- `Tuples`- similar to lists, but stored differently in memory in a way that makes accessing length faster, but modifying the collection more expensive.
- `Keyword lists` - special lists of two element tuples, whose first element is an atom
  - similar to a JS object

```elixir
[foo: "bar", hello: "world"]
[foo: "bar", hello: "world"]
```

- keys must be atoms
- keys are not ordered
- commonly used to pass options to functions

- `Maps` - go-to key-value data structure
  - allow keys of any type
  - defined with `%{}` and hash rockets `=>` between key-value pairs
  ```elixir
  %{"hash" => "rocket", "test" => "Map"}
  ```
  - if a duplicate is added to a map, it replaces the old value

## Relationship btw Elixir and erlang

Elixir is compiled to erlang. Sometimes, we will need to access the erlang library

---

## Modules Used In This Project

[**Enum**](https://hexdocs.pm/elixir/Enum.html) is an Elixir module used for enumerating over enumerables

- some common and familiar enum functions - `map` `each` `filter` `reduce` `sort`
- Enumerables in Elixir include Lists, Maps, and Ranges. Tuples are not enums.

- Functions in the Enum module work in linear time.
  - For this reason, it is more performant to prepend items to Lists than to append them.
  - Lists in Elixir are not Arrays like in JS or Ruby, they are instead Linked Lists

[**List**](https://hexdocs.pm/elixir/List.html) is an Elixir module for working with Lists

`split(enumerable, number_of_records)`

### Immutability in Elixir

Shuffle copies a list, creates a new list, then returns the new list.

Every modification method in the language creates a copy of the input, changes that copy and then returns the new, modified copy.

###### Contains Method

Takes in a list and returns whether

question marks are valid in method names in Elixir.

Convention is that methods with a `?` in the name will return a `true` or `false` value

`member?` takes in a list, and

###### Comprehension Over Lists

Writing some custom code.

List comprehension - for loops in elixir

a comprehension is inherently a map. For every thing that gets passed into the list comprehension, the do block is run. Then the new data structure gets returned

### Pattern Matching

Core concept of Elixir
Elixir's replacement assignment

If the data structure on the LHS, match up perfectly with RHS, the RHS values are accessible using the name stated in the LHS

```elixir
iex(28)> color1 = ["red"]
["red"]
iex(29)> [color1] = ["red"]
["red"]
iex(30)> color1
"red"
iex(31)> [color1, color2] = ["red", "blue"]
["red", "blue"]
iex(32)> color1
"red"
iex(33)> color2
"blue"
iex(34)> [color1, color2, color3] = ["red", "blue"]
```

If a hard coded value is used on the LHS, Elixir _requires_ the matching element on the RHS be the same value

underscore`_` tells Elixir that we don't care about a variable used for pattern matching.

## Running Many Functions back to back - The Pipe Operator

```elixir
def create_hand do
    deck = Cards.create_deck
    deck = Cards.shuffle(deck)
    hand = Cards.deal(deck, hand_size)
  end
```

Pipe Refactor

The result of the last method is automattically passed into the next method

The pipe operator requires that you write consisitent first arguments to work properly

```elixir
  Cards.create_deck
  |> Cards.shuffle
  |> Cards.deal(hand_size)
```

## Writing Documentation

1.  install XDoc
    @moduledoc
    @doc

## Testing

Testing is also a first-class citizen in Elixir

### Doc Testing

If the testing module sees any `## Examples`, it will run the code inside of the docs, testing that all example code results in proper outputs.

### Case Tests

```elixir
  defmodule CardsTest do
  use ExUnit.Case
  doctest Cards

  test "create_deck makes 20 cards" do
    deck_length = length(Cards.create_deck)
    assert deck_length == 52
  end
end
```

#### Case Test Key Words

`assert`
`refute`

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `cards` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:cards, "~> 0.1.0"}
  ]
end
```

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at [https://hexdocs.pm/cards](https://hexdocs.pm/cards).
