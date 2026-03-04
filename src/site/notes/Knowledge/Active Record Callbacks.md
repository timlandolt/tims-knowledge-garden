---
{"dg-publish":true,"permalink":"/knowledge/active-record-callbacks/","tags":["active-record","ruby","ruby-on-rails"]}
---


---

## Registering a Callback
### Macro-style class method

```rb
class User < ApplicationRecord
  validates :username, :email, presence: true

  before_validation :ensure_username_has_value

  private
    def ensure_username_has_value
      if username.blank?
        self.username = email
      end
    end
end
```

or

```rb
class User < ApplicationRecord
  validates :username, :email, presence: true

  before_validation do
    self.username = email if username.blank?
  end
end
```

### Pass in a Proc

```rb
class User < ApplicationRecord
  validates :username, :email, presence: true

  before_validation ->(user) { user.username = user.email if user.username.blank? }
end
```

### Custom callback Object

```rb
class User < ApplicationRecord
  validates :username, :email, presence: true

  before_validation AddUsername
end

class AddUsername
  def self.before_validation(record)
    if record.username.blank?
      record.username = record.email
    end
  end
end
```

### Register callback on Lifecycle events

```rb
before_validation :ensure_username_has_value, on: :create
```

see also [[Knowledge/test/Active Record Validations#On\|Knowledge/test/Active Record Validations#On]] 

## Available Callbacks
### Triggered when Creating an Object
```rb
before_validation
after_validation
before_save
around_save
before_create
around_create
after_create
after_save
after_commit / after_rollback
```

### Triggered when Updating an Object
```rb
before_validation
after_validation
before_save
around_save
before_update
around_update
after_update
after_save
after_commit / after_rollback
```

### Triggered when Destroying an Object

```rb
before_destroy
around_destroy
after_destroy
after_commit / after_rollback
```

### Others
```rb
after_initialize
after_find
after_touch
```

## Conditional Callbacks
Like in [[Knowledge/test/Active Record Validations#Conditional Validations\|validations]] you can add conditions to your callbacks.

```rb
before_save :normalize_card_number, if: :paid_with_card?

before_save :normalize_card_number,
    if: ->(order) { order.paid_with_card? }
    
before_save :normalize_card_number, if: -> { paid_with_card? }
```

## Association Callbacks

Triggered by associations

```rb
before_add
after_add
before_remove
after_remove
```

```rb
class Author < ApplicationRecord
  has_many :books, before_add: :check_limit

  private
    def check_limit(_book)
      if books.count >= 5
        errors.add(:base, "Cannot add more than 5 books for this author")
        throw(:abort)
      end
    end
end
```

## Transaction Callbacks

```rb
class PictureFile < ApplicationRecord
  after_commit :delete_picture_file_from_disk, on: :destroy

  def delete_picture_file_from_disk
    if File.exist?(filepath)
      File.delete(filepath)
    end
  end
end
```

In This example the physical file associated with the model only gets removed after the successful destruction of the object.

### Aliases for specific commits

```rb
after_destroy_commit
after_create_commit
after_update_commit
after_save_commit
```

then you can leave out the `on:`