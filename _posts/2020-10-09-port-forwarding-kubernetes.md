---
layout: post
title: Forwarding localhost ports to kubernetes services
tags: [kubernetes]
author: Ozan Öğreden
comment: false
---

I've been using Kubernetes pretty much weekly since I started working at ParkBee.
When I first started, I went through a few Kubernetes tutorials and I read quite a bit of documentation (and certainly way too much for a data scientist).

These helped me gain speed in testing our internal warehouse backend products, as well as data science APIs.
For instance for API testing, I have been getting the cluster IP address of a pod and copy pasting it to curl or Postman.
This takes a few clicks, but become easily frustrating when I have to repeat it a number of times.

It turns out, `kubectl` supports port forwarding, like so:

```
kubectl port-forward services/awesome-data-service-name 5000:5000
```

after which a GET request like `curl 127.0.0.1:5000` will be hitting our awesome service.

Wonderful! 👏🏽
