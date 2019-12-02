# Sample HTML Web Page Automatic Deployment using Jenkins and Kubernetes.

## Tools Used:

    1. Three CentOS AWS Virtual Machines.
    2. Docker Base Image Apache httpd v2.4
    3. Docker v1.13.1
    4. Kubernetes v1.16.3
    5. Jenkins v2.190.3
    6. Ansible v2.4.2
    

## Procedure for website configuration and automatic deployment on Kubernetes

    1. Provision 3 CentOS 7 AWS Virtual Machines. Configure appropriate network ACL rules for Public subnet as recommended on this AWS document - https://docs.aws.amazon.com/vpc/latest/userguide/vpc-recommended-nacl-rules.html
    2. Configure automatic installation of Kubernetes Cluster with 1 Master and 2 Worker nodes with the use of Ansible playbooks. Details given in this public repository - https://github.com/isingh14/kubernetes-installation-ansible.git
    __In my case, all kubernetes nodes belonged to the same subnet and I didn't configure firewall rules for communication between different Kubernetes resources e.g. api server, kube-scheduler, kube-controller, kubelet and kube-proxy. If your kubernetes nodes are part of different subnet then you need to define firewall rules and open the intended ports as mentioned in this document - 
