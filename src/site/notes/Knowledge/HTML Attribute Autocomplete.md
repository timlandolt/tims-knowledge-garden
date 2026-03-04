---
{"dg-publish":true,"permalink":"/knowledge/html-attribute-autocomplete/"}
---

Does what you would expect: Assists software like password managers to automatically fill in form fields. 
The attribute is available on `<input>` elements that take a text or numeric value as input, `<textarea>` elements, `<select>` elements, and `<form>` elements.

What's interesting, is that they also serve a purpose on hidden form attributes. When applied to a hidden input that has a value set, the user client can use these values for context. For example to choose the most relevant credit card based on the amount and currency:

```html
<form method=post action="step2.cgi">
  <input type=hidden autocomplete=transaction-currency value="CHF">
  <input type=hidden autocomplete=transaction-amount value="15.00">
  
  <input type=text inputmode=numeric autocomplete=cc-number>
  <input type=month autocomplete=cc-exp>
  
  <input type=submit value="Continue...">
</form>
```

### Important / interesting field Types

- `name` -> Full Name
- `username` 
- `new-password` -> When registering/changing password
- `current-password` -> Password belonging to `username`
- `one-time-code` 
- `street-address` 
- `country`
- `postal-code`
- `cc-*` -> credit card info (e.g. `cc-name`, `cc-number`...)
- `bday` -> Birthday
- `tel`
- `email`

Sources:
[HTML attribute: autocomplete](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/autocomplete)
[HTML Standard](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#autofill)
