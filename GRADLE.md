# Parallel Gradle Build

This branch adds a Gradle build next to the existing Maven build. The Maven
POMs are still authoritative. Gradle dependency and plugin versions are kept in:

```text
gradle/libs.versions.toml
```

Useful commands:

```bash
./gradlew -Pprofile=dev :dist:pluginJar
./gradlew -Pprofile=spigot-release :dist:pluginJar
./gradlew -PBUILD_NUMBER=4211 -Pprofile=dev :dist:pluginJar
```

If no profile is passed, Gradle uses the `dev` profile. That builds only:

```text
main
v26_2_R1
```

So this command also uses the dev module set by default:

```bash
./gradlew clean build --refresh-dependencies --info
```

The Gradle build targets Java 25 bytecode and can be run with Java 26:

```bash
JAVA_HOME=/usr/lib64/jvm/java-26-openjdk-26 ./gradlew clean build --refresh-dependencies --info
```

If Gradle is run with a JRE instead of a JDK, pass a compiler explicitly:

```bash
./gradlew -PjavacExecutable=/path/to/javac -Pprofile=dev :dist:pluginJar
```

The output jar is written to:

```text
dist/target/Citizens-2.0.43-b<BUILD_NUMBER>.jar
```

Build number priority:

```text
1. -PBUILD_NUMBER=<value>
2. BUILD_NUMBER environment variable
3. Git short commit hash, formatted as Gradle-g<hash>
4. Gradle-build fallback when Git is unavailable
```

With Git available and no explicit `BUILD_NUMBER`, the file is named like:

```text
dist/target/Citizens-2.0.43-bGradle-ged65ac7.jar
```

If Git is unavailable, the fallback file is named:

```text
dist/target/Citizens-2.0.43-bGradle-build.jar
```

Known differences from Maven:

```text
The branch includes a Gradle 9.6.1 wrapper and uses the com.gradleup.shadow
plugin.

The dev profile targets Java 25 bytecode and has been tested with Java 26:
JAVA_HOME=/usr/lib64/jvm/java-26-openjdk-26 ./gradlew clean build

The spigot-release profile still requires all Spigot artifacts to exist locally
or remotely. In this workspace, v1_21_R7 fails because
org.spigotmc:spigot:1.21.11-R0.2-SNAPSHOT is not available.

The v1_21_R7 module currently compiles against the remapped-mojang Spigot
artifact, but the Maven SpecialSource remap steps are not yet reproduced.

Gradle cannot use Maven's [26.2.build,) range directly, so the Paper API uses
the Gradle dynamic version 26.2.build.+ by default. It can be overridden with
-PpaperVersion=<version>.
```
