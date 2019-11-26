---
layout: docs
title: "Dashboard addon"
permalink: /docs/addon-dashboard
---

# Dashboard addon

The standard Kubernetes Dashboard is a convenient way to keep track of the
activity and resource use of MicroK8s

```bash
microk8s.enable dashboard
```

To log in to the Dashboard, you will need the access token (unless RBAC has
also been enabled). This is generated randomly on deployment, so a few commands
are needed to retrieve it:

```bash
token=$(microk8s.kubectl -n kube-system get secret | grep default-token | cut -d " " -f1)
microk8s.kubectl -n kube-system describe secret $token
```
In an RBAC enabled setup (`microk8s.enable rbac`) you need to create a user with
restricted permissions as detailed in the
[upstream Dashboard wiki][upstream-dashboard]

Next, you need a connection to the API server. While the MicroK8s snap will
have an IP address on your local network, the recommended way to do this is
through the proxy service. You can initiate the proxy with the command:

```bash
microk8s.kubectl proxy --accept-hosts=.* --address=0.0.0.0
```

> Note: Although you can run the above command in the background, it is more useful to run it in a different terminal so it is easier to catch any errors


You can then access the Dashboard at the address

[http://127.0.0.1:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/]

![IMAGE of Dashboard](https://assets.ubuntu.com/v1/c9cec03a-ubuntu18.04-microk8s+on+QEMU-KVM_007.png)

[upstream-dashboard]: https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md 
<!-- FEEDBACK -->
<div class="p-notification--information">
  <p class="p-notification__response">
    We appreciate your feedback on the docs. You can 
    <a href="https://github.com/canonical-web-and-design/microk8s.io/edit/master/docs/addon-dashboard.md" class="p-notification__action">edit this page</a> 
    or 
    <a href="https://github.com/canonical-web-and-design/microk8s.io/issues/new" class="p-notification__action">file a bug here</a>.
  </p>
</div>
