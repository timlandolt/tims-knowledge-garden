---
{"dg-publish":true,"permalink":"/knowledge/dependency-inversion-principle/","tags":["solid-principles"]}
---

---

D in the SOLID Principles.

1. High-level modules should not import anything from low-level modules. Both should depend on abstractions (e.g., interfaces).
2. Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.

## Example
> (c) Felix Stadelmann, original in C++

### Bad

```java
class DoorBell {
    void ring() {
        // Ringing logic
    }
}

class Button {
    DoorBell bell = new DoorBell();

    void press() {
        bell.ring();
    }
}
```

### Good

```java
// Abstraction
interface ButtonListener {
    void onButtonPress();
}

// High-Level Module
class Door {
    private final ButtonListener listener;

    public Door(ButtonListener listener) {
        this.listener = listener;
    }

    public void open() {
        listener.onButtonPress();
    }
}

// Low-Level Module
class DoorBell implements ButtonListener {
    @Override
    public void onButtonPress() {
        // Doorbell logic
    }
}

```
