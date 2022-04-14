<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

# Functional Thinking

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## What to expect from this talk:

- a re-iteration of functional programming concepts and tools

- explanations on why they are helpfull

- examples in various programming languages (not just Elixir)

- we'll scratch the surface, not going to dive too deep

- particular discussions - feel free to raise any question

- no good explanation about the meetup event avatar in the email notifications :)

- 2 tickets to Techsylvania conference at the end

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Have you ever ... ?

Even if not on purpose, you might have thought your programs in a _functional_ manner if you:

- used functions like `map`, `filter`, `find`
- passed a function as parameter to another function
- returned a function from another function
- wrote `let` or `val` instead of `var`, or `const` instead of `let`
- wrote a pure function (that does not have a side effect)
  ...

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

> "Learning Haskell is much like learning to program for the first time — it's fun! It forces you to think differently"

(from `Learn You a Haskell for Great Good!` book by Miran Lipovača)

You can replace "Haskell" with "Functional Programming".

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Functional Programming Concepts:

- declarative code

- discipline of immutability

- concurrency (imperative vs functional)

- higher order functions

- pure functions vs. side-effects

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Declarative code vs. Imperative code

- worry about the _what_ and let the compiler and runtime worry about the _how_

- explicitness - code should be as **obvious** as possible

- **side effects** are to be isolated to avoid surprises

- exceptions should be avoided

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

**Imperative code (HOW)**

- you give the computer a set of instructions to follow and the computer does what you want in a sequence

Example:

A rule in your app says new passwords must be at least 9 characters long. There's a list of new passwords and we validate them using this rule.

`javascript`

```javascript
const passwords = [
  "123456",
  "password",
  "admin",
  "freecodecamp",
  "mypassword123",
];

let longPasswords = [];
for (let i = 0; i < passwords.length; i++) {
  const password = passwords[i];
  if (password.length >= 9) {
    longPasswords.push(password);
  }
}

console.log(longPasswords); // logs ["freecodecamp", "mypassword123"];
```

1. We create an empty list called longPasswords.
2. Then we write a loop that will run as many times as there are passwords in the original passwords list.
3. Then we get the password at the index of the loop iteration we are presently on.
4. Then we check if that password is greater than or equal to 9 characters long.
5. If it is, we put it into the longPasswords list.

The same as the compiler we can reason about _how_ this program executes.
Although not very natural, this is not too _hard_ at this level, but as complexity grows it gets _harder_

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

**Declarative code (WHAT)**

- a process of constantly defining _what_
- more readable code that reflects what exactly we want to achieve
- combined with good names it can be very powerfull
- achieves the same goal

`javascript`

```javascript
const isAtLeast9CharsLong = (password) => password.length >= 9;

const longPasswords = passwords.filter(isAtLeast9CharsLong);

console.log(longPasswords); // logs ["freecodecamp", "mypassword123"];
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Immutability

> If you say that `a` is 5, you can't say it's something else later because you just said it was 5. What are you, some kind of liar?

(`Learn You a Haskell for Great Good!` book by Miran Lipovača)

- use _values_ not _variables_ as they don't change
- once a **thing** is created, it is that thing **forever**
- create a new thing instead of changing

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

In pure FP there are no _variables_, everything is a _value_.

`javascript`

```
const a = 42;
```

`kotlin`

```
val a = 42
```

`elixir`

```elixir
life = 42
```

etc...

- in functional programming languages everything is immutable by default
- personal rule: if I need to use a mutable variable I have to take a step back and rethink it

Example - same as declarative vs imperative

All modern languages have built in support for this:

`kotlin`

```kotlin
class Car(var name: String?)

val car = Car("BMW")
car.name = "Audi"
```

- this is not immutable; it can be modified after creation
- let's make it immutable

`kotlin`

```kotlin
class Car(val name: String)

