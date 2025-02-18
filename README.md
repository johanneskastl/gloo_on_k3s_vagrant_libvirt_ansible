# gloo_on_k3s_vagrant_libvirt_ansible

Vagrant-libvirt setup that creates a VM with [k3s](https://k3s.io/), the minimal
lightweight Kubernetes distribution.

Instead of Traefik, that normally comes with k3s, this setup installs the [gloo
API gateway](https://github.com/solo-io/gloo) and a small Nginx application,
that it exposes using the [Kubernetes
GatewayAPI](https://kubernetes.io/docs/concepts/services-networking/gateway/).

Default OS is openSUSE Leap 15.6, but that can be changed in the Vagrantfile.
Please be aware, that this might break the Ansible provisioning.

## Vagrant

1. You need `vagrant`, obviously. And `git`. And Ansible...
1. Fetch the box, per default this is `opensuse/Leap-15.6.x86_64`, using
   `vagrant box add opensuse/Leap-15.6.x86_64`.
1. Make sure the git submodules are fully working by issuing
   `git submodule init && git submodule update`
1. Run `vagrant up`
1. Wait for the Ansible provisioning to finish. At the end, it will output a URL
   that looks something like `http://nginx.192.0.2.13.sslip.io`.
1. Open that URL in your browser and you should see the Nginx welcome page,
   served by Nginx and Gloo.
1. Party!

## Cleaning up

The VMs can be torn down after playing around using `vagrant destroy`. This will
also remove the kubeconfig file `ansible/k3s-kubeconfig`.
