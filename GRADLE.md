# Gradle Build

This branch is a standalone Gradle-first Citizens2 project. Maven is not a
supported build system for this branch. Gradle dependency and plugin versions
are kept in:

```text
gradle/libs.versions.toml
```

Use the Gradle wrapper for all builds.

Full verification build:

```bash
./gradlew clean build
```

Default development plugin JAR:

```bash
./gradlew -Pprofile=dev :dist:pluginJar
./gradlew -PBUILD_NUMBER=4211 -Pprofile=dev :dist:pluginJar
```

Optional release module set:

```bash
./gradlew -Pprofile=spigot-release clean build
./gradlew -Pprofile=spigot-release :dist:pluginJar
```

The release profile compiles every included NMS module and requires the
corresponding Spigot artifacts to be resolvable from the configured Gradle
repositories or the local dependency cache.

If no profile is passed, Gradle uses the `dev` profile. That builds only:

```text
main
v26_2_R1
```

So this command also uses the dev module set by default:

```bash
./gradlew clean build --refresh-dependencies --info
```

The build targets Java 25 bytecode and is intended to run with a Java 26 build
environment:

```bash
JAVA_HOME=/usr/lib64/jvm/java-26-openjdk-26 ./gradlew clean build --refresh-dependencies --info
```

If Gradle is run with a JRE instead of a JDK, pass a compiler explicitly:

```bash
./gradlew -PjavacExecutable=/path/to/javac -Pprofile=dev :dist:pluginJar
```

The runnable plugin JAR is written to:

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

Build details:

```text
The branch includes a Gradle 9.6.1 wrapper and uses the com.gradleup.shadow
9.5.1 plugin.

Paper API 26.2 is selected by default through the version catalog.

The spigot-release profile requires all Spigot artifacts to exist locally or
remotely. In this workspace, `org.spigotmc:spigot:1.21.11-R0.2-SNAPSHOT` is not
available, so the default `dev` profile is the verified self-contained build.

The Paper API version can be overridden with -PpaperVersion=<version>.
```