val car = Car("BMW")
```

- you cannot change the name of a `Car` once it's created, you have to create a new `Car`

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Why is immutability important?

- avoids side effects: if it can't change, you don't worry about its state
- makes code more predictable and reliable
- easier to reason about
- multi-threaded programs are safer

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Concurrency

**Mutable class**

`kotlin`

```kotlin
class Car(var name: String?)
```

![concurency diagram](https://raw.githubusercontent.com/mveres/FunctionalThinking/main/assets/fp_concurrency_1.png)

- classic race condition read-modify write
- OOP solution: locks and mutexes - hard to use and analyse => deadocks 💀

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

**Immutable class**

`kotlin`

```kotlin
class Car(val name: String)
```

![concurrency diagram](https://raw.githubusercontent.com/mveres/FunctionalThinking/main/assets/fp_concurrency_2.png)

- T1 can compute without worry since T2 has another copy of `Car`
- no locks necessary
- immutability ensures that shared data is thread-safe
- _things_ that _should_ not be modified _cannot_ be modified\.

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Global State & Real World

- modifiable shared state must exists in realworld app
- in FP we use state isolation and pushing side effects to the edges of our system (DB, filesystem, etc.)

### Q: can (web) frontend code be functional (i.e. immutable and pure)?

YES and NO

YES:

- each update is a transformation that based on the input renders a new version of HTML that is passed to the frontend engine
- e.g.:
  - React that renders new output base on `props` and `state` changes
  - HTML custom elements that render new output based on `props` (`attributes`) changes (simple HTML custom elements, Lit HTML, Vue...)
  - functional programming languages for the frontend: ELM

NO:

- JS functions that change (mutate) HTML elements to render new states

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Immutability Downside - No free cake

- many immutable objects may fill up memory and overload the garbage collector
- this is solved by specialized data structures that provide immutability but are also optimized: ** Persistent Data Structures **

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Persistent Data Structures

- always preserves the previous version of itself when modified
- are immutable; operations do not update the structure, but yield a new updated version

Examples:

- for Android there's [PCollections](https://github.com/hrldcpr/pcollections) - inspired on closure
- for Javascript https://immutable-js.com/
- for Elixir most data structures are built in

`Java`

```Java
ConsPStack<String> list = ConsPStack.empty();
System.out.println(list);  // []

ConsPStack<String> list2 = list.plus("hello");
System.out.println(list);  // []
System.out.println(list2); // [hello]

ConsPStack<String> list3 = list2.plus("hi");
System.out.println(list);  // []
System.out.println(list2); // [hello]
System.out.println(list3); // [hi, hello]

ConsPStack<String> list4 = list3.minus("hello");
System.out.println(list);  // []
System.out.println(list2); // [hello]
System.out.println(list3); // [hi, hello]
System.out.println(list4); // [hi]
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Functions

### Pure Functions

- it is pure if it depends only on the input and has no _side-effects_
- a transformation rather than a mutation
- closer to the mathematical definition of a function

`typescript`

```typescript
function addImpure(x: number): number {
  const y = readNumFromFile();
  return x + y;
}
// depends on the state of the world outside the function

function addPure(x: number, y: number): number {
  return x + y;
}
// depends solely on the input
```

- if a function is called twice with the same parameters, it returns the same result === **referential transparency**

- it allows the compiler to reason about the program's behavior
- it allows you to prove that a function is correct (tests, tests, tests)
- build more complex functions by gluing simple functions together

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Testing in functional programming

- is a pure function easier to write tests for?
- no (fewer) mocks and stubs
- no (fewer) dependency injection

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### First Class Citizens

- a function is just a value, not treated differently from any other data
- Most programming languages -> functions and data are regarded as different things
- Functional programming languages -> functions are treated like any other data

Functions can:

- take other functions as parameters
- create and return new functions

☝️ These are called Higher Order Functions.
Ex: map, filter, reduce

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Side Effects

`kotlin`

```kotlin
fun add(x: Int, y: Int): Int {
  val result = x + y
  writeResultToFile(result)
  return result
}
```

- it is modifying the state of the outside world (by writing to a file)
- it needs a mock and dependecy injection for testing

`side effect === !pure`

- Functions with side effects depend on _historical context_ - they **harder** to reason about

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

Side effects examples:

- mutate a variable scoped outside of the function
- write to a file
- write to a DB
- delete something
- send data through the network
- UI

Can we get rid of these? Should our programs not use databases, filesystems, network, screens, etc. ?

NO: our apps don't have any utility without these
INSTEAD: isolate them.
FP is about containing the side effects - pushing them at the edges of our systems so that the rest of the code remains pure and easy to reason about.

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

- pure functions can be called in any order, on different CPU cores (_concurrency!_)

- compilers in advanced pure functional languages (like Haskell)
  - can tell by formally analyzing your code whether it’s concurrent or not
  - can stop you from shooting yourself in the foot with deadlocks, race conditions and the like

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Higher Order Functions

- functions that can take functions as parameters and return functions as results

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

#### Examples

A piece of code that compresses files using ZIP or RAR format
In traditional Java -> Strategy Pattern.

`java`

```java
public interface CompressionStrategy {
    void compress(List<File> files);
}

public class ZipCompressionStrategy implements CompressionStrategy {
    @Override public void compress(List<File> files) {
        // Do ZIP stuff
    }
}

public class RarCompressionStrategy implements CompressionStrategy {
    @Override public void compress(List<File> files) {
        // Do RAR stuff
    }
}

public CompressionStrategy decideStrategy(Strategy strategy) {
    switch (strategy) {
        case ZIP:
            return new ZipCompressionStrategy();
        case RAR:
            return new RarCompressionStrategy();
    }
}
```

