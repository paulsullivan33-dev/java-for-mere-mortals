# Your First Program

**Scope:** one file, compiled and run two ways, with every
line explained. All samples below were compiled and run
with OpenJDK 21.

## The file

Create `Hello.java`:

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

Three rules hiding in five lines:

- **The file name must match the class name.** `public class
  Hello` lives in `Hello.java` — capital H, both. Get this
  wrong and the compiler refuses (see
  [Troubleshooting](troubleshooting.md)).
- **`main` is where the program starts.** The exact
  incantation `public static void main(String[] args)` is
  non-negotiable; you'll memorize it by the third program.
  `String[] args` holds command-line arguments — ignore it
  for now.
- **`System.out.println`** prints a line. `System.out` is
  "the screen," `println` is "print line." Java names are
  long but literal.

## Compile, then run

```sh
javac Hello.java
java Hello
```

**Check:** the first command silently creates `Hello.class`
(bytecode — see [What Is Java?](what-java-is.md)); the
second prints:

```
Hello, world!
```

Note: you run `java Hello`, not `java Hello.class` and not
`java Hello.java`. The runner wants the *class name*.

## The shortcut: run the source directly

Since Java 11 you can skip the separate compile step for
single-file programs:

```sh
java Hello.java
```

**Check:** prints `Hello, world!` with no `.class` file
created. Handy for experiments; real projects still
compile explicitly.

## Reading error messages

Break it on purpose — delete the semicolon and compile:

```sh
javac Hello.java
```

```
Hello.java:3: error: ';' expected
        System.out.println("Hello, world!")
                                             ^
1 error
```

Java errors give you **file, line, and a caret** pointing
at the problem. Read the first error only; later ones are
often echoes of the first. Fix, recompile, move on.

## Try it in jshell

```sh
jshell
```

```
jshell> System.out.println("Hello, jshell!")
Hello, jshell!
```

No class, no `main`, no file — jshell wraps snippets for
you. Use it to test one-liners from the coming chapters.

## What's next

A program that just prints is a parlor trick. Next:
[Variables and Types](variables-and-types.md) — storing
values and doing arithmetic with them.
