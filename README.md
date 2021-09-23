<br /><br /><br /><br /><br />

# Functional Thinking

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

> "Learning ~Haskell~ Functional Programming is much like learning to program for the first time — it's fun! It forces you to think differently"

(adapted quote from `Learn You a Haskell for Great Good!` book by Miran Lipovača)

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## What is functional programming

- an umbrella for a range of programming concepts

- a style of programming that treats programs as evaluation of mathematical functions and avoids _mutable state_ and side effects

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Concepts

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

- Declarative code

  - worry about the _what_ and let the compiler and runtime worry about the _how_
  - Explicitness

  - code should be as **obvious** as possible
  - **side effects** are to be isolated to avoid surprises
  - Exceptions should be avoided

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

- Concurrency

  - functional code is concurrent by default because of purity (no side-effects)
  - CPU cores aren’t getting faster but multiply: concurrency to take advantage of multi-core architectures

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

- Higher Order Functions

  - functions are first class citizens
  - pass functions around just like you would a string or an int (filter, map, reduce)

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

- Immutability

  - variables don't change (they are values)
  - Once a **thing** is created, it is that thing **forever**
  - create a new thing instead of changing
  - this avoids side effects: if it can't change, you don't worry about its state

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Declarative code vs. Imperative code

- worry about the _what_ and let the compiler and runtime worry about the _how_

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

The same as the compiler we can reason about _how_ this program executes. This is not too hard at this level, but as complexity grows...

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

**Declarative code (WHAT)**

- a process of constantly defining _what_
- more readable code that reflects what exactly we want
- combined with good names it can be very powerfull
- achieves the same goal

`javascript`

```javascript
const isAtLeast9CharsLong = (password) => password.length >= 9;

const longPasswords = passwords.filter(isAtLeast9CharsLong);

console.log(longPasswords); // logs ["freecodecamp", "mypassword123"];
```

