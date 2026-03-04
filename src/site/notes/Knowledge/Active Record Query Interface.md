---
{"dg-publish":true,"permalink":"/knowledge/active-record-query-interface/","tags":["active-record","ruby-on-rails","ruby"]}
---


---
## Retrieving Objects from DB
### Find

```sql
Customer.find(10)
SELECT * FROM customers WHERE (customers.id = 10) LIMIT 1

Customer.find([1, 10])
SELECT * FROM customers WHERE (customers.id IN (1,10))

customers = Customer.find([3, 17]) -- composite primary key
SELECT * FROM customers WHERE store_id = 3 AND id = 17
```

### Take

```sql
customer = Customer.take
SELECT * FROM customers LIMIT 1

customers = Customer.take(2)
SELECT * FROM customers LIMIT 2
```

### First

```sql
customer = Customer.first
SELECT * FROM customers ORDER BY customers.id ASC LIMIT 1

customers = Customer.first(3)
SELECT * FROM customers ORDER BY customers.id ASC LIMIT 3
```

### Last

```sql
customer = Customer.last
SELECT * FROM customers ORDER BY customers.id DESC LIMIT 1

customers = Customer.last(3)
SELECT * FROM customers ORDER BY customers.id DESC LIMIT 3
```

### Find by

```sql
Customer.find_by first_name: 'Lifo'
SELECT * FROM customers WHERE (customers.first_name = 'Lifo') LIMIT 1
-- same as
Customer.where(first_name: "Lifo").take
```

### Find each

Loads batches of 1'000 entries to save memory.

```rb
Customer.find_each do |customer|
  NewsMailer.weekly(customer).deliver_now
end
```

#### Options for `find_each`
```rb
:batch_size
:start # it is by default ordered by the primary key in ascending order
:finish
:order # :asc or :desc
```

### Find in Batches

