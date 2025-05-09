# Kubernetes Single Node Cluster with External etcd + KubeSphere

This project demonstrates how to create a **single-node Kubernetes cluster** using **KubeKey**.

---

## Requirements

- Ubuntu 22.04 LTS VM
- Minimum 4 vCPU and 8 GB RAM (Recommended: 6 vCPU and 16 GB RAM)
- Docker + cri-dockerd
- Internet connection

---

## Installation Steps Overview

1. **Prepare the Environment**
   - Install Docker, cri-dockerd, kubeadm, kubectl, kubelet.
   - Install KubeKey binary (`kk`).

2. **Generate External etcd Certificates**
   - Create /etc/ssl/etcd/ssl/ and generate certs using kubeadm.

3. **Start External etcd Service**
   ```bash
   sudo nohup etcd --name etcd-node1 --data-dir /var/lib/etcd ... &
   ```

4. **Create Kubernetes Cluster with KubeKey**
   ```bash
   sudo kk create cluster -f config-sample.yaml
   ```

5. **Deploy KubeSphere**
   ```bash
   kubectl apply -f kubesphere-installer.yaml
   kubectl apply -f cluster-configuration.yaml
   ```

6. **Access Kubernetes**
   ```bash
   kubectl get pods -A
   kubectl get nodes
   ```

## Files Included

* `config-sample.yaml`: KubeKey cluster config file
* `kubeadm-config.yaml`: Kubeadm fix config for CRI
* `kubesphere-installer.yaml`: Installer manifest for KubeSphere
* `cluster-configuration.yaml`: Configuration file for KubeSphere

## References

* KubeKey Documentation: https://github.com/kubesphere/kubekey
* KubeSphere Installation Guide: https://kubesphere.io/