![Declarative vs Imperative](https://github.com/mveres/FunctionalThinking2021/blob/a932489e1c1f03b9dba3f08feeb0e5cd6202f8dc/assets/functiona_vs_imperative.png?raw=true)

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Immutability

> If you say that `a` is 5, you can't say it's something else later because you just said it was 5. What are you, some kind of liar?

(`Learn You a Haskell for Great Good!` book by Miran Lipovača)

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

In FP there are no _variables_, everything is a _value_.

javascript
`const a = 42;`

kotlin
`val a = 42`

etc...

- in functional programming languages everything is immutable by default
- if I need to use a mutable variable I have to rethink the algorithm

Example - same as declarative vs imperative

- variables don't change (they are values)
- once a **thing** is created, it is that thing **forever**
- create a new thing instead of changing

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
- this makes your code predictable and reliable

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Concurency

**Mutable class**

`kotlin`

```kotlin
class Car(var name: String?)
```

![concurency diagram](https://github.com/mveres/FunctionalThinking2021/blob/a932489e1c1f03b9dba3f08feeb0e5cd6202f8dc/assets/fp_concurency_1.png?raw=true)

- classic race condition read-modify write
- OOP solution: locks and mutexes - hard to use and analyse => deadocks 💀

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

**Immutable class**

`kotlin`

```kotlin
class Car(val name: String)
```

![concurrency diagram](https://github.com/mveres/FunctionalThinking2021/blob/a932489e1c1f03b9dba3f08feeb0e5cd6202f8dc/assets/fp_concurrency_2.png?raw=true)

- T1 can compute without worry since T2 has another copy of `Car`
- no locks necessary
- immutability ensures that shared data is thread-safe
- _things_ that _should_ not be modified _cannot_ be modified\.

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Global State & Real World

- modifiable shared state must exists in realworld app
- in FP we use state isolation and pushing side effects to the edges of our system (DB, filesystem, etc.)\.

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Immutability Downside

- many immutable objects may fill up memory and overload the garbage collector
- this is solved by specialized data structures that provide immutability but are also optimized: ** Persistent Data Structures **

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Persistent Data Structures

- always preserves the previous version of itself when modified
- are immutable; operations do not update the structure, but yield a new updated version

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

![persistent data structures diagram](https://i.stack.imgur.com/ywLvk.png)

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

Example:

- for Android there's [PCollections](https://github.com/hrldcpr/pcollections)
- inspired on closure
- for Javascript https://immutable-js.com/

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
- closer to the mathematical definition of a function

`kotlin`

```kotlin
fun addImpure(x: Int): Int {    val y: Int = readNumFromFile()    return x + y}


fun addPure(x: Int, y: Int): Int {    return x + y}
```

- if a function is called twice with the same parameters, it returns the same result === **referential transparency**

- it allows the compiler to reason about the program's behavior
- it allows you to prove that a function is correct
- build more complex functions by gluing simple functions together

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### First Class Citizens

- a function is just a value, not treated differently from any other data
- Most programming languages -> functions and data are regarded as different things
- Functional programming languages -> functions are treated like any other data

Functions can:

- take other functions as parameters
- create and return new functions

☝️ These are called Higher Order functions.
Ex: map, filter, reduce

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Side Effects

`kotlin`

```kotlin
fun add(x: Int, y: Int): Int { val result = x + y    writeResultToFile(result)    return result}
```

- it is modifying the state of the outside world (by writing to a file)

`side effect === !pure`

Side effects examples:

Give some examples

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

- mutate a variable scoped outside of the function
- write to a file
- write to a DB
- delete something
- send data through the network
- ....

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

- Functions with side effects depend on _historical context_ - they **harder** to reason about

Should our programs not use databases, filesystems, network, screens, etc. ?
...

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

- FP is about containing the side effects - pushing them at the edges of our systems so that the rest of the code remains pure and easy to reason about.

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

`kotlin`

```kotlin
fun compress(files: List<File>, applyStrategy: (List<File>) -> CompressedFiles){
    applyStrategy(files)
}

compress(fileList, {files -> // ZIP it})
compress(fileList, {files -> // RAR it})
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

_Sum_ the _doubles_ of all the _odds_ from an array.

`javascript`

```javascript
let sum = 0;

for (int i = 0; i < numbers.length; i++) {
  if (numbers[i] % 2 === 1) {
    sum = sum + 2 * numbers[i];
  }
}

numbers
  .filter(n => n % 2 === 1)
  .map(n => n * 2)
  .reduce((sum, n) => sum + n);


// it gets better with good naming

const isOdd = n => n % 2 === 1;
const double = n => n * 2;
const sum = (a, b) => a + b;


let s = 0;
for (int i = 0; i < numbers.length; i++) {
  if (isOdd(numbers[i])) {
    s = sum(s, double(numbers[i]));
  }
}

numbers
  .filter(isOdd)
  .map(double)
  .reduce(sum)
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Closures

- a value that is captured by the scope of a function - it closes over the value
- valuable if functions need to be aware of the surrounding environment
- you get encapsulation and other OOP like behaviors

`javascript`

```javascript
const i = 7;
const multiply = (n) => n * i;
```

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Currying

- after Haskell Curry - mathematician with important influence on functional programming
- ... partial function application
- ... a mathematical function can only have one parameter -> a function with multiple parameters is rewritten as a series of new functions, each with only one parameter

> "Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument." - _a definition from the internet_

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

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

# Tools of FP

## Chaining and Pipes

![Chain all the things](https://i.ibb.co/vZ1dP4m/Screenshot-2021-07-29-at-17-23-12.png)

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

- JavaScript doesn't have it... but [Lodash.chain](https://lodash.com/docs/4.17.15#chain)

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

- Kotlin and Swift don't have it but they are language proposals

`<|` - pipe backward operator - the less used brother

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Pattern matching / Destructuring

- it is a mechanism for checking a value against a pattern
- a successful match can also deconstruct a value into its constituent parts
- it is a more powerful version of the `switch` statement

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
- tail call optimization - javascript has it (ES6)

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

## Sources & Further Reading

- https://www.freecodecamp.org/news/imperative-vs-declarative-programming-difference/
- https://www.freecodecamp.org/news/functional-programming-for-android-developers-part-1-a58d40d6e742
- https://medium.com/free-code-camp/functional-programming-for-android-developers-part-2-5c0834669d1a
- https://medium.com/free-code-camp/functional-programming-for-android-developers-part-3-f9e521e96788
- https://www.freecodecamp.org/news/functional-programming-in-javascript/
- https://www.freecodecamp.org/news/functional-programming-in-javascript-explained-in-plain-english/

- "Programing F#" by Chris Smith
- Functional Programming Principles in Scala by Martin Odersky (https://www.coursera.org/learn/progfun1)
- Introduction to Functional Programming by Erik Meijer (https://www.edx.org/course/introduction-functional-programming-delftx-fp101x-0)
- https://fsharpforfunandprofit.com/
- "Learn You a Haskell for Great Good!" book by Miran Lipovača
- https://www.youtube.com/watch?v=iZLP4qOwY8I

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

# Exercise

The following market data chunk was received from the provider:

```
currencyPair price   changeAbsolute changePercent
EUR/USD     1.0735         -0.0045     -0.42
USD/JPY   112.0900          -0.494     -0.44
GBP/USD     1.2476         -0.0010     -0.08
AUD/USD     0.7648         -0.0032     -0.42
USD/CAD     1.3112          0.0092      0.71
USD/CHF     0.9927          0.0007      0.07
USD/CNY     6.8599         -0.0050     -0.07
EUR/JPY   120.3150         -1.1050     -0.91
EUR/GBP     0.8604         -0.0032     -0.37
```

1. Parse the string into a collection of objects. Prove that your implementation is correct with unit tests.
   Example type of parsed data:

`TypeScript`

```typescript
type MarketData = {
  currencyPair: string;
  price: number;
  changeAbsolute: number;
  changePercent: number;
}[];
```

NOTE: Do not assume & hardcode the properties but parse them from the header.

2. Retrieve the top 3 currency pairs with the biggest (percentage) changes from the data chunk. Prove that your implementation is correct with unit tests.
