# Sample HTML Web Page Automatic Deployment using Jenkins and Kubernetes.

## Tools Used:

    1. Three CentOS AWS Virtual Machines.
    2. Docker Base Image Apache httpd v2.4
    3. Docker v1.13.1
    4. Kubernetes v1.16.3
    5. Jenkins v2.190.3
    6. Ansible v2.4.2
    

## Procedure for website configuration and automatic deployment on Kubernetes

   * Provision 3 CentOS-7 AWS Virtual Machines. Configure appropriate network ACL rules for Public 
   subnet as recommended on this AWS document (https://docs.aws.amazon.com/vpc/latest/userguide/vpc-recommended-nacl-rules.html)
    
   * Configure automatic installation of Kubernetes Cluster with 1 Master and 2 Worker nodes with the 
   use of Ansible playbooks. Details given in this public repository (https://github.com/isingh14/kubernetes-installation-ansible.git)
    
     * In my case, all kubernetes nodes belonged to the same subnet and I didn't configure firewall rules 
    for communication between different Kubernetes resources e.g. api server, kube-scheduler, kube-controller, 
    kubelet and kube-proxy. If your kubernetes nodes are part of different subnet then you need to define 
    firewall rules and open the intended ports as mentioned in this document (https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/). Go to "Check required ports" section.
    
 * Create a namespace for Jenkins in the Kubernetes Cluster and run one copy of the Jenkins Official Docker Image in the Cluster. You can use the kubernetes deployment and service file given in this GIT repo (https://github.com/isingh14/jenkins-installation-kubernetes.git).
 
 * Access Jenkins here http://<host_ip>:8080. This repository (https://github.com/isingh14/sample-html-page-kubernetes.git) holds all the required code files for building this website. Configure the pipeline job in Jenkins, putting the GIT repo
 address in the "Pipeline from SCM".
 
 * Files in this repo:
   * Index.html file
     * HTML Source code to be copied into the apache web server container.
   * Dockerfile
     * Provision Docker Image using Apache httpd 2.4 as the base image. Copy Index.html file into it.
   * Jenkinsfile
     * CI Pipeline to build and push Docker Image into Docker Hub and then run the deployment in the Kubernetes Cluster.
   * Deployment.yaml file
     * Kubernetes deployment of our website triggered from Jenkins peipeline. This file contains deployment strategy of our website e.g. replicas, label, container port, expose method etc.
