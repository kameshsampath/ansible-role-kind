Kind
=========

Ansible to create [KinD](https://kind.sigs.k8s.io) cluster. The role can also be configured to install and configure

- [Ingress](https://kind.sigs.k8s.io/docs/user/ingress/#ingress-nginx)
- [Knative](https://knative.dev)
- [Tekton](https://tekton.dev)

IMPORTANT: Work in Progress

Requirements
------------

- Docker Desktop or Docker/Podman for Linux

- Ansible

```shell
pip3 install -U -r requirements.txt
ansible-galaxy collections install community.kubernetes
```

Role Variables
--------------

| Variable Name| Description | Default |
|--|--|--|
| cluster_name| Name of the KinD cluster| kind |
| kind_create|  If True creates the cluster | True |
| kind_destroy| If True destroys the cluster | True |
| kind_version| The KinD version | v0.8.1 |
| kind_home_dir| The directory where KinD files will be stored | $HOME/.kind |
| kind_cluster_config| The KinD cluster config file | $HOME/.kind/{{cluster_name}}/kind-cluster-config.yml |
| kind_custom_registry| Deploy a KinD registry | True |
| container_registry_name | The container registry name | kind-registry |
| container_registry_port | The container registry port | 5000 |
| deploy_knative | Deploy Knative | False |
| deploy_ingress | Deploy Ingress | True |
| deploy_tekton  | Deploy Tekton  | False |
|extra_port_mappings| Extra Port Mappings for KinD. A YAML list of format `listen-address:hostPort:containerPort` | '0.0.0.0:80:80', '0.0.0.0:443:443' |


Example Playbook
----------------

The following playbook creates an one master and one worker KinD cluster with Nginx Ingress Controller deployed.

```YAML
---
- name: Converge
  hosts: localhost
  connection: local

  collections:
    - community.kubernetes

  vars:
    ansible_python_interpreter: '{{ ansible_playbook_python }}'
    cluster_name: demo
    ingress: True

  roles:
    - role: kameshsampath.kind
```

License
-------

Apache v2

Author Information
------------------

[Kamesh Sampath](mailto:kamesh.sampath@hotmail.com)

Testing
=======

Requirements
------------

```shell
pip install molecule yamllint ansible-lint docker
```

All tests are built using [molecule](pre_reqs_local) with following scenarios

* default 
```shell
molecule test
```
* pre_reqs
```shell
molecule pre_reqs
```
* pre_reqs_local
```shell
molecule pre_reqs_local
```

