# Methods

**Scope:** defining methods, parameters, return values,
overloading, and `static`. All samples were compiled and
run with OpenJDK 21.

## Defining and calling

A method is a named chunk of logic. It lives inside a
class:

```java
public class Greeter {
    static String greet(String name) {
        return "Hello, " + name + "!";
    }

    public static void main(String[] args) {
        String message = greet("Ada");
        System.out.println(message);
    }
}
```

**Check:** prints `Hello, Ada!`.

Reading the definition `static String greet(String name)`:

- `String` — what it gives back (the *return type*).
- `greet` — its name.
- `(String name)` — what it takes in (a *parameter*).
- `static` — callable without creating an object. You'll
  meet the non-`static` kind in [Classes and
  Objects](classes-and-objects.md); for now, methods in
  these examples are `static` so `main` can call them
  directly.

## Return values

A method with a return type **must** return a value on
every path, or it won't compile:

```java
static String describe(int n) {
    if (n > 0) {
        return "positive";
    }
    return "zero or negative";  // required!
}
```

`void` means "returns nothing" — like `main` itself:

```java
static void shout(String s) {
    System.out.println(s.toUpperCase());
}
```

## Parameters are copies

Java passes arguments **by value** — the method gets a
copy:

```java
static void tryToChange(int x) {
    x = 99;
}

public static void main(String[] args) {
    int n = 1;
    tryToChange(n);
    System.out.println(n);  // still 1
}
```

**Check:** prints `1`. Reassigning the parameter inside
the method doesn't touch the caller's variable. (Objects
are subtler — a method can mutate an object's *contents*
through the copy of the reference. That's a [Classes and
Objects](classes-and-objects.md) topic.)

## Overloading

Same name, different parameters — Java picks by the
argument list:

```java
static int add(int a, int b) {
    return a + b;
}

static double add(double a, double b) {
    return a + b;
}
```

`add(2, 3)` calls the first, `add(2.5, 3.5)` the second.
Overloading is how the standard library offers one name
(`println`, for instance) for many types.

## A bigger example

```java
public class TempCheck {
    static String describe(int temp) {
        if (temp > 100) {
            return "Boiling";
        } else if (temp > 32) {
            return "Liquid";
        }
        return "Frozen";
    }

    public static void main(String[] args) {
        for (int t : new int[]{212, 85, 10}) {
            System.out.println(t + ": " + describe(t));
        }
    }
}
```

**Check:** prints

```
212: Boiling
85: Liquid
10: Frozen
```

Methods turn repeated logic into a name you can test,
reuse, and read at a glance. Next: [Classes and
Objects](classes-and-objects.md) — Java's real home
turf.
