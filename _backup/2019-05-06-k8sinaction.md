---
layout: post
title: "Kubernetes in action [Chapter 3]"

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

Make pods manually with yaml file.
{% highlight bash %}
kubectl create -f test-manual.yaml	# make pod manually with yaml

kubectl get po test-manual -o yaml	# get pod description <yaml>

kubectl get po test-manual -o json	# get pod description <json>

kubectl logs test-manual		# See logs in 'test-manual' pod
{% endhighlight %}

Port forwarding pod
{% highlight bash %}
kubectl port-forward test-manual 8888:8080

--> [another cmd] curl localhost:8888
{% endhighlight %}

Make manual pod with label

`test-label-manual.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: test-manual-v2
    labels:
      creation_method: manual
      env: prod
spec:
    containers:
    - image: rozen88/test
      name: test-manual
      ports:
      - containerPort: 8080
        protocol: TCP
```

{% highlight bash %}
kubectl create -f test-label-manual.yaml	# Make manual pod with label

kubectl get po --show-labels

kubectl get po -L creation_method,env
{% endhighlight %}

Modifying labels
{% highlight bash %}
kubectl label po test-manual creation_method=manual	# Labeling to exist pod

kubectl label po test-manual-v2 env=debug --overwrite	# Modifying labels different pod

kubectl get po -L creation_method,env			# Get pod labels
{% endhighlight %}

Label selector & multi select
{% highlight bash %}
kubectl get po -l creation_method=manual

kubectl get po -l env

kubectl get po -l '!env'

kubectl get po -l 'creation_method!=manual'

kubectl get po -l 'env in (debug)'
{% endhighlight %}


`test-manual-specific-node.yaml`
```yaml
apiVersion: v1
kind: Pod
metadata:
    name: test-manual-v2
    labels:
      creation_method: manual
      env: prod
spec:
    nodeSelector:
      gpu: "true"
    containers:
    - image: rozen88/test
      name: test-manual
      ports:
      - containerPort: 8080
        protocol: TCP
```


{% highlight bash %}

{% endhighlight %}

{% highlight bash %}

{% endhighlight %}
