---
{"dg-publish":true,"permalink":"/knowledge/rails-database-best-practices/","tags":["ruby-on-rails","ruby","active-record","best-practices"]}
---

---
*Based on [this](https://web.archive.org/web/20221226000533/https://blog.carbonfive.com/rails-database-best-practices) article about [[Knowledge/Ruby on Rails\|rails]] database best practices*

## Efficient and chainable Scopes

- Always return `ActiveRecord::Relation`, so scopes remain chainable
- Filter and sort in the database (its much quicker)
- Don't order inside the scope (or create a separate scope). So the user can oder as they like

**Bad**

![Pasted image 20250821110235.png](/img/user/Ressources/Pasted%20image%2020250821110235.png)

**Good**

![Pasted image 20250821110328.png](/img/user/Ressources/Pasted%20image%2020250821110328.png)

## Reduce Calls to the database
Try to use as much of `.includes()`, `.joins()` (see [[Knowledge/test/Active Record Query Interface#Joining Tables\|here]]), `.group()` (see [[Knowledge/test/Active Record Query Interface#Grouping\|here]])and `.having()` (see [[Knowledge/test/Active Record Query Interface#HAVING conditions\|here]]). Sometimes ![Pasted image 20250821110328.png](/img/user/Ressources/Pasted%20image%2020250821110328.png)the best way is to write custom SQL.
Check this chapter out for more about the topic [13. Eager Loading Associations](https://guides.rubyonrails.org/active_record_querying.html#eager-loading-associations)

## Use Indexes
Every column that gets used in a where clause should have an index.

```zsh
# shell command
bin/rails generate migration AddPartNumberToProducts part_number:string:index
```

```rb
# migration script

class AddPartNumberToProducts < ActiveRecord::Migration[8.0]
  def change
    add_column :products, :part_number, :string
    add_index :products, :part_number
  end
end
```

## Avoid 'ad-hoc' queries
Only ever use ad-hoc queries inside [[Knowledge/test/Active Record Query Interface#Scopes\|scopes]] or query objects. This allows for better testing and enables to reuse it.

## Use the Right Types
Use the types the RDBMS gives you. Not just the ORM ones. Some of them require an extension.

