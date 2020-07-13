Kind
=========

Ansible to create [KinD](https://kind.sigs.k8s.io) cluster. The role can also be configured to install and configure:

- [x] Default [Ingress](https://kind.sigs.k8s.io/docs/user/ingress/#contour)

- [x] [Knative](https://knative.dev), both Serving and Eventing

- [ ] [Tekton](https://tekton.dev)

Requirements
------------

- Docker Desktop or Docker/Podman for Linux

- Ansible >= v2.9.10 

```shell
pip3 install -U -r requirements.txt
ansible-galaxy collections install -r requirements.yml
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
| deploy_knative | Deploy Knative | False |
| knative_version | The Knative version | v0.16.0 |
| knative_serving_version | The Knative Serving version | v0.16.0 |
| knative_eventing_version | The Knative Eventing version | v0.16.0 |
| deploy_ingress | Deploy Ingress | True |
| ingress_namespace | The namespace for Contour Ingress | contour-system |
| ingress_namespace | The namespace for Contour Ingress | contour-system |
| ingress_manifest  | The Contour Ingress manifest file  | https://projectcontour.io/quickstart/contour.yaml |
|extra_port_mappings| Extra Port Mappings for KinD. A YAML list of format `listen-address:hostPort:containerPort` | '0.0.0.0:80:80', '0.0.0.0:443:443' |


Example Playbooks
----------------
The [examples](./examples) directory has various playbook examples to get started using this role

License
-------

[Apache v2](./LICENSE)

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

```shell
pip3 install molecule yamllint ansible-lint docker
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


* Knative
```shell
molecule test  -s deploy_knative
```

