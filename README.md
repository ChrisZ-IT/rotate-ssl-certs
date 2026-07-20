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
 - k8s_secret_name: <name of the k8s secret that stores your opnsense cert>
 - k8s_namespace: <namespace this secret is stored in>
 - synology_hostname: <opnsense hostname/ip>
 - synology_key: <opnsense api key>
 - synology_secret <opnsense api secret>
 - cert_description: K8s Let's Encrypt Managed Cert