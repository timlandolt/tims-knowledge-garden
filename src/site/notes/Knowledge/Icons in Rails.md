---
{"dg-publish":true,"permalink":"/knowledge/icons-in-rails/","tags":["ruby-on-rails"]}
---

---

While working on the redesign of the SwissICT Salärstudie I came across the challenge of adding the icons used in the [[figma\|figma]] design into the project. I've looked through various projects of ours to see how Icons usually get implemented. It turns out, that there is no such thing as the "normal" way of adding icons. Here are some of the options I found or came up with:

- Adding them as images
- Setting them as background images of pseudo-elements
- Font Awesome
- Glyphicons
- Google icons/symbol (the intended way)
- Google icons/symbols (the better way)

## Adding them as images

-  - Many files, hard to structure well (in my case there were different weights and sizes)
-  - To customize (without filter workaround) you need inline SVG => [Inline SVG Gem](https://github.com/jamesmartin/inline_svg)
- + Files can be customized
- + nice accessibility

## Setting them as background images of pseudo-elements

- + Icons can easily be added with classes
-  - Basically no customizability

## Font Awesome

- Didnt look into it, because required icons were google symbols

## Glyphicons

- Didnt look into it, because required icons were google symbols

## Google icons/symbol (the intended way)

Include the google material icons (or symbols for more customizability) using the cdn link. Then either enter the Unicode codepoint or write the icon name inside an element with a specific class: [Material Symbols guide  \|  Google Fonts  \|  Google for Developers](https://developers.google.com/fonts/docs/material_symbols)

- + Easy to load over CDN
-  - Google gets data

## Google icons/symbols (the better way)

First download the Font from the [material symbols Github repo](https://github.com/google/material-design-icons)
Then write a helper, that inserts the material symbols codepoints. For further customization, use CSS classes:

```scss
// _material_symbol.scss

.material-symbol {  
  display: inline-block;  
  width: 1em;  
  height: 1em;  
  
  font-family: "Material Symbols Outlined", sans-serif;  
  font-size: $icon-md;  
  line-height: 1;  
  font-style: normal;  
  font-variation-settings: 'wght' 200, 'opsz' $icon-md;  
  
  &.is-small {  
    font-size: $icon-sm;  
    font-variation-settings: 'wght' 300, 'opsz' $icon-sm;  
  }  
  
  &.has-fill {  
    font-variation-settings: 'FILL' 1;  
  }  
}
```

```rb
# application_helper.rb

module ApplicationHelper
	ICON_CODE_POINTS = {  
	  check: "\ue5ca", close: "\ue5cd", delete: "\ue872", edit: "\ue3c9"
	}.freeze  
  
	def icon(name, config = {class: ""})  
	  class_name = class_names(config[:class], "material-symbol")  
	  tag.i ICON_CODE_POINTS[name], "aria-hidden": true, class: class_name  
	end
end
```

```html.erb
# example.html.erb
<%= icon :close %>
<%= icon :delete, class_name: "is-small has-fill" %>
```

This approach has the problem that the whole font has to be loaded...

### Using pseudo-elements

It is also quite nice to set the icons in pseudo-elements based on the class, so all the frontend stuff stays completely in the views/css (and also if you want to use it in plain html projects).

```html
<!--index.html-->

<i class="icon icon-edit"></i>
```

- + In theory nice because it can be applied using classes only
-  - Many icons would lead to many variables/classes for all the different icons