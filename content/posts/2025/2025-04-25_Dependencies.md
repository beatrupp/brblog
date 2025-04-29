---
title: "Are you keeping up with 3rd party dependencies?"
date: 2025-04-25T12:00:38+02:00
slug: /managing-dependencies
description: Discover how to keep up to date
image: images/1.jpg
caption: Photo by Beat Rupp
categories:
  - iOS
tags:
  - dependencies
  - 3rd-party-libraries
  - security
draft: false
params:
  author: Beat Rupp
---

# Are you keeping up with 3rd party dependencies?

- Why would you invest time to update dependencies?
- Is there an easy way?

Installation

```bash
brew install swift-outdated
```

In your project directory, run the following command to check your dependencies:

```bash
swift-outdated
```

```swift
 import Foundation

 public class Test {
    /// This is a comment
    let x: Int = 10
 }
```
