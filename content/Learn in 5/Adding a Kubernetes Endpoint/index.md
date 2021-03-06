---
title: "Adding a Kubernetes Endpoint"
date: 26/04/2022
draft: false
---

In order to use a [Kuberenetes Task](/pipelines/tasks/kubernetes), or to use a kubernetes cluster as your [pipeline workspace](/pipelines/#kubernetes-workspace-only), you need to configure a [kubernetes endpoint](/configure/endpoints/kubernetes).

## Prerequisites
* Any Kubernetes compliant cluster
* Network connectivity to the Kubernetes cluster - either direct or via a Cloud Proxy (for vrealize automation cloud)
* An authentication token, certificate, or basic authentication username and password

The type of authentication you use will be dependant on the Kubernetes cluster you are using, and what type of access you want to allow Code Stream to have. Typically a Service Account can be created with a restricted set permissions and the token of this account used to authenticate.

