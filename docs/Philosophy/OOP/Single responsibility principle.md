---
title: Single responsibility principle
author: aren227
date: 2022-11-11T22:09:05+09:00
lastmod: 2022-11-14T01:19:46+09:00
tags:
- solid
- object-oriented-programming
- software-development-philosophy
---

Single responsibility principle imples "A class should have only one reason to change".
If a class has more than one responsibility, then the responsibilities become coupled. Breaking them into multiple classes could make you to think about more flexible code structure.

I personally think 'one responsibility' is quite ambiguous. Too many things being handled in a single class is a generally bad idea if you consider flexibility, But spreading micro-sized classes all over the place could be a bad idea too. Martin also noted that the SRP should be applied only if two responsibilities changed at different times. Otherwise it will increase needless complexity.

## Example
This example was taken from 'Agile Software Development' by Robert C. Martin.

![[Pasted image 20221112003204.png]]

The `Rectangle` class violates the SRP. It has two responsibilities.
- Providing a mathematical model of the geometry.
- Rendering the geometry to a GUI.

Since the `Computational Geometry Application` has nothing to do with `GUI`, the unncessary dependency was created. If we only changed the rendering logic of the `Rectangle` class, the change might impact the `Computational Geometry Application` in some ways.
According to the SRP, we can separate responsibilities like this.

![[Pasted image 20221112003232.png]]
