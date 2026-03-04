---
{"dg-publish":true,"permalink":"/knowledge/active-record-validations/","tags":["active-record","ruby","ruby-on-rails"]}
---

---
Is a part of [[Knowledge/Active Record\|Active Record]]

## Saving model in DB
 ```ruby
 m.new_record? # => true (it isn,t yet saved in the db)
 m.persisted? # => false (counterpart of the above)
 
 m.save # VALIDATES and saves model 
 ```

## Methods that trigger validations

```ruby
m.valid?
m.invalid?

create # => the object to be created (if invalid it doesn't get saved)
create! # => exception (if invalid)
save # => false (if invalid)
save! # => exception (if invalid)
update # => false (if invalid)
update! # => exception (if invalid)
```

>[!error] All other don't validate

## Validations

```ruby
validate :name, presence: true

# absence; phone_number and address must be empty if they are invited
validates :phone_number, :address, absence: true, if: :invited?

# validates checkboxes
validates :terms_of_service, acceptance: true

# checks if email matches email_confirmation (automatically creates virtual; attribute)
validates :email, confirmation: true # this alone wouldn't be enough because it would only check if it is not nil
validates :email_confirmation, presence: true, if: :email_changed?
```

### Comparisons

```ruby
class Promotion < ApplicationRecord
  validates :end_date, comparison: { greater_than: :start_date }
end
```

| Options                     |
| --------------------------- |
| `:greater_than`             |
| `:greater_than_or_equal_to` |
| `:equal_to`                 |
| `:less_than`                |
| `:less_than_or_equal_to`    |
| `:other_than`               |
### Format (regex)
```ruby
class Product < ApplicationRecord
  validates :legacy_code, format: { with: /\A[a-zA-Z]+\z/,
    message: "only allows letters" }
end
```

there is also the counterpart `:without`

### In- and Exclusion

```ruby
class Coffee < ApplicationRecord
  validates :size, inclusion: { in: %w(small medium large),
    message: "%{value} is not a valid size" }
end
```
*see [[Knowledge/Ruby Percent Literals\|Ruby Percent Literals]]*

There is also the counterpart `exclusion`

### Length
```ruby
class Person < ApplicationRecord
  validates :name, length: { minimum: 2 }
  validates :bio, length: { maximum: 500 }
  validates :password, length: { in: 6..20 }
  validates :registration_number, length: { is: 6 }
end
```

### Numericality

```ruby
class Player < ApplicationRecord
  validates :points, numericality: true
  validates :games_played, numericality: { only_integer: true }
end
```

#### Other Options

| Option                      | Description                                                              |
| --------------------------- | ------------------------------------------------------------------------ |
| `:greater_than`             | Specifies the value must be greater than the supplied value.             |
| `:greater_than_or_equal_to` | Specifies the value must be greater than or equal to the supplied value. |
| `:equal_to`                 | Specifies the value must be equal to the supplied value.                 |
| `:less_than`                | Specifies the value must be less than the supplied value.                |
| `:less_than_or_equal_to`    | Specifies the value must be less than or equal to the supplied value.    |
| `:other_than`               | Specifies the value must be other than the supplied value.               |
| `:in`                       | Specifies the value must be in the supplied range.                       |
| `:odd`                      | Specifies the value must be an odd number.                               |
| `:even`                     | Specifies the value must be an even number.                              |
### Uniqueness

```ruby
validates :email, uniqueness: true
```

There can only be one entry in the database with this value. There are also scopes and conditions.

### Validate Associations

``` ruby
has_many :books
validates_associated :books
```

here the associations also get validated

### Custom validations
``` ruby
class Person < ApplicationRecord
  validates_each :name, :surname do |record, attr, value|
    record.errors.add(attr, "must start with upper case") if /\A[[:lower:]]/.match?(value)
  end
end
```

#### Inside another class

```rb
class AddressValidator < ActiveModel::Validator
  def validate(record)
    if record.house_number.blank?
      record.errors.add :house_number, "is required"
    end

    if record.street.blank?
      record.errors.add :street, "is required"
    end

    if record.postcode.blank?
      record.errors.add :postcode, "is required"
    end
  end
end

class Invoice < ApplicationRecord
  validates_with AddressValidator
end
```

## Validation Options

```rb
validates :x, presence: true, allow_nil: true # obvious
validates :x, presence: true, allow_blank: true # same, but also "", etc.
validates :x, presence: { message: "%{attribute} in %{model}` cannot be %{value}" } # custom error message
```

### On

```rb
# it will be possible to update email with a duplicated value
validates :email, uniqueness: true, on: :create

# it will be possible to create the record with a non-numerical age
validates :age, numericality: true, on: :update

# the default (validates on both create and update)
validates :name, presence: true
```

## Conditional Validations

There are also the options `:if` and `:unless`.

```rb
class Order < ApplicationRecord
  validates :card_number, presence: true, if: :paid_with_card?

  def paid_with_card?
    payment_type == "card"
  end
end
```

You can also use procs or lambdas:

```rb
validates :password, confirmation: true, unless: -> { password.blank? }
```

### Group Conditional Validations

```rb
class User < ApplicationRecord
  with_options if: :is_admin? do |admin|
    admin.validates :password, length: { minimum: 10 }
    admin.validates :email, presence: true
  end
end
```

## Strict Validations

This way it always raises an exception 

```rb
validates :name, presence: { strict: true }
```

## Errors

```rb
person = Person.new
person.valid? # => false
person.errors.full_messages # => ["Name can't be blank", "Name is too short (minimum is 3 characters)"]

person.errors[:name] # same

person.errors.where(:name, :too_short) # => [...]
```

### Error Objects

```rb
error = person.errors.where(:name).last

error.attribute # => :name
error.type # => :too_short
error.options[:count] # => 3

error.message # => "is too short (minimum is 3 characters)"
error.full_message # => "Name is too short (minimum is 3 characters)" (more readable)
```
