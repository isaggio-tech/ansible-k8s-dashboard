# Ansible K8s Dispatcher

Anisble Kubernetes Dashboard helps in deploying Kubernetes-dahsboard along with the roles and certs for Access Ready. The Playbook does also print the token to be used for UI access !

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

Should have below installed on the Ansible playbook's executing Host

```
ansible
```

Should have below on K8s cluster Nodes,

```
> Up and Running Kubernetes Cluster
> Passwordless access from the Ansible Managing host to all K8s Nodes
> private_key_file in the right Location - to be used inside anisble.cfg
```

### Installing/Getting Ready

Git Clone this repo and modify and update the below files,

```
hosts
env_variables
ansible.cfg (remote_user, private_key_file etc)
```

### Run Playbook

Running playbook is simple and we have 2 wrapper playbooks that does the work for us,
First lets test the connection to the cluster nodes,


## Test Connection

echo hello on all nodes

```
ansible all -a "/bin/echo hello"

k8s-master | CHANGED | rc=0 >>
hello

```

If you see above output, please proceed deploying the playbook

## Deploy Kubernetes Dashboard

Assuming you have up and running Kubernetes Cluster

```
ansible-playbook setup_k8s_dashboard.yml
```

Note1: setup_k8s_dashboard.yml will drop existing kubernetes-dashboard-certs, dependents and Recreate
Note2: Currently NodePort is fixed to Port 32444, but can be configured in the Yaml file kubernetes-dashboard.yaml
Note3: Please take a note of the Token printed at the end of the Playbook run

### Verify Access to Dashboard

Connect to any node that has access to K8s Network, and run below

```
https://<kubernetes-node>:32444
```

Now you could use the Token printed from the Ansible Playbook output to access the Dashboard


## Built With

* [ansible](https://opensource.com/article/18/7/sysadmin-tasks-ansible) - IaaC Tool

## Authors

* **Hari Chintala** - *Initial work* 
