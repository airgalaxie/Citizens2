# Citizens Gradle Port Policy

## Purpose

This repository is a Gradle port of the official Citizens project.

The goal is to remain functionally equivalent to the official upstream while replacing only the build infrastructure.

Official upstream:

https://github.com/CitizensDev/Citizens2

Default branch:

master

---

## Principles

The official upstream is the only functional source of truth.

Functional behaviour follows upstream.

Build infrastructure follows Gradle.

---

## Synchronization

Before implementing any functional change:

1. Synchronize with the current upstream master.
2. Verify that local sources match upstream.
3. Verify that the Gradle build provides the same compile-time environment as the official Maven build.

Only if both source and build are equivalent may a source-code defect be investigated.

---

## Scope

Allowed:

- Gradle
- Build configuration
- Dependency management
- Project structure
- Build tooling

Not allowed:

- Local functional divergence
- Permanent fork-specific behaviour
- Partial adoption of non-merged upstream work

---

## Philosophy

This repository is maintained as an alternative build system, not as an alternative implementation.

Whenever possible, functional improvements belong in the official upstream.
