---
{"dg-publish":true,"permalink":"/knowledge/html-form-enctype/","tags":["webdevelopement","html","html-attribute"]}
---

---

The `enctype` attribute on [[Knowledge/HTML\|HTML]] form tags specify how the form data should be encoded when delivered using the `POST` method. 

```html
<form enctype="value">
```

The `enctype` is a [[Knowledge/Media Types\|MIME type]].


## Default (`application/x-www-form-urlencoded`)
All characters are encoded before being sent. Spaces become + and special ones are converted to ASCII HEX values.

```html
<form action="http://localhost:3333/post" method="post">
    <input type="text" value="Test, 1234" name="someInput">
    <input type="text" value="Ä und %" name="otherInput">
    <input type="submit">
</form>
```

```
someInput=Test%2C+1234&otherInput=%C3%84+und+%25
```


## `multipart/form-data`

This one has to be set when sending files over a form.

```html
<form action="http://localhost:3333/post" method="post" enctype="multipart/form-data">
    <input type="text" value="Test, 1234" name="someInput">
    <input type="text" value="Ä und %" name="otherInput">
    <input type="submit">
</form>
```

```
------WebKitFormBoundaryIu9hf318CXcd0tIK
Content-Disposition: form-data; name="someInput"

Test, 1234
------WebKitFormBoundaryIu9hf318CXcd0tIK
Content-Disposition: form-data; name="otherInput"

Ä und %
------WebKitFormBoundaryIu9hf318CXcd0tIK--
```

## `text/plain`

Sends the form data without encoding. This is not recommended.

```html
<form action="http://localhost:3333/post" method="post" enctype="text/plain">
    <input type="text" value="Test, 1234" name="someInput">
    <input type="text" value="Ä und %" name="otherInput">
    <input type="submit">
</form>
```

```
someInput=Test, 1234 otherInput=Ä und %
```

