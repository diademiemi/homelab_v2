# Homelab V2
This is my lab setup I built in January of 2023. It uses Terraform for provisioning, Ansible for configuration management and ArgoCD for deployment.  

## Related repositories
Please check the following repositories (as submodules) for specific information about the different parts of the setup:  
Name | Description | Link
--- | --- | ---
Ansible | Configuration management. Installs libvirt for use with Terraform to provision virtual machines and K3S on the virtual machines. | https://github.com/diademiemi/ansible_project_homelab_v2
Terraform | Infrastructure as Code. Provisioning virtual machines on a Hetzner dedicated machine and a local server. | https://github.com/diademiemi/terraform_homelab_v2
ArgoCD | Deploying applications to the clusters with ApplicationSets. | https://github.com/diademiemi/argocd_project_homelab_v2  
Charts | Helm Charts | https://github.com/diademiemi/charts | My personal Helm charts for applications deployed to the clusters

## Technologies used

Name | Description | Link | Used for
--- | --- | --- | ---
Terraform | Infrastructure as Code | https://www.terraform.io/ | Provisioning virtual machine on a Hetzner dedicated machine and a local server
Debian | Operating System | https://www.debian.org/ | Operating system for the virtual machines
Ansible | Configuration Management | https://www.ansible.com/ | Configuring the virtual machines and installing K3S
K3S | Lightweight Kubernetes | https://k3s.io/ | Running two single-node clusters
ArgoCD | GitOps | https://argoproj.github.io/argo-cd/ | Deploying applications to the clusters
Wireguard | VPN | https://www.wireguard.com/ | Connecting the remote server to the local network to reverse proxy traffic to local apps
## Applications deployed to the clusters:
Name | Description | Link | Deployed on | Used for
--- | --- | --- | --- | ---
ArgoCD | GitOps | https://argoproj.github.io/argo-cd/ | Both clusters | Deploying applications to the clusters
Traefik | Ingress Controller | https://traefik.io/ | Both clusters | Ingress for all applications. It is exposed to the internet on port 80 and 443 on the Hetzner hosted VM
Cert-Manager | Certificate Management | https://cert-manager.io/ | Cloud | Issuing certificates for all applications
Longhorn | Storage | https://longhorn.io/ | Cloud | Storage for all applications
GitLab | Git Repository | https://about.gitlab.com/ | Cloud | Git mirror of my GitHub repositories
Jellyfin | Media Server | https://jellyfin.org/ | Local | Media server for my local network
Joplin Server | Note Taking | https://joplinapp.org/ | Cloud | Sync for Joplin on my devices
Syncthing | File Sync | https://syncthing.net/ | Local | Sync for my local files between all my devices
Vaultwarden | Password Manager | https://github.com/dani-garcia/vaultwarden | Cloud | Password manager for my devices

## Archived
I'm ultimately abandoning these repositories as I'm not planning on using this setup anymore. Feel free to ask me questions about it though.  

You may notice the local server is only used for Syncthing and Jellyfin. The overhead on this for running it in a virtual machine, in Kubernetes, managed with ArgoCD is a bit extreme, even for me.  

I had other plans at first for distributing the load between the two servers, but the latency made this difficult. Or was it just a configuration error? I moved on by then as I realised that if I were okay with running an application in a cloud VM, there was no point anymore having it locally anyway. The dedicated server on Hetzner running that VM is more than powerful enough to run everything and I can access it from anywhere. I decided to reduce the complexity of my setup and just run everything on the Hetzner server except for files and media.  

Even then, Syncthing and Jellyfin don't really work well in a Kubernetes cluster due to networking requirements and have no benefit from it. My next setup will have the local server running everything bare metal.  

I learnt a lot from this setup and I'm glad I did it. I documented this for others to learn from it. This repository is licensed under the [MIT license](LICENSE). I hope this can serve as an example for others on how to use Ansible, ArgoCD, ArgoCD ApplicationSets, Terraform and K3S to build a homelab or any other environment.  