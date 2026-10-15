# Installing Java

**Scope:** getting a JDK on your machine, confirming it works,
and knowing which Java runs when you type `java`. Package
names below were checked against Debian/Ubuntu docs in
October 2026; Homebrew and Windows steps follow the vendors'
own instructions.

## Pick a JDK

You want an **LTS** release (see [What Is Java?](what-java-is.md)).
Two free, reputable sources cover everyone:

| Source | Good for | Package / how |
|---|---|---|
| Your Linux distro | Debian/Ubuntu/Mint | `sudo apt install openjdk-21-jdk` (or `openjdk-25-jdk` on Debian 13+) |
| [Temurin](https://adoptium.net/) (Eclipse Adoptium) | Windows, macOS, any Linux | Installer or archive from adoptium.net |

Avoid Oracle's branded JDK download unless you enjoy
reading license agreements — OpenJDK builds are the same
language, free for any use.

**Which version?** 21 if you want maximum compatibility
with existing tutorials and employers; 25 if you want the
current LTS. Everything in this guide works on 17 and up.

## Linux (Debian/Ubuntu/Mint)

```sh
sudo apt update
sudo apt install openjdk-21-jdk
```

**Check:**

```sh
java -version
javac -version
```

Expected (patch numbers move over time; the `21` is what
matters):

```
openjdk version "21.0.7" 2025-04-15
OpenJDK Runtime Environment (build 21.0.7+6-Ubuntu-0ubuntu124.04)
...
javac 21.0.7
```

Both commands must work. `java` runs programs; `javac`
compiles them. If `javac` is missing you installed a JRE
package by mistake — install the `-jdk` one.

## macOS

```sh
brew install --cask temurin21
```

**Check:** same `java -version` / `javac -version` as above.

Without Homebrew, download the macOS installer from
[adoptium.net](https://adoptium.net/) and run it.

## Windows

Download the Windows MSI installer from
[adoptium.net](https://adoptium.net/), run it, and accept
the option to set `JAVA_HOME` and update `PATH` (the
installer offers both — say yes).

**Check** in PowerShell:

```powershell
java -version
javac -version
```

## If you have several Javas

Developers accumulate JDKs. `java -version` shows the one
your `PATH` finds first. To see all of them:

```sh
# Linux: lists every installed java
update-alternatives --list java
```

```sh
# macOS: lists every installed JDK
/usr/libexec/java_home -V
```

On Windows, check `JAVA_HOME` in
*Settings → System → About → Advanced system settings →
Environment Variables*. Point it at the JDK you want
(e.g. `C:\Program Files\Eclipse Adoptium\jdk-21.0.7.6-hotspot`)
and make sure `%JAVA_HOME%\bin` is on `PATH`.

## A handy extra: jshell

The JDK ships a *read-eval-print loop* called `jshell`
(Java 9+). It runs snippets instantly without files —
perfect for trying things from this guide:

```sh
jshell
```

```
|  Welcome to JShell -- Version 21.0.7
|  For an introduction type: /help intro

jshell> 3 * 7
$1 ==> 21

jshell> /exit
```

Type `/exit` to leave. You'll see `jshell>` prompts in
later chapters wherever a quick experiment fits.

## What this doesn't cover

Maven and Gradle — the build tools real Java projects
use instead of raw `javac`. You don't need them for this
guide; every program here compiles with plain `javac`.
When your project outgrows single files, learn Maven
first (simpler mental model), Gradle second.
