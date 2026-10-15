# Variables and Types

**Scope:** declaring variables, the primitive types, strings,
`var`, and `final`. All samples were compiled and run with
OpenJDK 21.

## Declaring a variable

```java
int count = 42;
```

Read it as: "an `int` (integer) named `count`, holding 42."
Java needs the type up front — the compiler checks every
use against it.

```java
int count = 42;
count = "hello";   // compile error: incompatible types
```

That strictness is the point: a whole class of bugs becomes
a compile error instead of a 2 AM production incident.

## The primitive types

Eight types are built into the language itself (not
objects — more on that distinction in
[Classes and Objects](classes-and-objects.md)):

| Type | Holds | Example | Size |
|---|---|---|---|
| `int` | Whole numbers | `int n = 42;` | 32-bit |
| `long` | Bigger whole numbers | `long big = 9_000_000_000L;` | 64-bit |
| `double` | Decimals | `double pi = 3.14159;` | 64-bit |
| `boolean` | True/false | `boolean done = false;` | — |
| `char` | One character | `char grade = 'A';` | 16-bit |
| `byte`, `short`, `float` | Smaller/older variants | rarely needed today | — |

In practice you need four: `int`, `long`, `double`,
`boolean`. Notes:

- `long` literals need an `L` suffix: `9_000_000_000L`
  (underscores are just visual separators).
- `char` uses **single** quotes (`'A'`); strings use
  **double** quotes (`"A"`). Mixing them up is a rite of
  passage.
- There is no `float` default: `3.14` is a `double`.

## Strings

`String` is not a primitive — it's an object (capital S
is the tell: class names start uppercase). The essentials:

```java
String name = "Ada";
System.out.println(name.length());        // 3
System.out.println(name.toUpperCase());   // ADA
System.out.println("Hello, " + name);     // Hello, Ada
```

**Check:** prints `3`, `ADA`, `Hello, Ada`.

Two gotchas that bite everyone once:

1. **Strings are immutable.** `toUpperCase()` returns a
   *new* string; `name` still holds `"Ada"`.
2. **Compare with `.equals()`, never `==`.** `==` asks "same
   object in memory?" — `.equals()` asks "same text?":

```java
String a = new String("hi");
System.out.println(a == "hi");       // false (usually!)
System.out.println(a.equals("hi"));  // true
```

**Check:** prints `false` then `true`. Use `.equals()`
for strings, always.

## Letting the compiler infer: `var`

Since Java 10, `var` lets the compiler fill in the type
from the value:

```java
var count = 42;          // int
var name = "Ada";        // String
var pi = 3.14159;        // double
```

`var` is not "no types" — the variable still *has* a
type, you just didn't write it. `var count = 42; count =
"hello";` is still a compile error. Use `var` when the
type is obvious from the right-hand side; write the type
when it aids the reader.

## Constants with `final`

```java
final double TAX_RATE = 0.0825;
TAX_RATE = 0.09;   // compile error: cannot assign a value
                  // to final variable TAX_RATE
```

`final` means "assign once." Convention: constants shout
in `UPPER_SNAKE_CASE`.

## Arithmetic

```java
System.out.println(7 / 2);    // 3, not 3.5!
System.out.println(7.0 / 2);  // 3.5
System.out.println(7 % 2);    // 1 (remainder)
```

**Check:** prints `3`, `3.5`, `1`. Integer division
*truncates* — the classic beginner bug. If you want
decimals, make at least one side a `double`.

## Try it

In `jshell`:

```
jshell> var total = 7 / 2;
jshell> total
$2 ==> 3
```

Then `var precise = 7.0 / 2;` and compare. Next:
[Control Flow](control-flow.md) — making decisions and
repeating work.
