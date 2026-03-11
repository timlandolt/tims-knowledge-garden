---
{"dg-publish":true,"permalink":"/knowledge/variable-fonts/","tags":["webdevelopement","design","css","fonts"]}
---

---

## Formats
Variable fonts are available for TrueType (.ttf), OpenType (.otf) and Web Open Font Format (.woff2).
Most variable fonts come in TrueType, but for Web, the woff2 format is preferred, as it is much smaller. Variable fonts can become quite large.

## Loading Variable Fonts in CSS

```css
@font-face {  
  font-family: "My-Font";  
  src: url("My-Font.woff2") format("woff2 supports variations"),  
       url("My-Font.woff2") format("woff2-variations"),  
       url("My-Font.ttf")   format("truetype-variations");  
  font-weight: 100 900;  
  font-style: normal;  
}
```
