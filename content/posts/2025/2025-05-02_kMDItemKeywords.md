---
title: "Boost App Visibility with This Secret Tip"
date: 2025-06-20
description: Use kMDItemKeywords to make your app findable
image: images/posts/kMDItemKeywords.png
categories:
  - iOS
  - development
tags:
  - feature
draft: true
author: ben
---

## 🚀 Discover a simple yet powerful spotlight technique to make your iOS app more discoverable.

Follow these steps to ensure your app appears in Spotlight and the iOS App Library 📚 under multiple names, not just its display name.

‼️ You won't find this one in Apple’s official documentation (at least not for iOS).

### 1. Update Your App’s 𝗜𝗻𝗳𝗼.𝗽𝗹𝗶𝘀𝘁:
- Add a new key **𝗸𝗠𝗗𝗜𝘁𝗲𝗺𝗞𝗲𝘆𝘄𝗼𝗿𝗱𝘀**
- Set the type to String

### 2. Set the Keywords:
 - Enter a comma-separated list of alternative names you want your app to be found by. This can include previous app names or even the names of competing apps 🤐

### 3. Test the Changes:
- **Important**: Delete any previous version of the app before reinstalling it on your phone/ simulator to ensure the changes take effect
- Install the app on your device or simulator and search for the new keyword via Spotlight or in your App Library


#### 👉𝗣𝗿𝗼 𝗧𝗶𝗽:
If you’re using string catalogues for your info.plist, you can easily create localized versions of this keyword list for each locale your app supports.

<!-- Hint: this is using a shortcode to display the image -->
{{< image src="images/posts/kMDItemKeywords_demo.png" alt="kMDItemKeywords" width="600" >}}