- a lot of code and ceremony

With HoF:

`typescript`

```typescript
// also, simpler form of dependency injection
function compress(files: File[], applyStrategy: (l: File[]) => CompressedFiles){
  applyStrategy(files)
}

compress(fileList, {files -> // ZIP it})
compress(fileList, {files -> // RAR it})
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Currying

- after Haskell Curry - mathematician with important influence on functional programming
- ... partial function application
- ... a mathematical function can only have one parameter -> a function with multiple parameters is rewritten as a series of new functions, each with only one parameter

> "Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument." - _a definition from the internet_

`haskell`

```haskell
multThreeNums :: (Num a) => a -> a -> a -> a
multThreeNums x y z = x * y * z

let multTwoNumsWithNine = multThreeNums 9
multTwoNumsWithNine 2 3
-- 54
let multWithEighteen = multTwoNumsWithNine 2
multWithEighteen 10
-- 180
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

`javascript`

```javascript
const sumNotCurried = (a, b) => a + b;
const sumCurried = (a) => (b) => a + b;

const s1 = sumNotCurried(1, 2);
const s2 = sumCurried(1)(2);

const add1ToEach = (numbers) => numbers.map((e) => sumNotCurried(e, 1));

const add2ToEach = (numbers) => numbers.map(sumCurried(2));

const addNToEach = (n) => (numbers) => numbers.map(sumCurried(n));
addNToEach(n)(numbers);

const add2ToEach = addNToEach(2);
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

`F#`

```F#
let sum a b = a + b

let add1 = sum 1

let add1ToEach ns = ns |> List.map add1

let add1ToEach ns = ns |> List.map (sum 1)

let add1ToEach = List.map (sum 1)

```

`Elixir`

- functions can have the same name with different arities => creating Haskell-style “compile time notational currying” is not possible
- the first argument position is targeted - this effectively puts the first argument position in the role that is typically filled by the last argument position in other (curried) FP languages

`elixir`

```elixir
Enum.map([1, 2, 3], fn x -> x * 2 end)
[1, 2, 3] |> Enum.map(fn x -> x * 2 end)
-- first param is injected
```

VS.

`F#`

```F#
List.map (fun x -> x + 1) [1; 2; 3]
[1; 2; 3] |> List.map (fun x -> x + 1)
# last parameter is injected
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

# Tools of FP

## Chaining and Pipes

`|>` - pipe forward operator
Passes the result of the left side to the function on the right side (forward pipe operator).

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

`Elixir`

```elixir
foo(bar(baz(new_function(other_function()))))

other_function() |> new_function() |> baz() |> bar() |> foo()

"Elixir rocks" |> String.upcase() |> String.split()
# ["ELIXIR", "ROCKS"]
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

`F#`

```F#
[1..10]
|> List.map square
|> List.filter ((>) 50)
|> List.sum
|> (printf "%A")
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

- JavaScript doesn't have it... but [Lodash.chain](https://lodash.com/docs/4.17.15#chain) can offer a similar but more limited behavior

`javacript`

```javascript
import _ from "lodash";

const users = [
  { user: "barney", age: 36 },
  { user: "fred", age: 40 },
  { user: "pebbles", age: 1 },
];

const youngest = _.chain(users)
  .sortBy("age")
  .map((o) => `${o.user} is ${o.age}`)
  .head()
  .value();
// => 'pebbles is 1'
```

`<|` - pipe backward operator - the less used brother

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Pattern matching / Destructuring

- it is a mechanism for checking a value against a pattern
- a successful match can also deconstruct a value into its constituent parts
- it is a more powerful version of the `switch` statement from imperative programming

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

`kotlin`

```kotlin
val (name, age) = person
```

`elixir`

```elixir
{a, b, c} = {:hello, "world", 42}
```

`F#`

```F#
let rec somethingWithAList l =
    match l with
    | [] -> "it is empty"
    | [42] -> "the answer to everything!!!"
    | [_; 42; _] -> "the answer is in the middle"
    | h :: t -> "the answer is out there" + somethingWithAList t
```

`Scala`

```scala
// Case classes are especially useful for pattern matching.

abstract class Notification

case class Email(sender: String, title: String, body: String) extends Notification

case class SMS(caller: String, message: String) extends Notification

case class VoiceRecording(contactName: String, link: String) extends Notification


//Notification is an abstract super class which has three concrete Notification types implemented with case classes Email, SMS, and VoiceRecording. Now we can do pattern matching on these case classes:

def showNotification(notification: Notification): String = {
  notification match {
    case Email(sender, title, _) =>
      s"You got an email from $sender with title: $title"
    case SMS(number, message) =>
      s"You got an SMS from $number! Message: $message"
    case VoiceRecording(name, link) =>
      s"You received a Voice Recording from $name! Click the link to hear it: $link"
  }
}
val someSms = SMS("12345", "Are you there?")
val someVoiceRecording = VoiceRecording("Tom", "voicerecording.org/id/123")

println(showNotification(someSms))  // prints You got an SMS from 12345! Message: Are you there?

println(showNotification(someVoiceRecording))  // prints You received a Voice Recording from Tom! Click the link to hear it: voicerecording.org/id/123
```

