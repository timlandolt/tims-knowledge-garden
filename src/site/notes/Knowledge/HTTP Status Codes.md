---
{"dg-publish":true,"permalink":"/knowledge/http-status-codes/","tags":["http","status-codes","http-status-codes"]}
---

---

## 1xx: Informational Messages
Purely for informational purposes

## 2xx: Successful

- **200 OK** - request was successful, body contains requested content
- **202 Accepted** - request was processed successfully, but may not contain the requested body (for example with async processing)
- **204 No Content** - No contentent available
- **205 Reset Content** - Indicates, that the client should reset the document view
- **206 Partial Content** - The body only contains a part of the content. The other headers specify more.

## 3xx: Redirection

- **301 Moved Permanently** - Resource is at new URL
- **303 See Other** - The resource is temporarily at a new URL. The new URL is passed in the Location header.
- **304 Not Modified** - The resource has not changed and the client should use the cached version. (This can be determined by the ETag sent by the client - a hash of the page)

## 4xx: Client Error

- **400 Bad Request**: the request was malformed.
- **401 Unauthorized**: request requires authentication. The client can repeat the request with the `Authorization` header. If the client already included the `Authorization` header, then the credentials were wrong.
- **403 Forbidden**: server has denied access to the resource.
- **404 Not Found**: indicates that the resource is invalid and does not exist on the server. The other codes in this class include:
- **405 Method Not Allowed**: invalid HTTP verb used in the request line, or the server does not support that verb.
- **409 Conflict**: the server could not complete the request because the client is trying to modify a resource that is newer than the client's timestamp. Conflicts arise mostly for PUT requests during collaborative edits on a resource.

## 5xx: Server Error

- **500 Internal Server Error**: the server had some sort of crash or internal error that stopped it from fulfilling the request.
- **501 Not Implemented**: the server does not yet support the requested functionality.
- **503 Service Unavailable**: this could happen if an internal system on the server has failed or the server is overloaded. Typically, the server won't even respond and the request will time out.
