---
title: "Boost App Visibility with This Secret Tip"
date: 2025-06-18
description: Use kMDItemKeywords to make your app findable
image: images/posts/kMDItemKeywords.png
categories:
  - iOS
  - development
tags:
  - feature
draft: false
author: ben
---

## 🚀 Discover a simple yet powerful spotlight technique to make your iOS app more discoverable

Follow these steps to ensure your app appears in Spotlight and the iOS App Library 📚 under multiple names, not just its display name.

‼️ You won't find this one in Apple’s official documentation (at least not for iOS).

### 1. Update Your App’s 𝗜𝗻𝗳𝗼.𝗽𝗹𝗶𝘀𝘁:
- Add a new key [kMDItemKeywords](https://developer.apple.com/documentation/coreservices/kmditemkeywords)
- Set the type to String

### 2. Set the Keywords:
- Enter a comma-separated list of alternative names you want users to find your app by. This can include previous app names, common typos, or even the names of competing apps 🤐

 <!-- Hint: this is using a shortcode to display the image -->
{{< image src="images/posts/kMDItemKeywords_demo.png" alt="kMDItemKeywords" width="600" >}}

### 3. Test the Changes:
- **Important**: Delete any previous version of the app before reinstalling it on your phone/ simulator to ensure the changes take effect
- Install the app on your device or simulator and search for the new keyword via Spotlight or in your App Library


### 👉 𝗣𝗿𝗼 𝗧𝗶𝗽:
If you’re using string catalogues for your info.plist, you can easily create localized versions of this keyword list for each locale your app supports.


## Conclusion
By leveraging the hidden potential of the kMDItemKeywords property in your app’s Info.plist, you can significantly boost your app’s discoverability across Spotlight and the iOS App Library. Give this spotlight technique a try and watch your app become easier for users to find, no matter what they search for!