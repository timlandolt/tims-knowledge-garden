---
{"dg-publish":true,"permalink":"/knowledge/media-types/","tags":["webdevelopement"]}
---

---

Media types indicate the format of a file or document. They used to be called MIME types. MIME stands for Multipurpose Internet Mail Extensions.
The browser uses the media type, and not the file extension to interpret the content.
The media type can be set in the `Content-Type` header.

The MIME types are specified like this:
`type/subtype` an optional; parameter can be added: `text/plain;charset=UTF-8`

## Types
There are two types: Discrete and Multipart.

### Discrete
Examples for discrete types are:
- `application`
	- `application/json`
- `audio`
- `font`
- `image`
- `text`
	- `text/plain`
	- `text/css`
	- `text/html`
	- `text/javascript`
- `video`
- ...

### Multipart
Multipart types represent a composite document.
There are only two types:
- `message` -- a message encapsulating other messages
	- `message/rfc822` -- forwarded message
	- `message/partial` -- a part of a message that will be reassembled by the recipient
- `multipart`
	- `multipart/form-data` -- used for `POST` of html forms
	- `multipart/alternative` -- used for emails that have a text and html representation
	- `multipart/mixed` -- used for emails with attachments