---
{"dg-publish":true,"permalink":"/knowledge/one-way-data-binding/","tags":["webdevelopement","react","angular","vue"]}
---

---

**React Example**
```jsx
import React from 'react';

function App() {
  const [count, setCount] = React.useState(0);

  return (
    <>
      <input value={count} />
      
      <button
        onClick={() => setCount(count + 1)}
      >
        Increment
      </button>
    </>
  );
}
```

**Angular Example**
```js
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  standalone: true,
  template: `
    <button (click)="increment()">
      Increment
    </button>

    <p>Count is: {{ count }}</p>
  `,
})
export class AppComponent {
  count = 0;

  increment() {
    this.count++;
  }
}
```

**Vue example**
```vue
<script setup>
import { ref } from 'vue';

const count = ref(0);

function increment() {
  count.value++;
}
</script>

<template>
  <button @click="increment">Increment</button>
  <p>Count is: {{ count }}</p>
</template>
```

To also get user input, [[Knowledge/Two-Way Data Binding\|two-way data binding]] is required.