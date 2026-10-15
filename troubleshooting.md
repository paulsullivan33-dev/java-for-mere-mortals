# Troubleshooting

**Scope:** the errors every Java beginner hits, each as
symptom → cause → fix. Read the first error the compiler
prints; later ones are often echoes.

## `error: class Hello is public, should be declared in a file named Hello.java`

**Cause:** the file name doesn't match the `public class`
name — including capitalization.

**Fix:** rename the file to `Hello.java` (or the class to
match the file). On case-insensitive filesystems
(Windows, default macOS), `hello.java` vs `Hello.java`
still matters to `javac`.

## `error: cannot find symbol`

```
Hello.java:5: error: cannot find symbol
        System.out.println(mesage);
                           ^
  symbol:   variable mesage
```

**Cause:** a misspelled name — variable, method, or class.

**Fix:** check the spelling against the declaration. If
it's a class from the standard library (`ArrayList`,
`HashMap`), you probably forgot the `import` — see next.

## `error: cannot find symbol` for `ArrayList` / `List` / `Map`

**Cause:** missing import. `java.lang` (`String`,
`System`, `Math`) is automatic; `java.util` is not.

**Fix:** add the imports at the top:

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Map;
```

## `error: main method not found`

```
Error: Main method not found in class Hello, please define
the main method as:
   public static void main(String[] args)
```

**Cause:** the signature is wrong — `Main` instead of
`main`, missing `static`, `String args[]` in the wrong
shape, or the method is inside a non-public class file
mismatch.

**Fix:** copy the incantation exactly:
`public static void main(String[] args)`.

## `NullPointerException`

**Cause:** calling a method (or reading a field) on a
reference that points at nothing — a variable never
assigned, or a `Map.get()` for a missing key.

**Fix:** find where the reference was supposed to be set.
Defensive habits: initialize fields in the constructor,
check `Map` results with `containsKey()`, and validate
method arguments ([Classes and Objects](classes-and-objects.md)).

## `ClassCastException`

```
Exception in thread "main" java.lang.ClassCastException:
  class java.lang.String cannot be cast to class java.lang.Integer
```

**Cause:** treating an object as a type it isn't — almost
always a raw (non-generic) collection handing back
`Object`.

**Fix:** parameterize the collection (`List<String>`,
not `List`) so the compiler catches the mismatch at
`add` time instead of crashing at `get` time. See
[Collections](collections.md).

## `';' expected` / `illegal start of expression`

**Cause:** usually a missing semicolon, brace, or
parenthesis on *this* line or the one above it.

**Fix:** look at the line the caret points to *and the
line before it*. Count braces — every `{` needs its `}`.

## `incompatible types: possible lossy conversion from double to int`

```java
int x = 3.9;   // error
```

**Cause:** assigning a wider type to a narrower one
silently drops data, so Java refuses.

**Fix:** decide what you meant — `double x = 3.9;`, or
`int x = (int) 3.9;` (the cast truncates to `3`).

## Program compiles, prints nothing / wrong output

**Cause:** logic bug, not a compiler bug. Common
suspects: integer division (`7 / 2` is `3`), `==` on
strings (use `.equals()`), off-by-one loop bounds.

**Fix:** print intermediate values. `System.out.println`
is a legitimate debugger — print the variable right
before the suspicious line and check your assumption.
