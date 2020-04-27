---
tags:
  - docker
categories:
  - development
excerpt: >-
    removing docker compose containers and images using rmi command
---

Stop and remove images in a docker compose project
```
docker-compose down --rmi all -v
```
It may be necessary to prune the images to fully remove them from disk
```
docker image prune --all
```

 
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogZG9ja2VyXG5jYXRlZ29yaW
VzOiBkZXZlbG9wbWVudFxuZXhjZXJwdDogcmVtb3ZpbmcgZG9j
a2VyIGNvbXBvc2UgY29udGFpbmVycyBhbmQgaW1hZ2VzIHVzaW
5nIHJtaSBjb21tYW5kXG4iLCJoaXN0b3J5IjpbLTU2OTI3NzM3
OCw2MjA5OTI4MTYsLTg1MDMwMTM2NywtMjA4ODc0NjYxMl19
-->