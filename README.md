# Java for Mere Mortals

**Java** is the language behind banks, Android apps, and
half the servers on earth: write once, compile to
bytecode, run on the Java Virtual Machine anywhere. This
guide covers the language itself — installing a JDK, your
first program, types, methods, classes and objects,
interfaces, exceptions, and the collections you'll use
daily.

No CS degree assumed. If you've written any program in
any language, you're ready.

## What this guide covers

- [**What Java is**](what-java-is.md) — the JVM, bytecode,
  why Java is still everywhere, and which version to pick
- [**Installing Java**](installing-java.md) — a JDK on
  Linux, macOS, or Windows, plus `jshell` for experiments
- [**Your first program**](first-program.md) — one file,
  compiled and run two ways, every line explained
- [**Variables and types**](variables-and-types.md) —
  primitives, strings, `var`, `final`, and integer
  division's classic trap
- [**Control flow**](control-flow.md) — `if`, modern
  `switch`, the three loops, `break`/`continue`
- [**Methods**](methods.md) — defining, calling, return
  values, overloading, `static`
- [**Classes and objects**](classes-and-objects.md) —
  fields, constructors, `new`, and encapsulation
- [**Interfaces and inheritance**](interfaces-and-inheritance.md) —
  `extends`, `implements`, abstract classes
- [**Exceptions**](exceptions.md) — `try`/`catch`, checked
  vs unchecked, try-with-resources, reading stack traces
- [**Collections**](collections.md) — `List`, `Map`,
  generics, and autoboxing
- [**Troubleshooting**](troubleshooting.md) — symptom →
  fix, nine ways

## What it doesn't cover

Build tools (Maven, Gradle), web frameworks (Spring),
Android development, and the module system. This guide
gets you *writing* Java — the advanced topography comes
later.

## How to use this guide

Code samples were compiled and run with OpenJDK 21;
everything here works on any LTS from 17 up. Commands
are meant to be run — **Check:** blocks show what success
looks like. Version-sensitive facts (like which LTS is
current) were verified in October 2026 and link their
sources; treat them as "check again in a year."

## Validation notes

- Every Java sample in these chapters was compiled and
  executed with OpenJDK 21.0.12; outputs shown are the
  actual outputs.
- `apt` package names (`openjdk-21-jdk`,
  `openjdk-25-jdk`) were checked against Debian
  documentation current as of October 2026.
- Homebrew cask and Windows installer steps follow the
  vendors' own instructions and were not run here.
