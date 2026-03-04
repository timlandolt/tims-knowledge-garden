---
{"dg-publish":true,"permalink":"/knowledge/why-no-ssh-in-docker/","tags":["docker"]}
---

---

- larger container image
- Complex to manage all the different ssh connections from each container (keys, users, ...)
- Longer build times
- A docker container should only do one thing
- Running the container uses a lot more resources.
- More potential security issues

- Better alternative: Ssh into host, docker exec into container