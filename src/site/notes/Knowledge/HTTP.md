---
{"dg-publish":true,"permalink":"/knowledge/http/","tags":["http","https","protocol","webdevelopement"]}
---

---

**HTTP** = Hypertext Transfer Protocol

HTTP is a protocol based on [[Knowledge/TCP and UDP\|TCP]]/IP. It is stateless, which means every request needs to carry the information needed to fulfil it. This information is carried in the header.
In HTTP, all the requests and responses (including headers) are human-readable.

## HTTP/1.1 vs HTTP/2.0
HTTP/2.0 supports multiplexing. This means that multiple requests can be sent at once:

![Pasted image 20251201122025.png](/img/user/Ressources/Pasted%20image%2020251201122025.png)

## HTTP URLs

`https://www.domain.com:1234/path/to/resource?a=b&x=y`

- **https** specifies the protocol. It can be http or https, which makes the communication secure. 
- **www.domain.com** is the host.
- **1234** is the port. In many cases, the browser hides the port. The default is 80.
- **path/to/resource** is the resource path. It helps the server identify a specific resource and generate the right response. 
- **?a=b&x=y** are query string parameters. Query string parameters are used by the server to spot the right resource.

## HTTP Request

### Structure
![Pasted image 20251201122746.png](/img/user/Ressources/Pasted%20image%2020251201122746.png)

### HTTP Request Verbs

- **GET**: Fetch a resource, all pieces of information shopuld be delivered over the URL
- **POST**: Create an object. Payload is optional
- **PUT**: Update/Raplace existing resource, payload is optional
- **DELETE**: Deletes a resource

PUT and DELETE are in theory also just POST requests

## HTTP Status Codes
Look [[Knowledge/HTTP Status Codes\|here]].