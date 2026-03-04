---
{"dg-publish":true,"permalink":"/knowledge/ruby-percent-literals/"}
---

%w = String array
%i = symbol array
%r = regex

%q = non interpolated string (no string interpolation, only `\\` and `\'`  escaping allowed)
%Q = INTERPOLATED STRING (`#{...}` AND STUFF LIKE `\n` is allowed )
%Q can also be written with just %

In theory you could replace the braces with any symbol, but the way to go is as followed:

```ruby
arrays = %w[hello world]
regex = %r{hello}
strings_and_others = %(world)
```