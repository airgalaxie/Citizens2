Citizens welcomes contributors and pull requests. Feel free to join the [Discord](https://discord.gg/Q6pZGSR) for tips and tricks when writing your first pull request.

Before you get started, bear in mind that we do require a Contributor's License Agreement (CLA) to prevent licensing issues in the future.
Sign the CLA [here](https://cla-assistant.io/CitizensDev/Citizens2)

Development environment setup
=============================
1. Clone Citizens2 and CitizensAPI repos to your machine
2. Import the Gradle project into your IDE of choice. This branch targets Java 25 bytecode and is intended to build with Java 26.

Citizens is structured as a Gradle multi-project build:
`main` - the main Citizens codebase which implements commands and Spigot plugin-specific code
`v1_21_R7`, `v26_1_R1`, `v26_2_R1` - version-specific NMS modules
`dist` - the distribution subproject which builds the runnable Citizens JAR from the selected modules

3. Build your first Citizens2 JAR with Gradle:

```bash
./gradlew clean build
```

The default `dev` profile builds `main` and `v26_2_R1`. Use
`-Pprofile=spigot-release` when you need the full release module set.

Now you're ready to start creating a pull request!

Creating a pull request
=======================
1. Pull request your changes to the relevant Citizens repo using Github's pull request feature
2. Sign the CLA and make sure you own the rights to all of your contributions
3. Include JavaDocs for your code that other people might use, such as API methods
4. There are no specific style requirements at present
