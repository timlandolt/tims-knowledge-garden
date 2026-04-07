---
{"dg-publish":true,"permalink":"/knowledge/rails-asset-pipeline/","tags":["rails-asset-pipeline","ruby-on-rails"]}
---

---

=> library for organizing, caching, and serving static assets like images, [[Knowledge/JavaScript\|JavaScript]] or [[Knowledge/CSS\|CSS]] in [[Knowledge/Ruby on Rails\|Ruby on Rails]]

> [!info] Since rails 8, Propshaft is the default asset pipeline for rails. Before it was Sprockets

## Asset organization

- app
	- assets
		- images
		- javascripts
		- stylesheets

### Add additional asset paths

```rb
# config/initializers/assets.rb

Rails.application.config.assets.paths << Emoji.images_path
```

## Loading Assets

### Inside Templates

```erb
<!-- application.html.erb -->
<head>
 <%= stylesheet_link_tag "reset" %>
 <%= stylesheet_link_tag "base" %>
 <%= stylesheet_link_tag "main" %>
</head>
<body>
 <%= javascript_include_tag "utilities" %>
 <%= javascript_include_tag "main" %>
</body>
```

### With JavaScript (ES6) Modules

```js
// main.js
import { initUtilities } from "./utilities.js";
import { setupFeature } from "./feature.js";

initUtilities();
setupFeature();
```

```html
<script type="module" src="main.js"></script>
```

## Fingerprinting

Propshaft appends a digest of the file contents to the filenames so when the content changes, the files get new names. This allows to circumvent many bugs related to caching.

The filenames get mapped inside the `public/assets/.manifest.json`

```json
{
  "application.css": "application-6d58c9e6e3b5d4a7c9a8e3.css",
  "application.js": "application-2d4b9f6c5a7c8e2b8d9e6.js",
  "logo.png": "logo-f3e8c9b2a6e5d4c8.png",
  "favicon.ico": "favicon-d6c8e5a9f3b2c7.ico"
}
```

This allows us to access the files easily:
```erb
<%# application.erb %>

<%= stylesheet_link_tag "application", media: "all" %>
<%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
<%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
<%= image_tag "icons/rails.png" %>
```

```css
/*application.css*/

background: url("/bg/pattern.svg");
```

>[!warning] Attention!
>In JavaScript you have to manually trigger the asset transformation
>```js
>export default class extends Controller {
>  init() {
>    this.img = RAILS_ASSET_URL("/icons/trash.svg");
>  }
>}
>```

## Configure CDN

```rb
# config/environments/production.rb

config.asset_host = "mycdnsubdomain.fictional-cdn.com"
config.asset_host = ENV["CDN_HOST"]
```