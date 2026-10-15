# Control Flow

**Scope:** `if`/`else`, `switch`, the three loops, and
breaking out early. All samples were compiled and run
with OpenJDK 21.

## If and else

```java
int temp = 85;

if (temp > 100) {
    System.out.println("Boiling");
} else if (temp > 32) {
    System.out.println("Liquid");
} else {
    System.out.println("Frozen");
}
```

**Check:** prints `Liquid`.

The condition must be a `boolean` — `if (temp)` doesn't
compile in Java. No truthy/falsy shortcuts like Python or
JavaScript; write the comparison out.

## Switch

For "one variable, many exact values," `switch` beats a
ladder of `else if`. The modern arrow form (Java 14+):

```java
int day = 3;
String name = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    default -> "Weekend-ish";
};
System.out.println(name);
```

**Check:** prints `Wednesday`.

The arrow form (`->`) returns a value and can't
accidentally "fall through" into the next case — the old
colon form could, which was a decades-long source of
bugs. Prefer arrows.

## The for loop

```java
for (int i = 1; i <= 3; i++) {
    System.out.println("Count: " + i);
}
```

**Check:** prints `Count: 1`, `Count: 2`, `Count: 3`.

Three parts in the parentheses: *start* (`int i = 1`),
*keep going while* (`i <= 3`), *step* (`i++`, meaning
"add one"). The loop variable `i` exists only inside the
loop.

## The for-each loop

For walking through every element of an array or list:

```java
String[] fruits = {"apple", "banana", "cherry"};
for (String fruit : fruits) {
    System.out.println(fruit);
}
```

**Check:** prints each fruit on its own line. Read the
colon as "in": "for each fruit *in* fruits." No indexes
to get wrong — use this whenever you don't need the
index.

## The while loop

```java
int n = 3;
while (n > 0) {
    System.out.println(n);
    n--;
}
```

**Check:** prints `3`, `2`, `1`. `while` repeats as long
as the condition holds. If the condition never becomes
false, the loop never ends — the classic infinite loop.
(Every programmer writes one. `Ctrl+C` stops a runaway.)

## Break and continue

```java
for (int i = 1; i <= 10; i++) {
    if (i == 3) {
        continue;   // skip 3, keep looping
    }
    if (i == 6) {
        break;      // stop the loop entirely
    }
    System.out.println(i);
}
```

**Check:** prints `1`, `2`, `4`, `5`. `continue` skips to
the next round; `break` walks out of the loop.

## A note on braces

Java doesn't require braces for single-statement bodies:

```java
if (temp > 100)
    System.out.println("Boiling");
```

Don't. The day someone adds a second line without adding
braces, the program silently does the wrong thing. Always
use braces — every linter agrees.

Next: [Methods](methods.md) — packaging logic into
reusable, named chunks.
