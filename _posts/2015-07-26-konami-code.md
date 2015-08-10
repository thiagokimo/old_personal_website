---
layout: post
title: "Konami Code"
date: 2015-07-26 23:01
summary: Adding our favorite easter-egg in any Android app.
---

A Few days ago I was wondering how does an easter-egg like the **Konami Code** in Google Play Games works. Since Google Play Games is not open-source I had no option but trying to reproduce it by myself.

<center><iframe width="420" height="315" src="https://www.youtube.com/embed/59xCH_1CAPc" frameborder="0" allowfullscreen></iframe></center>

Before starting any kind of hack I like to write down what would I think will be the main important/challenging topics to accomplish my goals. I came up with the following points:

- Detect swipe gestures
- Register a sequence of swipes
- Show a dialog with buttons
- Register a sequence of pressed buttons
- Show a final message to the user

With those points in mind, I've divided the Konami Code into 2 parts: The **Directional Part**, which is the moment where the user executes the *UP, UP, DOWN, DOWN, LEFT, RIGHT, LEFT and RIGHT* sequence; and the **Buttons Part**, which is the moment where the user presses the *B, A and START* buttons. Let's hack!

### The Directional Part
To detect swipe gestures I've created a [SimpleOnGestureListener](http://developer.android.com/reference/android/view/GestureDetector.SimpleOnGestureListener.html), implementing the **onFling** method. The gesture listener stores any swipes done by the user and checks if the last added swipe follows the the Konami Code. When the sequence is completed a dialog shows up with the necessary buttons to perform the second part of the code, otherwise previously stored swipes are cleared from the memory and the user must swipe all over again.

### The Buttons Part
It was the easiest part. I showed a custom [AlertDialog](http://developer.android.com/reference/android/app/AlertDialog.html) with the buttons representing the keys **A**, **B** and **START** inside it. The same principle of the *Directional Part* was applied here: The order of the pressed buttons was stored. Whenever the order gets wrong the dialog closes and the user must begin the whole Konami Code again. When the buttons are pressed in the correct order, the dialog closes and a [Toast](http://developer.android.com/reference/android/widget/Toast.html) with a default message is presented.

![Freddie]({{ "/images/freddie.jpg" | prepend: site.baseurl }})

### How did it end
Right after finishing I thought "Wouldn't be great if the konami code could be injected into other's people apps?". So, I wrapped up everything in a class with a [builder pattern](https://en.wikipedia.org/wiki/Builder_pattern), I added some methods to let developers customize a thing or two and then...a nerdy library was born \o/

<center><iframe width="420" height="315" src="https://www.youtube.com/embed/vIRdoI-V-Pk" frameborder="0" allowfullscreen></iframe></center>

Now developers can easily add this awesome easter-egg into their apps. The instructions are in [this Github repository](https://github.com/thiagokimo/KonamiCode).

Cheers!
