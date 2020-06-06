---
layout: post
title:  "Hide navigation bar space for SwiftUI"
date:   2020-06-03 14:48:56 +0100
categories: xcode swiftui
featured: true
image: assets/images/jumbotron.jpg
hidden: true
---

The first solution is to hide the navigation bar:

```swift
NavigationView {
    Text("Test")
        .navigationBarTitle("") // Must be called to hide
        .navigationBarHidden(true)
}
```

It however hides the navigation bar for all of the views. 

---

2nd solution is to show a inline navigation:

```swift
NavigationView {
    Text("Test")
        .navigationBarTitle("", displayMode: .inline)
}
```