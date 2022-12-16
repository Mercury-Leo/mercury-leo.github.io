---
title: "Humble Object Pattern"
excerpt_separator: "<!--more-->"
categories:
  - Teaching  
tags:
  - Unity
  - Tips
  - Pattern

---

### Definition

The Humble Object pattern as stated in book 'Clean Architecture: A Craftsman's Guide to Software Structure and Design'
By Robert Martin states: "The Humble Object pattern is a design pattern that was originally identified as a way to help
unit testers to separate behaviors that are hard to test from behaviors that are easy to test.". This means, in order to
make your code more testable, it's good practice to decouple business logic as much as possible and by so it's easier to
test that business logic.
For example, Let's say we have a class that represents an ATM, and calculates the balance when money is deposited or
withdrawn, and also, presents that data in some sort of UI. What we should do to refactor this, is extract the balance
logic into a different class and have the UI present the data and nothing else, and by so the UI becomes the humble
object. And the logic for calculating the balance becomes a pure C# class and will be much easier to test.

### Usage

For Unity, there are more considerations to be made.
When just starting to learn Unity, we tend to overuse MonobBehaviors. Which is fine for learning and small projects, but
MonoBehaviors are costly, here the Humble Object pattern works wonders.
We want to keep our MonoBehaviors as humble as possible, have them do only the minimum required of them. Having all of
the business logic in pure C# classes and let our MonoBehaviors present that data.
This approach is also good for lightening the load off Unity, by having less heavy MonoBehaviors run, and have more pure
C# classes do the bulk of the work.

Of course, there are places where we can't separate some of the logic in cases of Coroutines and such, but we must
strive to use the Humble Object pattern as much as possible.