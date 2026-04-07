---
{"dg-publish":true,"permalink":"/knowledge/css-media-queries/","tags":["webdevelopement","css","media-queries"]}
---

---

## Basic usage of [[Knowledge/CSS\|CSS]] Media Queries

```css
@media only screen and (max-width: 600px) {
  body {
    background-color: lightblue;
  }
}
```

## Typical Device Breakpoints

```css
/* Extra small devices (phones, 600px and down) */  
@media only screen and (max-width: 600px) {...}  
  
/* Small devices (portrait tablets and large phones, 600px and up) */  
@media only screen and (min-width: 600px) {...}  
  
/* Medium devices (landscape tablets, 768px and up) */  
@media only screen and (min-width: 768px) {...}  
  
/* Large devices (laptops/desktops, 992px and up) */  
@media only screen and (min-width: 992px) {...}  
  
/* Extra large devices (large laptops and desktops, 1200px and up) */  
@media only screen and (min-width: 1200px) {...}
```

## Orientation: Portrait / Landscape

```css
@media only screen and (orientation: landscape) {
  body {
    background-color: lightblue;
  }
}
```