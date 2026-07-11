Citizens2 README
================

Fork branch notice
==================

This branch is a standalone Gradle-first Citizens2 project. Maven is not a
supported build system for this branch.

Citizens is an NPC plugin for the Bukkit API. It was first released on March 5, 2011, and has since seen numerous updates. Citizens provides an API which developers can use to create their own NPC characters. More information on the API can be found on the API page of the Citizens Wiki (https://wiki.citizensnpcs.co/API).

Building
========

Use the Gradle wrapper:

```bash
./gradlew clean build
```

The build targets Java 25 bytecode and is intended to run with a Java 26 build
environment. The default development build uses the `dev` profile and builds the
`main` and `v26_2_R1` modules. The optional release module set is available with:

```bash
./gradlew -Pprofile=spigot-release clean build
```

The release profile requires all configured Spigot artifacts to be resolvable
from the Gradle repositories or local dependency cache. The default development
profile is the self-contained build used for normal development.

The runnable plugin JAR is written to:

```text
dist/target/Citizens-2.0.43-b<BUILD_NUMBER>.jar
```

See `GRADLE.md` for build profiles, Java configuration, and output naming.

Compatible with:
* Minecraft (for specific compatible version information, see https://wiki.citizensnpcs.co/Versions for info)
* CitizensAPI (for compiling purposes only)

Extra information
=================

Javadoc: http://jd.citizensnpcs.co

Spigot page: https://www.spigotmc.org/resources/citizens.13811

Developmental builds: https://ci.citizensnpcs.co/job/Citizens2/

For questions/help join our discord at: https://discord.gg/Q6pZGSR
