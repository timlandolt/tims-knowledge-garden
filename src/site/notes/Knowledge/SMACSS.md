---
{"dg-publish":true,"permalink":"/knowledge/smacss/","tags":["smacss","css"]}
---

---

> [!info] **SMACSS** = **S**calable and **M**odular **A**rchitecture for **CSS**

SMACSS categorizes the [[Knowledge/CSS\|CSS]] styles in 5 categories:

1. base
2. layout
3. module
4. state
5. theme

These can be separate files or folders.

## Base

For [[Knowledge/HTML\|HTML]] tags like `body`, `a`, `a:hover`, etc. It also includes the reset CSS.

```css
body, form { margin: 0; padding: 0; }
a { color: #039; }
a:hover { color: #03F;     }
```

## Layout

The main layout elements.
Reusable classes use the `l-` prefix.

```css
#article { width: 80%; float: left; }
#sidebar { width: 20%; float: right; } 
.l-fixed #article { width: 600px; } 
.l-fixed #sidebar { width: 200px; }
```

## Module

Reusable blocks.

```css
.module { padding: 10px }
.module .title { color: red; }
.module .description { width: 200px; }
```

## State

State describes how the appearance changes in different situations. These classes are applied by [[Knowledge/JavaScript\|JS]] in most cases.
State classes are prefixed with `is-`

```css
.is-error{  border: 1px solid red;}
.is-active{ border: 2px solid green;}
```

## Theme

Describes the colours, shapes, borders, shadows, etc. 
Base is only meant for the default appearance.
The goal of the separation of theming styles it that now it's easy to completely change the theming styles. It also opens the possibility to provide multiple different themes.

```css
/* in modules.css */
.mod {  border: 1px solid;}
/* in theme.css */
.mod {border-color: blue;}
```

