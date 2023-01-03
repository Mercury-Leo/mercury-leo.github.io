---
title: "What is Require Component"
excerpt_separator: "<!--more-->"
categories:
    - Teaching
tags:
  - Unity
  - Tips
  - Attribute
---

When creating scripts, they may use a lot of different components, and we would want to check that those components are
attached before we perform any actions on them. And in other cases we have scripts that rely heavily on other
components, that when we attach that script to a gameobject we would need to add all the components we need as well.
This process can break the flow of creating and in general be cumbersome.
Unity has a very simple attribute that can save a lot of time:
`'RequireComponent'`

`[RequireComponent(typeof(someType))]`

Require Component is an attribute that automatically adds components as dependencies.
What does that mean? We can decide what components are required for our script, and this has two major advantages:

1. Any required component will be added automatically to the game object. And it can not be removed as long as the
   script is attached to the game object.
2. It promises us that the component is on the game object.

Unity will also block any attempts to remove the component while the 'RequireComponent' is still there.

For further reading:

[RequireComponent](https://docs.unity3d.com/ScriptReference/RequireComponent.html)
