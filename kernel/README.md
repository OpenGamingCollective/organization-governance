# OGC Kernel Repository Layout and Workflow

## 1. Introduction

The Open Gaming Collective (OGC) maintains a custom Linux kernel intended for use by downstream distributions and their users. This document describes the repository layout, workflows, and policies for developing, maintaining, and distributing OGC kernel patches.

The goal is to:

* Provide a structured development environment for kernel-related work.
* Provide a fast way for patch developers to distribute their work, and provide a way to quickly install (experimental) kernels to the downstream users.
* Enable downstream distributions to selectively consume OGC-maintained patch sets.
* Maintain alignment with upstream Linux development wherever possible.

---

## 2. Guiding Principles

### 2.1 Upstream-First Policy

OGC follows an **upstream-first** development model. Any patch series proposed for inclusion must fall into one of the following categories:

1. **Work-in-Progress (WIP) Patches**

   * Patches under active development that are intended for upstream submission.
   * OGC serves as a testing and validation ground.
   * Requirement: The patch series **must already be posted to a public mailing list** before OGC will consider merging it.
   * Example: `asus-linux` patches.

2. **Non-Upstreamable Patches**

   * Patches that cannot realistically be accepted upstream.
   * OGC assumes responsibility for maintaining these patches.
   * Patches are periodically reviewed for relevance, applicability, and maintenance burden.
   * Examples: handheld-specific hardware support, gaming-specific kernel behavior.

3. **Externally Maintained Patch Sets**

   * Patches maintained by third parties (e.g. CachyOS, Linux stable).
   * The OGC org will merge and keep up with these patches.
   * These patches are also periodically reviewed for relevance and maintenance cost.

**Patches that do not clearly fit into one of these categories will not be accepted.**

---

## 3. Repository Overview

To support both development and distribution, OGC will maintain two primary repositories:

1. **Development Kernel Repository**
2. **Kernel Package Repository**

Each repository serves a distinct purpose and audience.

---

## 4. Development Kernel Repository

### 4.1 Purpose

This repository is dedicated exclusively to **kernel patch development and testing**. It is not intended to provide production-ready kernels.

### 4.2 Repository Origin

* **Forked from:** `torvalds/linux`
* **Branched from:** tagged releases e.g. `6.18`

### 4.3 Continuous Integration and Builds

* GitHub Actions are used to automatically build kernel packages on:

  * Pull request creation or updates targeting an OGC branch.
  * Manual workflow triggers for developers.
* These builds are:

  * **For testing purposes only**
  * **Not officially supported**

### 4.4 Supported Package Formats (Built at PR Time or Manual trigger from a developer)

* Fedora (latest version available at build time)
* Arch Linux (packages frozen at build time)
* Ubuntu (latest version available at build time)

---

### 4.5 Pull Request Requirements

* All supported package formats are built for every pull request.
* Builds use the KConfig files stored in the repository:

  * **Base configuration:** Arch Linux KConfig
  * **Additional configuration:** Development-specific options, which may be freely modified by patch developers to set default values.
* Each pull request and its commits **must include a reference to the upstream submission** (e.g. mailing list link).

---

### 4.6 Branching Model

#### OGC Release Branches

* Kernel development occurs on branches suffixed with `/OGC`.

  * Example: Kernel version `6.18` → `6.18/OGC`
* The history of `/OGC` branches **must not be rewritten**.

  * Only merge commits and tag commits are permitted.
  * Updates to patch series and/or linux-stable are applied via merges only.
  * This means that these branches will not be rebased for a clear history.

#### Tagging and Releases

* When a tag is created on a `<version>/OGC` branch:

  * A GitHub Release is automatically generated.
  * The release contains patch files relative to mainline.
  * These patches are consumed by the Kernel Package Repository.

#### Branch Naming Rules

* **OGC release branches:**

  * Must start with the kernel version (e.g. `6.18/OGC`)
* **Developer feature branches:**

  * Must be prefixed with the developer’s name
  * Example: `6.18/pastaq/some-feature`
* Feature branches:

  * Do **not** need to be based directly on mainline.
  * May track other remotes for development flexibility.
* Before opening a pull request into an `/OGC` branch:

  * Developers **must rebase** their branch onto the target `/OGC` branch.

---

### 4.7 Developer Tooling

To improve the developer experience, the repository will provide:

* VS Code devcontainers with local caching to speed up builds.
* An automated rebase script to assist rebasing onto:

  * `<version>/OGC` branches
  * Other upstream or third-party remotes

---

## 5. Kernel Package Repository

### 5.1 Purpose

The Kernel Package Repository is responsible for:

* Creating **release-ready kernel packages**
* Publishing and signing packages
* Providing a flexible structure that allows downstream distributions to:

  * Select specific patch sets
  * Customize packaging workflows

This mirrors approaches used by projects such as CachyOS, which differentiate between handheld and general-purpose kernels.

---

### 5.2 Repository Structure

Proposed layout:

```
arch/
  - PKGBUILD
  - kconfig

bazzite/
  - spec
  - kconfig

chimeraos/
  - PKGBUILD
  - kconfig

fedora/
  - spec
  - kconfig

ubuntu/
  - build files
```

---

### 5.3 Downstream Distribution Responsibilities

* Each downstream distribution is responsible for:

  * Maintaining its own build files
  * Defining supported versions
* If a distribution chooses to relinquish maintenance:

  * It may symlink its configuration to another distribution
  * Example: `chimeraos` symlinking to `arch`

---

### 5.4 Release and Distribution Model

* **Rolling distributions:**

  * Releases are distributed via container images and rebuilt periodically (e.g. daily or weekly)

* **Non-rolling distributions:**

  * Releases are distributed as packages via GitHub Releases.
* Downstream distributions may choose to alter this model if desired.

---

### 5.5 Signing and Support Policy

* Kernels for **Arch, Fedora, and Ubuntu**:

  * Are officially supported by OGC.
  * Are signed using the OGC signing key.
* Other distributions:

  * May use their own signing keys if desired.
  * Are not officially supported by OGC unless explicitly stated.

---

## 6. Summary

This document outlines:

* A clear separation between kernel development and packaging.
* A strict but flexible upstream-first policy.
* Predictable branching and release practices.
* A modular packaging approach that empowers downstream distributions.

Together, these practices aim to ensure maintainability, transparency, and long-term sustainability of OGC’s kernel efforts.