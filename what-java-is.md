# What Is Java?

**Scope:** what the language is, what the JVM does, and why Java
still runs so much of the world's software. No code in this
chapter — just the mental model everything else hangs on.

## The one-sentence version

Java is a general-purpose programming language where you write
source code once, compile it to an intermediate form called
*bytecode*, and run that bytecode on the *Java Virtual Machine*
(JVM) — a program that pretends to be a computer, so your code
runs on Windows, macOS, and Linux without recompiling.

## The three pieces

| Piece | What it is | Analogy |
|---|---|---|
| **JDK** (Java Development Kit) | The toolbox: compiler (`javac`), runner (`java`), and libraries | A kitchen with oven, knives, and pantry |
| **JVM** (Java Virtual Machine) | The program that runs your compiled code | The oven — same dish, any kitchen that has one |
| **JRE** (Java Runtime Environment) | JVM plus the standard libraries, no compiler | A rented kitchen: you can cook, not renovate |

You install the **JDK** to write Java. The JDK includes
everything else. If someone says "install Java," they mean the
JDK.

## Why bytecode?

Most languages pick one of two strategies:

- **Compile to machine code** (C, Go, Rust): fast, but you build
  a separate binary for every operating system and CPU.
- **Interpret the source** (Python, Ruby): portable, but the
  interpreter re-reads your source every run.

Java splits the difference. `javac` compiles your `.java`
files once, into `.class` files holding bytecode — compact
instructions for a *virtual* machine. Any real machine with a
JVM can run those `.class` files. "Write once, run anywhere"
was the 1990s slogan; the honest version is "compile once, run
anywhere there's a JVM" — and there's a JVM just about
everywhere.

## Why Java is still everywhere

- **Enterprise software.** Banks, airlines, and retailers run
  Java services written decades ago. That code isn't going
  anywhere, and neither is the language.
- **Android.** Android apps were Java (now Kotlin, which runs
  on the JVM too) for over a decade.
- **Big data.** Hadoop, Spark, Kafka, and Elasticsearch are
  Java/JVM systems.
- **The ecosystem.** Thirty years of libraries mean someone
  has already solved your problem — databases, web servers,
  PDF generation, you name it.

## The honest trade-offs

- **Verbose.** Java makes you spell things out. A "hello
  world" needs a class, a method, and a specific incantation
  (next chapter). Modern Java (17+) is less wordy than the
  Java of 2005, but it'll never win a brevity contest.
- **Memory-hungry.** The JVM itself needs a few hundred
  megabytes before your program does anything. Fine on a
  server; noticeable on a tiny microcontroller.
- **Slow to start.** The JVM warms up — it watches your code
  run, then compiles the hot parts to fast machine code. Long
  services love this; one-shot scripts feel the startup cost.
- **The Oracle question.** Java the *language* is open
  (OpenJDK). Oracle's *branded* JDK has licensing terms that
  changed over the years. Most developers sidestep this
  entirely by using free OpenJDK builds like Temurin or their
  Linux distro's package — see [Installing Java](installing-java.md).

## Which Java?

Versions come in two flavors:

- **LTS (Long-Term Support)** every two years: 17, 21, 25.
  These get security patches for years. Boring is good —
  pick an LTS.
- **Feature releases** every six months in between: 22, 23,
  24, 26. New toys, short support life. Fine for
  experimenting, not for anything you must maintain.

As of late 2026, **Java 25 is the current LTS**
(supported to 2030) and **Java 21 is the previous LTS**
(supported to 2028). Any LTS from 17 on covers everything
in this guide. If a tutorial demands a specific version,
21 is the safe conservative pick; 25 is the current one.

## What this guide doesn't cover

Build tools (Maven, Gradle), web frameworks (Spring),
Android development, and the module system — real topics,
each big enough for its own guide. This one gets you
*writing* Java: the language, the object model, and the
standard library pieces you reach for daily.
