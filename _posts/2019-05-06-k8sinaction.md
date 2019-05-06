---
layout: post
title: "Kubernetes in action Chapter 3 with command line"
categories: k8s in action ch3
---
This is refered to 'Kuberenetes in action' book.
Chapter3 is for user what is pod and how to use pod.

`test-manual.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: test-manual
spec:
    containers:
    - image: rozen88/test
      name: test-manual
      ports:
      - containerPort: 8080
        protocol: TCP
```

{% highlight bash %}
kubectl create -f test-manual.yaml
{% endhighlight %}
