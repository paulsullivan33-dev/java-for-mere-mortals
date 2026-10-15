# Glossary

Terms as this guide uses them. Jargon is explained on
first use in each chapter; this page collects the
definitions in one place.

- **Abstract class** — a class that can't be instantiated,
  meant to be extended; may contain both abstract methods
  and shared code.
- **Autoboxing** — automatic conversion between primitives
  (`int`) and their wrapper objects (`Integer`).
- **Bytecode** — the intermediate instructions `javac`
  produces (`.class` files); run by the JVM, not directly
  by your CPU.
- **Checked exception** — an exception the compiler forces
  you to catch or declare (`IOException`).
- **Class** — a blueprint defining fields and methods;
  objects are built from it.
- **Constructor** — a special method (same name as the
  class, no return type) that runs when an object is
  created with `new`.
- **Diamond (`<>`)** — shorthand letting the compiler infer
  generic type arguments: `new ArrayList<>()`.
- **Encapsulation** — hiding an object's internals behind
  `private` fields and public methods.
- **Field** — a variable belonging to a class or object.
- **Final** — "assign once": a `final` variable can't be
  reassigned after initialization.
- **Generics** — type parameters in angle brackets
  (`List<String>`) letting collections enforce element
  types at compile time.
- **Getter / setter** — methods (`getName`/`setName`) that
  read or write a private field, often with validation.
- **Immutable** — unchangeable after creation (`String`;
  methods like `toUpperCase()` return new objects).
- **Instance** — one object built from a class; instance
  methods/fields belong to each object separately.
- **Interface** — a contract of method signatures a class
  promises to implement; enables programming to abilities
  rather than concrete types.
- **JAR** — Java ARchive: a zip of compiled classes and
  resources, Java's unit of distribution.
- **JDK** — Java Development Kit: compiler, runner,
  libraries. What you install to write Java.
- **JRE** — Java Runtime Environment: JVM plus libraries,
  no compiler. For running, not writing.
- **jshell** — the JDK's interactive snippet runner
  (Java 9+).
- **JVM** — Java Virtual Machine: the program that runs
  bytecode on any platform.
- **LTS** — Long-Term Support release (17, 21, 25):
  years of security patches; the boring, correct choice.
- **Method** — a named block of logic inside a class;
  called on an object, or `static` on the class itself.
- **Null** — "points at nothing": the value of an
  unassigned reference. Calling methods on it throws
  `NullPointerException`.
- **Object** — an instance of a class: state (fields)
  plus behavior (methods).
- **Overloading** — defining several methods with the
  same name but different parameters; Java picks by the
  argument list.
- **Override** — replacing an inherited method in a
  subclass; mark with `@Override`.
- **Package** — a namespace grouping related classes
  (`java.util`); also the unit of distribution.
- **Primitive** — one of Java's eight built-in value
  types (`int`, `double`, `boolean`, …); not objects.
- **Reference** — a variable pointing at an object (as
  opposed to holding the object itself).
- **Stack trace** — the exception report listing the
  failure and the chain of method calls that led there.
- **Static** — belonging to the class rather than any
  object; callable without `new`.
- **Unchecked exception** — an exception needing no
  declaration (`NullPointerException`,
  `IllegalArgumentException`); signals a bug.
- **var** — "infer the type from the value" (Java 10+);
  the variable still has a static type.
- **Wrapper class** — object version of a primitive
  (`Integer` for `int`) so primitives can live in
  collections.
