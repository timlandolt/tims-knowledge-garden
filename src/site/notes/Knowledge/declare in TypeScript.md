---
{"dg-publish":true,"permalink":"/knowledge/declare-in-type-script/","tags":["webdevelopement","typescript"]}
---

---

```ts
declare const someVariable: any
```

`declare` in [[Knowledge/TypeScript\|TypeScript]] is used to tell the compiler that a variable already exists and can be referenced.
It is not compiled to any [[Knowledge/JavaScript\|JavaScript]].

For example, when an object is created by a script that is loaded externally. If it now isn't explicitly `declare`d, the compiler won't be happy.
