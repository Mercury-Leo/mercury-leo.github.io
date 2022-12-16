---
title: "Life Cycle"
excerpt_separator: "<!--more-->"
categories:
    - Teaching
tags:
  - Unity
  - Life Cycle

---

# Unity Life Cycle - Initialization

When using a MonoBehaviour script, there are three possible methods: Awake, OnEnable and Start. It's important to
distinguish between them and to know what works best for each case.

### Definitions:

From the Unity documentation: “Awake is called when the script instance is being loaded” which means that Awake is
called either whenever a Gameobject that contains the script is loaded in a scene, a previously inactive Gameobject is
set to active or when a GameObject is created. It’s also important to note that all the active scripts will call their
Awake function before anything else happens.

From the Unity documentation: “Start is called on the frame when a script is enabled just before any of the Update
methods are called the first time” which means Start will be called once a script is enabled, before the Update method
is called and after Awake has been called.

OnEnable is called when the script or the object holding it becomes enabled and active. OnEnable may be called any
number of times. OnEnable will be called after the awake function and before the start function.

These functions are called in the following order: Awake -> OnEnable -> Start

### Usage:

Awake and Start are both called once in the script's lifetime, OnEnable will be called whenever the script is enabled.

This means both Awake & Start are most suited for the script’s initialization. The question is what to initialize and
when.

Awake should be used to initialize appropriate elements that belong to the script itself and not another script. For
example, using GetComponent and initializing other in-script variables. This is useful because as defined earlier, Awake
is called for all scripts before the first Start function is called. Let’s say you have a script A that has a reference
to an Image component, and calls GetComponent at the Start function. Now script B wants, for whatever reason, to change
script A’s image color; A’s Image component may not have been referenced yet, which is problematic. But if A’s
GetComponent call was in the Awake function, we can guarantee that the reference to the Image component is made before
any of the other scripts tries to access them.

OnEnable has a different use case than Awake & Start, as it may be called anytime a script is enabled. This makes
OnEnable a prime candidate for subscribing and unsubscribing events and other similar things. For example, let's say
script C has a reference to a Button component, and you now want to add a function to the Button’s onClick method. In
most cases it’s best to register the event on the OnEnable function and unregister on the OnDisable, which is the same
as OnEnable but is called when a script is disabled. This makes sure your listeners are only active while the script is
enabled, and also a good way to prevent memory leaks.

* Of course there is nothing wrong with subscribing to events at Awake/Start and unsubscribing at OnDestroy, there are
  different use cases when it's better to use them but it's outside of the scope of this document.

I would also like to mention that when using Scriptable Objects, the flow is quite different for Awake and OnEnable, and
there's no Start function. Yet this is a huge subject I would get into in a different post.

For further reading:

Awake - [https://docs.unity3d.com/ScriptReference/MonoBehaviour.Awake.html](https://docs.unity3d.com/ScriptReference/MonoBehaviour.Awake.html)

Start - [https://docs.unity3d.com/ScriptReference/MonoBehaviour.Start.html](https://docs.unity3d.com/ScriptReference/MonoBehaviour.Start.html)

OnEnable - [https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnEnable.html](https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnEnable.html)

ExecutionOrder - [https://docs.unity3d.com/Manual/ExecutionOrder.html](https://docs.unity3d.com/Manual/ExecutionOrder.html)