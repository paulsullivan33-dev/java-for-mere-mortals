# Interfaces and Inheritance

**Scope:** `extends`, `implements`, abstract classes, and
what interfaces are actually for. All samples were compiled
and run with OpenJDK 21.

## Inheritance: `extends`

A class can *extend* another, inheriting its fields and
methods:

```java
class Animal {
    String name;

    Animal(String name) {
        this.name = name;
    }

    void speak() {
        System.out.println(name + " makes a sound");
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name);   // calls Animal's constructor — required first
    }

    @Override
    void speak() {
        System.out.println(name + " says woof!");
    }
}
```

`Dog` *is an* `Animal` with a better `speak()`.
`@Override` is a promise to the compiler: "I'm replacing
the parent's method — error if I misspelled it." Always
use it.

## Interfaces: `implements`

An **interface** is a contract: "any class implementing me
provides these methods." No implementation, just promises:

```java
interface Swimmer {
    void swim();   // no body — implementing classes fill it in
}

class Duck extends Animal implements Swimmer {
    Duck(String name) {
        super(name);
    }

    @Override
    public void swim() {
        System.out.println(name + " paddles");
    }
}
```

A class extends **one** parent but can implement **many**
interfaces — that's how Java gets most of multiple
inheritance's benefits without its messes.

## Why interfaces matter

They let code depend on *abilities*, not concrete types:

```java
static void race(Swimmer s) {
    s.swim();
}
```

`race` accepts a `Duck`, a `Fish`, a `Human` — anything
that swims. The [Collections](collections.md) chapter
leans on this: `List` is an interface, `ArrayList` one
implementation of it.

## Abstract classes

Halfway between: a class you can't instantiate, meant to
be extended, which *can* hold shared code:

```java
abstract class Shape {
    abstract double area();   // subclasses must define this

    void describe() {         // but shared code lives here
        System.out.println("Area: " + area());
    }
}

class Circle extends Shape {
    double radius;

    Circle(double radius) {
        this.radius = radius;
    }

    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}
```

Use an abstract class when subclasses share *code*;
an interface when they share only a *contract*.

## Putting it together

```java
public class Zoo {
    public static void main(String[] args) {
        Duck d = new Duck("Daffy");
        d.speak();   // inherited from Animal... but wait
        d.swim();    // from Swimmer
        Circle c = new Circle(2.0);
        c.describe();
    }
}
```

**Check:** prints

```
Daffy makes a sound
Daffy paddles
Area: 12.566370614359172
```

(`Duck` didn't override `speak()`, so `Animal`'s version
runs — inheritance in action.)

Next: [Exceptions](exceptions.md) — how Java handles
things going wrong.
