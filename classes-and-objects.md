# Classes and Objects

**Scope:** what a class is, creating objects with `new`,
fields, constructors, and encapsulation. All samples were
compiled and run with OpenJDK 21.

## The idea

A **class** is a blueprint; an **object** is a thing built
from it. The class `Dog` describes what dogs have (a name)
and do (bark); each `Dog` object has its own name.

```java
public class Dog {
    String name;                      // a field: each dog's own data

    void bark() {                     // a method: what dogs do
        System.out.println(name + " says woof!");
    }

    public static void main(String[] args) {
        Dog d1 = new Dog();           // build a Dog object
        d1.name = "Rex";
        d1.bark();

        Dog d2 = new Dog();
        d2.name = "Luna";
        d2.bark();
    }
}
```

**Check:** prints `Rex says woof!` then `Luna says woof!`.

Notes:

- `new Dog()` builds the object; `d1` is a *reference*
  to it (think: a nametag tied to the dog, not the dog
  itself).
- `bark()` is **not** `static` here — it belongs to each
  object, and uses that object's `name`. That's why
  `main` (static) had to build dogs first: static code
  can't call instance methods without an object.

## Constructors

`d1.name = "Rex"` after construction is clumsy. A
**constructor** runs at `new` time and sets things up:

```java
public class Dog {
    String name;

    Dog(String name) {        // the constructor: same name as the class,
        this.name = name;     // no return type
    }

    void bark() {
        System.out.println(name + " says woof!");
    }

    public static void main(String[] args) {
        Dog d = new Dog("Rex");
        d.bark();
    }
}
```

**Check:** prints `Rex says woof!`.

`this.name` means "this object's `name` field" —
needed because the parameter is also called `name`.
If you define no constructor, Java gives you a free
empty one (`new Dog()`).

## Encapsulation: keep fields private

Direct field access (`d.name = ...`) works until someone
sets `d.name = null` and `bark()` prints `null says
woof!`. The fix: `private` fields plus methods that guard
them:

```java
public class Dog {
    private String name;

    Dog(String name) {
        setName(name);
    }

    void setName(String name) {
        if (name == null || name.isBlank()) {
            throw new IllegalArgumentException("name required");
        }
        this.name = name;
    }

    String getName() {
        return name;
    }

    void bark() {
        System.out.println(name + " says woof!");
    }
}
```

`private` means "only code inside this class may touch
it." Outsiders go through `getName`/`setName` (called
*getters* and *setters*), where you can validate.
`throw` and `IllegalArgumentException` are [Exceptions](exceptions.md)
— peek ahead if you're curious.

## Static vs instance, finally

| | `static` | instance (no `static`) |
|---|---|---|
| Belongs to | the class itself | each object |
| Called as | `Math.sqrt(9)` | `d.bark()` |
| Can use | other statics only | fields, instance and static methods |
| Example | `main`, utility functions | `name`, `bark()` |

Rule of thumb: if a method needs an object's data, it's
instance. If it's a pure calculation on its arguments,
`static` is fine.

## Try it

In `jshell`, classes work too:

```
jshell> class Cat { String name; void meow() { System.out.println(name + ": meow"); } }
jshell> Cat c = new Cat(); c.name = "Miso"; c.meow();
Miso: meow
```

Next: [Interfaces and
Inheritance](interfaces-and-inheritance.md) — how classes
relate to each other.
