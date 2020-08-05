Ansible role for KinD
=====================

Ansible to create [KinD](https://kind.sigs.k8s.io) cluster. 


Requirements
------------

- [Docker Desktop](https://www.docker.com/products/docker-desktop) or Docker for Linux

- [Ansible](https://ansible.com) >= v2.9.10 

```shell
pip3 install \
  -r https://raw.githubusercontent.com/kameshsampath/ansible-role-kind/master/requirements.txt
ansible-galaxy role install kameshsampath.kind
```
__NOTE__: For Windows its recommended to use Windows Subsystem for Linux (WSL)

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
|extra_port_mappings| Extra Port Mappings for KinD. A YAML list of format `listen-address:hostPort:containerPort` | '0.0.0.0:80:80', '0.0.0.0:443:443' |


Example Playbooks
----------------
The [examples](https://github.com/kameshsampath/ansible-role-kind/tree/master/examples) directory has various playbook examples to get started using this role

License
-------

[Apache v2](https://github.com/kameshsampath/ansible-role-kind/tree/master/LICENSE)

Author Information
------------------

[Kamesh Sampath](mailto:kamesh.sampath@hotmail.com)

Issues
=======

[Issues](https://github.com/kameshsampath/ansible-role-kind/issues)

Testing
=======

Requirements
------------
- Extra Python modules
```shell
pip3 install \
  -r https://raw.githubusercontent.com/kameshsampath/ansible-role-kind/master/molecule/requirements.txt
```

All tests are built using [molecule](https://molecule.readthedocs.io/en/latest/index.html) with following scenarios:

* default 
```shell
molecule test
```
* pre_reqs
```shell
molecule test -s pre_reqs
```
* pre_reqs_local
```shell
molecule test  -s pre_reqs_local
```

