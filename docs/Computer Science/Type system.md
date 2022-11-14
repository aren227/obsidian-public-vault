---
title: Type system
author: aren227
date: 2022-10-28T21:36:34+09:00
lastmod: 2022-11-14T01:19:24+09:00
tags:
- computer-science
---

## Strong vs weak typing
> [!todo]

## Static vs dynamic type checking
Static type checking is the process of verifying the type safety of a program with its source code, whereas dynamic type checking does at runtime. Static type checking can be seen as an optimization because it reduces various type safety checking at runtime.
Still, many languages do both static and dynamic type checking. For example, [[Java]] is statically-typed language but every objects still have runtime type information (RTTI). This is useful when we try to downcast a object. Suppose `Dog` and `Cat` is a subclass of `Animal`.

```java
Animal animal;
// A condition we can't know at compile time.
if (condition) {
	animal = new Dog();
}
else {
	animal = new Cat();
}
...
Dog dog = (Dog) animal;
```

This will work if the condition is true. Becuase the object in `animal` is actually a instance of the class `Dog`. What will happen if the condition is false? Well, it will throw `ClassCastException`. Obviously you can't cast a `Cat` object to a `Dog`. These type checking are done at runtime, so Java does dynamic type checking also.

>[!note]
> You can use `instanceof` operator to make the above example safe.

## Structural vs duck typing
> [!todo]
