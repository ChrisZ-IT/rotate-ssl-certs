# rotate-ssl-certs
Ansible Playbooks to rotate SSL certs

These playbooks were created to automate rotating my SSL certs on applications/services running outside of K8s.
I deployed [cert-manager and certificate](https://github.com/ChrisZ-IT/cert-manager) resources in my k8s cluster.


Im using cert manager in my k8s cluster to renew the let's encrypt cert and then created these ansible playbooks to then read the new certs and rotate them in the services outside of k8s; for example in opnsense and synology. These then just run once a day as a scheduled jobs from my [awx](https://github.com/ChrisZ-IT/awx_homelab) server


## Required variables
### rotate_opnsense_cert.yml
 - k8s_control_node: <Hostname of your k8s control node>
 - k8s_secret_name: <name of the k8s secret that stores your opnsense cert>
 - k8s_namespace: <namespace this secret is stored in>
 - opnsense_hostname: <opnsense hostname/ip>
 - opnsense_key: <opnsense api key>
 - opnsense_secret <opnsense api secret>
 - cert_description: K8s Let's Encrypt Managed Cert


### rotate_synology_cert.yml
 - k8s_control_node: <Hostname of your k8s control node>
 - k8s_secret_name: <name of the k8s secret that stores your synology cert>
 - k8s_namespace: <namespace this secret is stored in>
 - synology_hostname: <synology hostname/ip>
 - synology_port: <Port DSM run on>
 - synology_username: <synology api key>
 - synology_password <synology api secret>
 - cert_description: K8s Let's Encrypt Managed Cert


### rotate_proxmox_cert.yml
 - proxmox_hostname: <proxmox node name>
 - domain: <domain name>
 - acme_account: <Datacenter \> ACME \> account name>
 - acme_plugin: <Datacenter \> ACME \> plugin name>
 - api_port: <Set via env var `PROXMOX_PORT`>
 - api_token_id: <Set via env var `PROXMOX_TOKEN_ID`>
 - api_token_secret(use this if token_password is not set): <Set via env var `PROXMOX_TOKEN_SECRET`>
 - api_password(use this if token_secret is not set): <Set via env var `PROXMOX_PASSWORD`>

    I just manually setup the initial ACME accounts/pugins/certs in proxmox since its a 1 time thing. This playbook then renews the cert when it expires. I will create another playbook for the config as code setup of these parts in the future.