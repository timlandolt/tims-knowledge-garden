---
{"dg-publish":true,"permalink":"/knowledge/java-script-prototypes/","tags":["javascript","webdevelopement"]}
---

---

From Greek:
- **prōto-** = “first”
- **typos** = “impression, model, pattern, or stamp”

Prototypes are the way inheritance is handled in JavaScript. Every JS Object has a prototype. The prototype again is also set to an Object. => Prototype Chain
The chain ends when a prototype is set to null.

```mermaid
graph LR

A["const nums = [1, 2, 3]"]:::main
A-->|.\_\_proto__|B[Array]
B-->|.\_\_proto__|C[Object]
C-->|.\_\_proto__|D[null]
```

