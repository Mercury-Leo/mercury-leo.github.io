---
title: "Another way to get a component"
excerpt_separator: "<!--more-->"
categories:
- Teaching
tags:
- Unity
- Tips
- Component
---

When trying to get a component in a script, we mainly use `GetComponent<T>` to find that component. So what does
GetComponent actually do? It cycles on the object components and returns the first one that matches the given type T
that is found. If the method doesn’t find it, it will return a special null object Unity uses to track errors and other
things. Which means it doesn’t actually return a null. This causes some allocation, only in editor, that can be avoided.
By using `TryGetComponent<T>` we can eliminate the editor allocation.
TryGetComponent works the same as the normal GetComponent but will not allocate in the editor when a component doesn't
exist.

### Different uses:

1. Declaring a variable allows to not express which type is being searched for.

```c#
private Image _image;

private void Awake()
{
	TryGetComponent(out _image);
}
```

2. When not declaring a variable, the type T that is searched for, must be expressed.

```C#
private void Awake()
{
	TryGetComponent<TMP_Text>(out var _text);
}

// Or

private void Awake()
{
	TryGetComponent(out TMP_Text _text);
}
```

3. Can be used to check if the search was successful and perform some logic on that.

```C#
private void Awake()
{
	if(TryGetComponent<Image>(out var _image))
	{
		// Some Logic
	}
}
```

Available from Unity version: 2019.2

For further reading:

[TryGetComponent](https://docs.unity3d.com/ScriptReference/Component.TryGetComponent.html)