# Exceptions

**Scope:** `try`/`catch`/`finally`, checked vs unchecked
exceptions, and `throw`. All samples were compiled and run
with OpenJDK 21.

## The idea

When something goes wrong — bad input, missing file —
Java *throws* an exception object. If nobody catches it,
the program crashes with a stack trace. Catching one is
saying "I know this can fail, and here's plan B":

```java
public class Safe {
    public static void main(String[] args) {
        try {
            int n = Integer.parseInt("abc");
            System.out.println(n);
        } catch (NumberFormatException e) {
            System.out.println("Not a number: " + e.getMessage());
        }
        System.out.println("Still running");
    }
}
```

**Check:** prints

```
Not a number: For input string: "abc"
Still running
```

`Integer.parseInt("abc")` throws; the `catch` block runs
instead of the crash; the program continues. The
`NumberFormatException` message (`For input string:
"abc"`) comes from the JDK — exact wording varies by
version, so match on the shape, not the text.

## Try / catch / finally

```java
try {
    riskyWork();
} catch (IOException e) {
    System.out.println("I/O failed: " + e.getMessage());
} catch (Exception e) {
    System.out.println("Something else: " + e.getMessage());
} finally {
    System.out.println("Always runs");
}
```

- Multiple `catch` blocks: most specific first.
- `finally` runs whether or not anything threw — for
  cleanup like closing files. (Modern code usually uses
  try-with-resources instead; see below.)

## Checked vs unchecked

Java's famous split:

| | Checked | Unchecked |
|---|---|---|
| Examples | `IOException`, `SQLException` | `NullPointerException`, `IllegalArgumentException` |
| Rule | Must be caught or declared | No compiler enforcement |
| Meaning | "This can fail; deal with it" | "This is a bug; fix your code" |

A method that can throw a checked exception must say so:

```java
static String readFirstLine(String path) throws IOException {
    return Files.readString(Path.of(path)).lines().findFirst().orElse("");
}
```

Callers then choose: catch it, or add `throws IOException`
themselves and push the decision upward. Unchecked
exceptions need no declaration — `throw new
IllegalArgumentException("name required")` just works
(you saw this in [Classes and
Objects](classes-and-objects.md)).

Opinionated advice: catch checked exceptions where you
can actually *do* something (retry, default value, tell
the user). Let unchecked ones crash during development —
a `NullPointerException` is a bug report, not a runtime
condition to paper over.

## Try-with-resources

Files and other closeable things get automatic cleanup:

```java
try (var reader = new BufferedReader(new FileReader("notes.txt"))) {
    System.out.println(reader.readLine());
} catch (IOException e) {
    System.out.println("Couldn't read notes.txt");
}
```

**Check:** with a `notes.txt` present, prints its first
line; without one, prints `Couldn't read notes.txt`.
The `reader` closes itself when the block exits — even
on exception. No `finally` needed.

## Reading a stack trace

Uncaught, an exception prints something like:

```
Exception in thread "main" java.lang.NullPointerException:
  Cannot invoke "String.length()" because "this.s" is null
    at Example.broken(Example.java:5)
```

Read it **top-down**: the exception type and message
first ("tried to call `.length()` on a null `s`"), then
the `at` lines — your code is usually the first line
naming *your* class. Library frames below it are the
call path that got you there.

Next: [Collections](collections.md) — lists, maps, and
the generics that keep them honest.
