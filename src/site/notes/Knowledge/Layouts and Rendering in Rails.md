---
{"dg-publish":true,"permalink":"/knowledge/layouts-and-rendering-in-rails/","tags":["ruby-on-rails","ruby"]}
---

---

## Sending Responses
### `render`
The Controller returns the corresponding view automatically if it is named right. Alternatively you can use `render` to render a different view.

```rb
def update
  @book = Book.find(params[:id])
  if @book.update(book_params)
    redirect_to(@book)
  else
    render :edit, status: :unprocessable_entity
  end
end
```

If the view belongs to a different controller you need to specify it:

```rb
render "products/show"
```

You can also render not-views:

```rb
render inline: "<% products.each do |p| %><p><%= p.name %></p><% end %>"
render plain: "OK"
render html: helpers.tag.strong("Not Found")
render json: @product
render xml: @product
render js: "alert('Hello Rails');"
render body: "raw"
render file: "#{Rails.root}/public/404.html", layout: false
```

#### Options for `render`

```rb
# content type
render template: "feed", content_type: "application/rss"

# different layout
render layout: "special_layout"
render layout: false

# location (redirect)
render xml: photo, location: photo_url(photo)

# set status
render status: 500
render status: :forbidden

# specify format
render formats: :xml
render formats: [:json, :xml]

# Render a specific variant
render variants: [:mobile, :desktop]
# app/views/home/index.html+mobile.erb
# app/views/home/index.html+desktop.erb
```

#### Using Layouts
[[Knowledge/Ruby on Rails\|Rails]] automatically checks if there is a layout with the same name as the controller. Else it falls back to the `application.html.erb`. You can also set it manually.

```rb
class ProductsController < ApplicationController
  layout "inventory"
  #...
end
```


### `redirect_to`

If you want the browser to make a completely new request, you can use `redirect_to`

```rb
redirect_to photos_url

# there's also redirect back
redirect_back(fallback_location: root_path)
# some browsers need the fallback location
```

### Header-Only Responses

```rb
head :bad_request

# or use some options:
head :created, location: photo_path(@photo)
```

