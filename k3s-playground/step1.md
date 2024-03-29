Execute the K3s installation using the following command:

```
time curl -sfL https://get.k3s.io | sh -
```{{exec}}
**Note**: command `time` is used to measure the execution time of k3s installation process.


To install with specific version of Kubernetes, use environment variable `INSTALL_K3S_VERSION` as follow:

```
$ curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v1.25.7 sh -
```

The above installation is single node installation, which is often a perfect environment for quick development, experimentation, validation, and learning purpose. We can check the cluster node status:

```
systemctl status k3s.service
```{{exec}}

```
k3s kubectl get nodes
```{{exec}}

*Inspect K3s Resource consumption*

In the previous step, we obtained the current disk and memory utilization of this Linux system before installing K3s. To assess the disk and memory usage of K3s, we are now examining the resource consumption after the K3s installation.

```
df -h 
```{{exec}}

```
free -h 
```{{exec}}

## K3s Kubernetes Control Plane
You can lookat the whole cluster with the `kubectl cluster-info`:

```
kubectl cluster-info
```{{exec}}

You will notice that :
* The Kubernetes API is exposed on port 6443
* The standard _CoreDNS_ and _Metrics-server_ is present. 

You can execute the command below to inspect the main component of Control node:
```
kubectl get componentstatus
```{{exec}}



To further inspect the control plane:

```
kubectl get pods,services --all-namespaces
```{{exec}}

If you're concerned about the memory footprint of K3s, list the base component memory impacts while the cluster is in a quiet state:

```
top -o %MEM -b -n1 | head -n 24
```{{exec}}
