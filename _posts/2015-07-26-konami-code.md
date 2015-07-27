---
layout: post
title: "Konami Code Installer"
date: 2015-07-26 23:01
summary: Adding our favorite easter-egg in any Android app.
---

Few days ago I was wondering how does an easter-egg like the **Konami Code** in Google Play Games works. Since Google Play Games is not open-source I had no option but trying to reproduce it by myself.

<center><iframe width="420" height="315" src="https://www.youtube.com/embed/59xCH_1CAPc" frameborder="0" allowfullscreen></iframe></center>

Before start any kind of hack I like to write down what would I think will be the main important/challenging topics to accomplish my goals. I came up with the following points:

- Detecting swipe gestures
- Registering a sequence of swipes
- Showing the keyboard dialog
- Registering a sequence of pressed buttons
- Showing a final message to the user

With those points in mind I've divided the Konami Code into 2 parts: The **Directional Part**, which is the moment where the user executes the *UP, UP, DOWN, DOWN, LEFT, RIGHT, LEFT and RIGHT* sequence; and the **Buttons Part**, which is the moment where the user presses the *B, A and START* buttons. Let's hack!

### The Directional Part
To detect swipe gestures I've created a [SimpleOnGestureListener](http://developer.android.com/reference/android/view/GestureDetector.SimpleOnGestureListener.html), implementing the **onFling** method. The gesture listener stores any swipe done by the user and it checks if the last added swipe is following the correct sequence of the Konami Code. If the sequence is incorrect, all swipes stored are cleared and the user must begin swiping the code from the begining. When the code is finished, a dialog shows up with the buttons necessary to execute the second part of the code.

### The Buttons Part
This was the easiest part. A custom [AlertDialog](http://developer.android.com/reference/android/app/AlertDialog.html) with the buttons representing the keys **A**, **B** and **START** inside it. The same principle of the *Directional Part* was done here: The order of the pressed buttons were stored. Whenever the order gets wrong the dialog closes and the user must beging the whole Konami Code again. When the buttons are pressed in the correct order, the dialog closes and a [Toast](http://developer.android.com/reference/android/widget/Toast.html) with a default message is shown.

![Freddie]({{ "/images/freddie.jpg" | prepend: site.baseurl }})

### How did it end
Right after finishing I thought "Wouldn't be great if the konami code could be injected into other's people apps?". So, I wrapped up everything in a class with a [builder pattern](https://en.wikipedia.org/wiki/Builder_pattern), I added some methods to let developers customize a thing or two and then...a nerdy library was born \o/

Now developers can easily add this aswesome easter-egg into their apps. The instructions are in [this Github repository](https://github.com/thiagokimo/KonamiCode).

Cheers!