- destructuring in javascript

```javascript
const { id, name, ...everything } = person;
const [first, second, rest] = persons;
```

- hidden in `try-catch` statements in C#, Java, ...

```
try {
  throw new InterestingException();
}
catch (VeryInterestingException viex) {
  doSomethingWithIt(viex);
}
catch (InterestingException iex) {
  doSomethingElseWithIt(iex);
}
catch (Exception ex) {
  dealWithIt(ex);
}
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## (Discriminated) Union types

- a discriminated union is a pattern that indicates to the compiler all of the possible types that a newly created type can represent
- a.k.a. algebraic data types

`F#`

```f#
type Shape =
    | Rectangle of width : float * length : float
    | Circle of radius : float
    | Prism of width : float * float * height : float

type Tree =
    | Empty
    | Leaf of int
    | Node of Tree * Tree

match t with
| Empty -> "there's nothing here"
| Leaf (value) -> "there's ${value} in the leaf"
| _ -> "not sure what to do with this"

type Optional<T> = None | Some of T
```

`Java`

```java
String strNull = null;
Optional nullableOptional = Optional.ofNullable( strNull );
Optional sizeOptional = stringOptional.map( String::length );

```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

Tagged tuples in Elixir

```elixir
@type animal :: {:cat, number(), integer()}
  | {:dog, number(), integer()}
  | {:monkey, number(), integer(), integer()}
  | ...

# then the type can be used in case statements like:

case some_animal do
  {:cat, weight, _} -> # do something with weight

  _ ->
    # do something if some_animal isn't the kind we care about
end
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Recursion & Tail-Recursion

- recursion + immutability = the FP alternative for loops + variables
- possible issue: Stack Overflow
- tail recursive patterns: accumulator, continuation
- tail call optimization (ES6 javascript has it)

```javascript
const isEven = (x) => x % 2 === 0;

const filter = (xs, isOk) => {
  if (!xs.length) return [];
  const [head, ...tail] = xs;

  const newHead = isOk(head) ? [head] : [];
  const newTail = filter(tail, isOk);
  return [...newHead, ...newTail];
};

console.log(filter([1, 3, 6, 8], isEven));

const tailRecursiveFilter = (xs, isOk, acc = []) => {
  if (!xs.length) return acc;
  const [head, ...tail] = xs;

  const newAcc = isOk(head) ? [...acc, head] : acc;
  return filter(tail, isOk, newAcc);
};

console.log(tailRecursiveFilter([1, 3, 6, 8], isEven));
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Sources & Further Learning

- "Programing F#" by Chris Smith
- Functional Programming Principles in Scala by Martin Odersky (https://www.coursera.org/learn/progfun1)
- Introduction to Functional Programming by Erik Meijer (https://www.edx.org/course/introduction-functional-programming-delftx-fp101x-0)
- https://fsharpforfunandprofit.com/
- "Learn You a Haskell for Great Good!" book by Miran Lipovača
- https://www.youtube.com/watch?v=iZLP4qOwY8I

- https://fsharpforfunandprofit.com/
- https://www.freecodecamp.org/news/imperative-vs-declarative-programming-difference/
- https://www.freecodecamp.org/news/functional-programming-for-android-developers-part-1-a58d40d6e742
- https://medium.com/free-code-camp/functional-programming-for-android-developers-part-2-5c0834669d1a
- https://medium.com/free-code-camp/functional-programming-for-android-developers-part-3-f9e521e96788
- https://www.freecodecamp.org/news/functional-programming-in-javascript/
- https://www.freecodecamp.org/news/functional-programming-in-javascript-explained-in-plain-english/

- great FP walkthrough for SWIFT programmers: https://www.raywenderlich.com/9222-an-introduction-to-functional-programming-in-swift#

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## The ~million dollar~ Techsylvania tickets question!

(find the chat and write your answer there)

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### What is the result of the following Elixir computation?

```elixir
"Cr4ft1ng!"
|> String.split("")
|> Enum.filter(fn e -> Regex.match?(~r/\d/, e) end) # is digit?
|> Enum.map(&String.to_integer/1)
|> Enum.map(fn e -> if rem(e, 2) == 1, do: e * 2, else: e end)
|> Enum.join("")
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

What is the meaning of life the universe and everything?

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
