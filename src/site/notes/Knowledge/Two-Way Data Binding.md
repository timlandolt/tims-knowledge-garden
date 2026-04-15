---
{"dg-publish":true,"permalink":"/knowledge/two-way-data-binding/","tags":["webdevelopement","react","angular","vue"]}
---

---

When data binding is two-way => User inputs
In contrary: [[Knowledge/One-Way Data Binding\|One-Way Data Binding]]

**React example**
```jsx
import React, { useState } from 'react';

function App() {
  const [val, setVal] = useState('');

  const handleChange = (event) => {
    setVal(event.target.value);
  };

  return (
    <div>
      Enter the value: 
      <input 
        type="text" 
        value={val}
        onChange={handleChange}
      />
      <br />
      Entered value is: {val}
    </div>
  );
}
```

**Angular example**
```js
import { Component } from '@angular/core'; 
 
 @Component({ 
   selector: 'app-example', 
   template: ` 
               Enter the value  : <input [(ngModel)] ='val'> 
               <br> 
                Entered value is:  {{val}} 
             ` 
}) 
export class AppComponent { 
   val: string = ''; 
}
```

**Vue example**
```vue
<script setup>
import { ref } from 'vue'

const val = ref('')
</script>

<template>
  <div>
    Enter the value: <input v-model="val" />
    <br />
    Entered value is: {{ val }}
  </div>
</template>
```

### Why is it different?
React follows the “Controlled Component” pattern. This means you link the value to a state and have to update the state using an event handler.