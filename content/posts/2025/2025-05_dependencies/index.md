---
title: "Code Rot is Real: Stay Fresh with Library Updates"
date: 2025-05-24
description: "Keeping Your Dependencies Updated to Avoid Security and Stability Pitfalls"
slug: keeping-dependencies-updated
image: images/posts/dependencies-title.png
categories:
  - ios
  - development
tags:
  - dependencies
  - 3rd-party-libraries
  - security
  - spm
draft: false
author: beat
---

In the world of app development, time is never standing still. Even if your project doesn't change much, the world around it is constantly evolving. Not only operating systems and compilers change, but also libraries receive updates - sometimes even critical security updates - that should be applied rather sooner than later to protect your customer's data.

Most projects depend on some third-party dependencies for example to simplify networking, to enable user tracking or just by incorporating [a beautiful
UI component](https://github.com/benrudhart/AppleEffortScorePicker) that doesn't need to be written from scratch.

How can you keep track of all this?

The first and direct approach is to use Xcode's `File` > `Packages` > `Update to latest Package Versions`. This works fine as long as you don't have a custom dependency management, which is often used in bigger projects.

However, with this approach it's intransparent what actually is updated and what changes are incorporated from 3rd party libraries. With some luck, your project will still compile and work after such a dependency update. If you want to know a bit more what exactly will be udpated and what has changed in between, you need to dig a bit deeper.

Fortunately, for Swift Package Manager-based projects there is a tool called [swift-outdated](https://github.com/kiliankoe/swift-outdated) that can assist you.

Install it via [homebrew](https://brew.sh):

```bash
brew install swift-outdated
```

In your project directory, run it as follows to check your dependencies:

```bash
swift-outdated
```

This will show you a table such as this

![swift-outdated output](swift-outdated-output.png)

and list all your dependencies, the currently resolved version and the latest version available in their upstream repository. And conveniently, a clickable link to the project's web page.

The color code of the version number gives you an idea how old the dependency is:

| color| dependency "age"|
|-------| -- |
| white | current (it can still differ in minor or patch versions, though) |
| green | one major version behind |
| yellow | two major versions behind |
| red | more than 3 major versions behind |

With this table you can now visit the project page of each dependency to check their changelog and get an idea whether you need to update your code for the update to work smoothly.
