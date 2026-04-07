---
{"dg-publish":true,"permalink":"/knowledge/debugging-in-rails/","tags":["ruby-on-rails","debug"]}
---

---
Some tools used for debugging in [[Knowledge/Ruby on Rails\|Rails]].

## View Helpers
### `debug`

```erb
<%= debug @article %>

<%# The same as %>
<%= simple_format @article.to_yaml %>
```

Outputs the object as formatted YAML.

### `inspect`

Like `.to_s` but with better output.

## Debugger

In The ruby code, write `debugger`. The debugger will then open in the console.