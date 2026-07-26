# PORTING_POLICY.md
Version: 1.0
Status: Binding
Applies to: Citizens Gradle Port

# Purpose

This repository is a Gradle port of the official CitizensDev/Citizens2 project.

The official upstream repository is the only functional reference.

Repository:
https://github.com/CitizensDev/Citizens2

Default branch:
master

The Gradle fork must remain functionally identical to the official upstream.
Only build infrastructure may differ.

---

# Allowed changes

- Gradle
- Kotlin DSL
- Build configuration
- Dependency configuration
- Project structure
- CI
- Build tooling

---

# Forbidden changes

Do NOT introduce local functional differences.

Do NOT cherry-pick code from pull requests.

Do NOT implement local API extensions.

Do NOT compensate build problems by modifying source code.

Do NOT create fork-specific behaviour.

---

# Mandatory analysis order

Every task MUST follow this order.

## STEP 1

Compare all affected source files against the official upstream master.

If any source file differs:

STOP.

Synchronize with upstream first.

No functional analysis.

No optimisation.

No local fixes.

---

## STEP 2

Determine the origin of every non-upstream change.

Allowed origins:

- official master
- merged upstream commit
- official release branch

Special handling required:

- open pull request
- closed pull request
- local commit

Code originating from an open or closed pull request MUST NOT be integrated unless explicitly requested.

---

## STEP 3

If all sources are identical:

Compare the Gradle build against the official Maven build.

Verify:

- dependencies
- transitive dependencies
- exclusions
- repositories
- compiler configuration
- annotation processors
- generated resources
- active build profiles

Only Gradle differences may be corrected.

---

## STEP 4

Only after

- identical sources
- identical classpath

may source code be analysed or modified.

---

# Build policy

Compiler errors are NOT automatically source code errors.

Always determine whether the problem originates from

- source code
- build configuration
- dependency resolution
- repository configuration
- missing artifacts

Never compensate build configuration differences by introducing new source code.

---

# Architecture policy

Never introduce

- wrappers
- bridges
- facade methods
- helper APIs
- delegation layers

unless they already exist in the official upstream or are explicitly requested.

---

# Commit classification

Every commit MUST belong to exactly one category.

SYNC

Synchronize with upstream.

BUILD

Gradle or build infrastructure only.

INFRA

Repository or tooling only.

UPSTREAM_FIX

A confirmed defect existing in the official upstream.

---

# Required commit header

Every commit report MUST contain

Upstream Repository:
https://github.com/CitizensDev/Citizens2

Upstream Branch:
master

Upstream Commit:
<sha>

Source Classification:
MASTER
MERGED_COMMIT
LOCAL
OPEN_PR
CLOSED_PR

Commit Category:
SYNC
BUILD
INFRA
UPSTREAM_FIX

---

# Goal

The Gradle fork shall behave as an alternative build system for the official
Citizens project.

Functional behaviour shall remain equivalent to the official upstream.

All functional improvements belong upstream whenever possible.
