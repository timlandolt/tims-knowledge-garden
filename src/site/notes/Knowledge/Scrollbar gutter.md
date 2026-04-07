---
{"dg-publish":true,"permalink":"/knowledge/scrollbar-gutter/","tags":["webdevelopement","css"]}
---

---

When no scrollbar is present, it adds a gutter (like a padding). This prevents tha layout from shifting.

```css
html {
  scrollbar-gutter: stable;
  
  /* also adds it to the other edge*/
  scrollbar-gutter: stable both-edges;
}
```

