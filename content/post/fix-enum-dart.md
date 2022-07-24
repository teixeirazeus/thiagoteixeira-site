+++
title = "Fixing dart enumeration"
author = "Thiago S. Teixeira"
date = "2022-07-23"
description = "Enumeration of the dart as it should be."
tags = [
    "dart",
    "enumeration",
    "clean code",
]
+++

Dart is a programming language with a simple syntax and an object-oriented programming structure.
I like the syntax of dart, some things remind me of python and js, which makes me happy.
However, enumeration is different.

Suppose you need to enumerate a status of a purchase order.
In dart, you can do this as:

```dart
enum Status {
    PENDING,
    APPROVED,
    REJECTED,
}
```

Now, you want to print these statuses on the console.

```dart
print(Status.PENDING);
print(Status.APPROVED);
print(Status.REJECTED);
```

And that's the result:

```
Status.PENDING
Status.APPROVED
Status.REJECTED
```

It comes with the name of the status, not the value.
Now you can split the string, using the dot as a separator. Or use a map, to map the value to the name.
Which doesn't look so good.

```dart
print(Status.PENDING.toString().split(".").last);
print(Status.APPROVED.toString().split(".").last);
print(Status.REJECTED.toString().split(".").last);
```

Ideally, you should put a .value, to access the value. This is how it works in python.

For this, you need to create an extended method for the enum.

```dart
extension StatusExtension on Status {
  String get value => this.toString().split(".").last;
}
```

It still has the split, but now it can be accessed by .value.

```dart
print(Status.PENDING.value);
print(Status.APPROVED.value);
print(Status.REJECTED.value);
```

Result:

```
PENDING
APPROVED
REJECTED
```

Clean code.