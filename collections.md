# Collections

**Scope:** `List`/`ArrayList`, `Map`/`HashMap`, generics,
and iterating. All samples were compiled and run with
OpenJDK 21.

## Why not just arrays?

Arrays (`String[]`) are fixed-size — once created, they
never grow. Real programs need lists that grow, shrink,
and search. That's `java.util`:

```java
import java.util.ArrayList;
import java.util.List;

public class Lists {
    public static void main(String[] args) {
        List<String> fruits = new ArrayList<>();
        fruits.add("apple");
        fruits.add("banana");
        System.out.println(fruits.size());   // 2
        System.out.println(fruits.get(0));   // apple

        for (String fruit : fruits) {
            System.out.println(fruit);
        }
        fruits.remove("apple");
        System.out.println(fruits);          // [banana]
    }
}
```

**Check:** prints `2`, `apple`, the two fruits, `[banana]`.

Three things to notice:

- **`List<String>` is the interface, `ArrayList<>` the
  implementation** — the [Interfaces](interfaces-and-inheritance.md)
  pattern in daily use. Declare the interface type; pick
  the implementation at construction.
- **The `<>` (diamond)** means "same type arguments as the
  left side" — `new ArrayList<>()` instead of repeating
  `<String>`.
- **`System.out.println(fruits)`** prints `[banana]` —
  collections have readable `toString()` output. Handy
  for debugging.

## Generics: the `<String>` part

`List<String>` means "a list holding Strings, and the
compiler will enforce it":

```java
List<String> names = new ArrayList<>();
names.add("Ada");
names.add(42);              // compile error: incompatible types
String first = names.get(0); // no cast needed — the compiler knows
```

Without generics (raw `List`), you'd get `Object` back
and cast everywhere — the pre-2004 way, now a warning.
Always parameterize.

Primitives can't go in collections directly — use the
wrapper classes:

| Primitive | Wrapper |
|---|---|
| `int` | `Integer` |
| `long` | `Long` |
| `double` | `Double` |
| `boolean` | `Boolean` |
| `char` | `Character` |

```java
List<Integer> scores = new ArrayList<>();
scores.add(95);          // auto-boxed: int -> Integer
int top = scores.get(0); // auto-unboxed: Integer -> int
System.out.println(top); // 95
```

**Check:** prints `95`. *Autoboxing* converts silently;
it costs a little performance in hot loops, but you can
ignore that until a profiler tells you otherwise.

## Maps: keys to values

A `Map` pairs keys with values — dictionaries in Python,
objects-as-hashmaps in JavaScript:

```java
import java.util.HashMap;
import java.util.Map;

public class Maps {
    public static void main(String[] args) {
        Map<String, Integer> ages = new HashMap<>();
        ages.put("Ada", 36);
        ages.put("Grace", 85);
        System.out.println(ages.get("Ada"));          // 36
        System.out.println(ages.get("Unknown"));      // null
        System.out.println(ages.containsKey("Grace")); // true

        for (String name : ages.keySet()) {
            System.out.println(name + " is " + ages.get(name));
        }
    }
}
```

**Check:** prints `36`, `null`, `true`, then the two
entries (order not guaranteed — `HashMap` doesn't sort).

`get()` on a missing key returns `null` — check with
`containsKey()` first, or use `getOrDefault(key,
default)`.

## Choosing between them

| Need | Use |
|---|---|
| Ordered items, duplicates OK | `List` / `ArrayList` |
| Unique items, fast "is it in there?" | `Set` / `HashSet` |
| Look up by key | `Map` / `HashMap` |
| Fixed size, primitives, speed | array (`int[]`) |

`ArrayList` covers 90% of list needs. (`LinkedList`
exists; you almost never want it — random access is
slow.)

Next: [Troubleshooting](troubleshooting.md) — the
errors you'll actually hit, symptom → fix.
