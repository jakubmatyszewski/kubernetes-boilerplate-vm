Vagrant kubernetes boilerplate VM
---

Prerequisites:
---
- vagrant
- ansible

Setup
---
`vagrant up` produces 2 provisioned vm's standing on Debian 11 with Kubernetes running.

To access kubernetes dashboard check kubernetes-dashboard service port:
```console
kubectl get svc kubernetes-dashboard -n kubernetes-dashboard -o go-template="{{ (index .spec.ports 0).nodePort }}"
```

The dashboard is accessible via `https://192.168.50.10:SERVICE_PORT`. Token for admin user is saved on k8s-master VM in `/home/vagrant/dashboard_admin_token.txt`.
