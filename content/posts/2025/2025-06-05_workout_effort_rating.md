---
title: "Make Your Fitness App Stand Out with Effort Ratings"
date: 2025-06-04
description: How to catch up with Apple's Fitness & Workout App
image: images/posts/workout_effort_picker.png
categories:
  - iOS
  - development
tags:
  - HealthKit
  - 3rd party libraries
draft: false
author: ben
---
Apple raised the bar for fitness apps with the introduction of effort ratings in iOS 18 and watchOS 11! If you missed their [announcement](https://www.youtube.com/shorts/SGPTKzZVpbc), now’s the perfect time to catch up.

With new `HealthKit` APIs, developers can also bring this highly-requested feature to their own apps. Here’s how you can make your fitness app as polished and user-friendly as Apple’s ✨!

## What Are Effort Ratings?

Effort ratings let users log how hard a workout felt, from “Easy” to “All in”. This personal touch can help users track progress, stay motivated, and get more out of every session.

### The HealthKit APIs

Apple introduced two key APIs for effort ratings:

- [HKQuantityTypeIdentifier.workoutEffortScore](https://developer.apple.com/documentation/healthkit/hkquantitytypeidentifier/workouteffortscore): The identifier for effort [rating samples](https://developer.apple.com/documentation/healthkit/hksampletype)
- [HKUnit.appleEffortScore](https://developer.apple.com/documentation/healthkit/hkunit/appleeffortscore()): The unit for effort ratings

As always Apple "forgot" 🙄 to publish the documentation, so here’s what you need to know:

- The effort rating is an `Int` value:
    - 0: User skipped the rating
    - 1 to 10: Levels from “Easy” (1) to “All in” (10)
- Any other value will cause HealthKit to throw an error

### Requesting Permissions

Before you can read or write effort ratings, you’ll need user permission:

```swift
let effortType = HKQuantityType(.workoutEffortScore)
try await healthStore.requestAuthorization(toShare: [effortType], read: [effortType])
```

### Reading Effort Ratings

To read a stored effort rating for a specific workout:

```swift
let predicate = HKQuery.predicateForWorkoutEffortSamplesRelated(workout: workout, activity: nil)
let sortDescriptor = NSSortDescriptor(key: HKSampleSortIdentifierStartDate, ascending: false)

let query = HKSampleQuery(
    sampleType: HKQuantityType(.workoutEffortScore),
    predicate: predicate,
    limit: 1,
    sortDescriptors: [sortDescriptor]
) { _, results, error in
    let sample = results?.first as? HKQuantitySample
    let effortRating = sample?.quantity.doubleValue(for: .appleEffortScore())
    // handle effort score
}

healthStore.execute(query)
```

### Writing Effort Ratings

To save a new effort rating for a workout:

```swift
let newRating: Int // values 0 ... 10
let sample = HKQuantitySample(
    type: HKQuantityType(.workoutEffortScore),
    quantity: HKQuantity(unit: .appleEffortScore(), doubleValue: Double(newRating)),
    start: workout.startDate,
    end: workout.endDate
)

try await healthStore.relateWorkoutEffortSample(sample, with: workout, activity: nil)
```

## 🚀 Introducing WorkoutEffortPicker

Ready to wow your users? Apple’s APIs are powerful, but they didn’t provide a ready-made UI component for effort ratings 😢. That’s where my package [WorkoutEffortPicker](https://github.com/benrudhart/WorkoutEffortPicker) comes in 🎉🎁!

Why you’ll love it:
- Built with pure SwiftUI, it closely mimics Apple’s own effort picker
- Seamless integration — simple to integrate and easy to use
- Convenience extensions on [HKHealthStore](https://github.com/benrudhart/WorkoutEffortPicker/blob/main/Sources/WorkoutEffortPicker/Helper/HKHealthStore%2BWorkoutEffortScore.swift) make reading and writing effort ratings a breeze
- The [WorkoutEffortScore](https://github.com/benrudhart/WorkoutEffortPicker/blob/main/Sources/WorkoutEffortPicker/WorkoutEffortScore.swift) enum ensures you only use valid effort values, eliminating bugs from invalid entries

### Conclusion

Adding effort ratings is a small tweak that can make a huge difference in user engagement and satisfaction. With Apple’s new APIs and the `WorkoutEffortPicker` package, you can deliver a premium experience that keeps users coming back for more.

Ready to level up your fitness app? 👉 Check out [WorkoutEffortPicker on GitHub](https://github.com/benrudhart/WorkoutEffortPicker) and improve your app with a few lines of code!

Spotted a typo or have suggestions? Drop a comment or reach out—I’d love to hear your feedback!