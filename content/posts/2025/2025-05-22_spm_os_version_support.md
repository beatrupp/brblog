---
title: "Swift Package Manager’s Platforms Trap"
date: 2025-07-22
description: Why @available is Your New Best Friend
image: images/posts/spm_os_versions.png
categories:
  - iOS
  - development
tags:
  - feature
draft: true
author: ben
---
When building Swift packages that leverage APIs from the latest OS versions, developers face a critical dilemma:

> How do I create cutting-edge packages while supporting apps that haven’t adopted the latest OS?

```swift
// The deceptive simplicity of platform declarations
let package = Package(
    name: "ModernKit",
    platforms: [.iOS(.v18), .watchOS(.v11)], // ❌ Recipe for adoption disaster
    // ...
)
```

### The Brutal Reality
The only viable path 😢

1. **SPM’s Iron Rule**

   Your package’s minimum deployment target must be ≤ the consumer app’s target. A package declaring iOS 18 simply cannot be used in iOS 17 projects. This is because **weak linking** of packages is [not supported by SPM](https://github.com/swiftlang/swift-package-manager/issues/6632#issuecomment-1574138076), and the Compiler will emit an error when trying to import a library with a higher OS version than the app targets deployment version.

2. **The @available Tax**

   If you decide to lower the supported platform version, you’ll need to [add availability conditions](https://forums.swift.org/t/pitch-spm-lift-minimum-deployment-target-constraint-for-package-dependencies/53783/2) to every API that uses new platform features. This can quickly become tedious as your package grows 😬.

   ```swift
   @available(iOS 18, watchOS 11, *)
   public struct MyPublicType {
       public func foo() -> Bar { ... }
   }
   ```

## Conclusion

As an (open source) package maintainer, you must make a clear decision: do you want to support only the latest OS versions (and thus drop support for apps targeting older OSes), or are you willing to add `@available` conditions to all relevant types and APIs (which can be labor-intensive)? 

There’s currently no way around this with Swift Package Manager — your package’s minimum deployment target (aka platforms) must not exceed that of the consuming app, and supporting new APIs on older OSes means embracing the `@available` tax.