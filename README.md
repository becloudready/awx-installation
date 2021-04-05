# AWX-Installation
> This repo provides the details how to install to AWX in Kubernetes.

# Prerequisites
* A Kubernetes Cluster.
* A Kubectl CLI Tool.

# Step 1: Clone the AWX GitHub repository

> git clone https://github.com/becloudready/awx.git
>
> cd awx
>
> git checkout -b branch-17

# Step 2: Edit & Delete the following files
* Now go inside the installer directory
> cd installer
* Edit the following values in the inventory file.
> kubernetes_context=Your context name  # You can find this in kubeconfig file
>
> kubernetes_namespace=Your namespace   # You can give any name for namespace
>
> kubernetes_web_svc_type=NodePort
>
> admin_user=admin          # Default user name
>
> admin_password=password   # Default password

* Now go back to installer directory & delete the following line from install.yml file
> {role: local_docker, when: "openshift_host is not defined and kubernetes_context is not defined"}
* Next, edit the main.yml file placed inside awx/installer/roles/Kubernetes/default/ directory with the following content.
> 
>
>dockerhub_version: "{{ lookup('file', playbook_dir + '/../VERSION') }}"
>
>create_preload_data: true
>
>admin_user: 'admin'
>
>admin_email: 'root@localhost'
>
>admin_password: ''
>
>kubernetes_base_path:"{{local_base_config_path|default('/tmp')}}/{{kubernetes_deployment_name }}-config"
>
>kubernetes_awx_version: "{{ dockerhub_version }}"
>
>kubernetes_awx_image: "ansible/awx"
>
>kubernetes_web_svc_type: "NodePort"
>
>awx_psp_create: false
>
>awx_psp_name: 'awx'
>
>awx_psp_privileged: true
>
>web_mem_request: 1
>
>web_cpu_request: 500
>
>web_security_context_enabled: true
>
>web_security_context_privileged: false
>
>task_mem_request: 2
>
>task_cpu_request: 1500
>
>task_security_context_enabled: true
>
>task_security_context_privileged: true
>
>redis_mem_request: 2
>
>redis_cpu_request: 500
>
>redis_security_context_enabled: true
>
>redis_security_context_privileged: false
>
>redis_security_context_user: 1001
>
>kubernetes_redis_image: "redis"
>
>kubernetes_redis_image_tag: "6.2.1"
>
>kubernetes_redis_config_mount_path: "/usr/local/etc/redis/redis.conf"
>
>openshift_pg_emptydir: false
>
>openshift_pg_pvc_name: postgresql
>
>kubernetes_deployment_name: awx
>
>kubernetes_serviceaccount_name: awx
>
>kubernetes_deployment_replica_size: 1
>
>postgress_activate_wait: 60
>
>restore_backup_file: "./tower-openshift-backup-latest.tar.gz"
>
>insights_url_base: "https://example.org"
>
>automation_analytics_url: "https://example.org"
>
>insights_agent_mime: "application/example"
>
>custom_venvs_path: "/opt/custom-venvs"
>
>custom_venvs_python: "python2"
>
>ca_trust_bundle: "/etc/pki/tls/certs/ca-bundle.crt"
>
>container_groups_image: "ansible/ansible-runner"
>
>uwsgi_bash: "bash -c"

# Step 3: Run the Ansible Playbook
* Now go to the directory awx/installer & run the ansible playbook **install.yml** by running the following command.
> ansible-playbook -i inventory install.yml
>
> It will take around 5-10 minutes to complete.

# Step 4: Access the AWX Web UI
* To access the AWX web interface with **NodePort IP** & **NodePort port number** run the following command
> kubectl get nodes -o wide |  awk {'print $1" " $2 " " $7'} | column -t
* Now you can access the awx web interface at http://NodePort-IP:Port