Similar to [[Knowledge/test/Active Record Query Interface#Find each\|find_each]] but loads the batch into an array.

```rb
Customer.find_in_batches do |customers|
  export.add_customers(customers)
end
```

#### Options for `find_in_batches`
```rb
:batch_size
:start # it is by default ordered by the primary key in ascending order
:finish
```

## Conditions

```rb
Book.where("title = ? AND out_of_print = ?", params[:title], false)

Book.where("created_at >= :start_date AND created_at <= :end_date", { start_date: params[:start_date], end_date: params[:end_date] })

Book.where("title LIKE ?", Book.sanitize_sql_like(params[:title]) + "%")

```

### Hash Conditions

```rb
Book.where(out_of_print: true)

Book.where([:author_id, :id] => [[15, 1], [15, 2]])

Book.where(created_at: (Time.now.midnight - 1.day)..Time.now.midnight) # range condition

Customer.where(orders_count: [1, 3, 5])
```

### Logical conditions

```rb
Customer.where.not(orders_count: [1, 3, 5]) # NOT

Customer.where(last_name: "Smith").or(Customer.where(orders_count: [1, 3, 5])) # OR

Customer.where(last_name: "Smith").where(orders_count: [1, 3, 5]) # AND
Customer.where(id: [1, 2]).and(Customer.where(id: [2, 3])) # AND

```

## Ordering

```rb
Book.order(:created_at) # orders ascending
Book.order("created_at")



Book.order(created_at: :desc)
Book.order(created_at: :asc)

Book.order("created_at DESC")
Book.order("created_at ASC")

# Multiple fields
Book.order(title: :asc, created_at: :desc)
Book.order(:title, created_at: :desc)

Book.order("title ASC, created_at DESC")
Book.order("title ASC", "created_at DESC")

Book.order("title ASC").order("created_at DESC")
```

## Selecting specific Fields

```rb
Book.select(:isbn, :out_of_print)
Book.select("isbn, out_of_print")

Customer.select(:last_name).distinct
```

## Limit and Offset

```rb
Customer.limit(5)
Customer.limit(5).offset(30)
```

## Grouping

```rb
Order.select("created_at").group("created_at")

Order.group(:status).count
```

### HAVING conditions

>[!info] `HAVING` adds conditions to a group

```rb
big_orders = Order.select("created_at, sum(total) as total_price")
                  .group("created_at")
                  .having("sum(total) > ?", 200)

big_orders[0].total_price
# Returns the total price for the first Order object
```

```sql
SELECT created_at, sum(total) as total_price
FROM orders
GROUP BY created_at
HAVING sum(total) > 200
```

## Readonly Objects

```rb
customer = Customer.readonly.first
customer.visits += 1
customer.save # Raises an ActiveRecord::ReadOnlyRecord
```

### Locking Records
*See also [[School/INFO/223_Multi-User App#5.1 Locking\|223_Multi-User App#5.1 Locking]]*

#### Optimistic Locking
For explaination of the concept look [[School/INFO/223_Multi-User App#5.1.1 Optimistic Locking\|here]].
In Rails Locking works by adding a `lock_version` column with an integer, that gets incremented after every update. To enable locking you just have to add a new column `lock_version` of type integer, Active Record handles the rest.

```rb
c1 = Customer.find(1)
c2 = Customer.find(1)

c1.first_name = "Sandra"
c1.save

c2.first_name = "Michael"
c2.save # Raises an ActiveRecord::StaleObjectError
```

#### Pessimistic Locking

```rb
Book.transaction do
  book = Book.lock.first
  book.title = "Algorithms, second edition"
  book.save!
end
```

##### When there is already an object instance

```rb
book = Book.first
book.with_lock do
  # This block is called within a transaction,
  # book is already locked.
  book.increment!(:views)
end
```

## Joining Tables

```rb
# Raw SQL
Author.joins("INNER JOIN books ON books.author_id = authors.id AND books.out_of_print = FALSE")

Book.joins(:reviews)
# SELECT books.* FROM books
#  INNER JOIN reviews ON reviews.book_id = books.id

Book.joins(:author, :reviews) 
# all books that have an author and at least one review
# SELECT books.* FROM books
#  INNER JOIN authors ON authors.id = books.author_id
#  INNER JOIN reviews ON reviews.book_id = books.id

Book.joins(reviews: :customer)
# all books that have a review by a customer.
# SELECT books.* FROM books
#  INNER JOIN reviews ON reviews.book_id = books.id
#  INNER JOIN customers ON customers.id = reviews.customer_id

Author.joins(books: [{ reviews: { customer: :orders } }, :supplier])
# all authors that have books with reviews and have been ordered by a customer, and the suppliers for those books.
```

### Left outer joins

```rb
Customer.left_outer_joins(:reviews).distinct.select("customers.*, COUNT(reviews.*) AS reviews_count").group("customers.id")
# all customers with their count of reviews, whether or not they have any reviews at all
# SELECT DISTINCT customers.*, COUNT(reviews.*) AS reviews_count FROM customers
# LEFT OUTER JOIN reviews ON reviews.customer_id = customers.id GROUP BY # customers.id

```


## Scopes

```rb
class Book < ApplicationRecord
  scope :out_of_print, -> { where(out_of_print: true) }
end

Book.out_of_print # => #<ActiveRecord::Relation> # all out of print books
```

There is a lot more possible. See: [14. Scopes](https://guides.rubyonrails.org/active_record_querying.html#scopes) and [16. Enums](https://guides.rubyonrails.org/active_record_querying.html#enums)

## Find or Build a New Object

```rb
Customer.find_or_create_by(first_name: 'Andy')
# doesn't get persisted if validations fail

Customer.find_or_create_by!(first_name: 'Andy')
# throws exception if validations fail

nina = Customer.find_or_initialize_by(first_name: 'Nina')
# won't persist the customer. You have to call nina.save
```

## Finding by SQL

```rb
Customer.find_by_sql("SELECT * FROM customers INNER JOIN orders ON customers.id = orders.customer_id ORDER BY customers.created_at desc")

Customer.lease_connection.select_all("SELECT first_name, created_at FROM customers WHERE id = '1'").to_a # => [{...}, {...}, ...] (hash array of database entries)

Book.where(out_of_print: true).pluck(:id) # => [1, 5, 8]

Customer.where(id: 1).pick(:id)
# same as
Customer.where(id: 1).pluck(:id).first

Customer.ids
# same as
Customer.pluck(:id)
```

## Existence of Objects

```rb
Customer.exists?(1)
Customer.exists?(first_name: ["Jane", "Sergei"])
Customer.where(first_name: "Ryan").exists?
```

## Calculations

```rb
Customer.count(:title)
Order.average("subtotal")
Order.minimum("subtotal")
Order.maximum("subtotal")
Order.sum("subtotal")
```