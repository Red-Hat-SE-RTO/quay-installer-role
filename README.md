Quay Installer Role
=========

The quay installer role will install the quay operator using ansible.

Requirements
------------

* OpenShift Cluster
* Cluster that can support [ODF](https://www.redhat.com/en/technologies/cloud-computing/openshift-data-foundation)
* pip3 plugins
```
pip3 install kubernetes
pip3 install openshift
```
* Ansible Collections
```
 ansible-galaxy install -r requirements.yml
```

Role Variables
--------------
Type  | Description  | Default Value
--|---|--
config_location | Location of config files |  "/tmp/"
openshift_token | OpenShift login token | 1234567890
openshift_url | OpenShift target url | https://api.ocp4.example.com:6443
insecure_skip_tls_verify | Default insecure tls verify | false
domain | Default domain url for quay route | ocp4.example.com
quay_project_name | Default target project | "quay-enterprise"
quay_csv | Default Quay Operator version | "red-hat-quay.v3.5.6"
quay_channel | Default Quay Operator Channel | "stable-3.6"
quay_urlprefix | Default Quay route prefix | "quayecosystem-quay-{{ quay_project_name }}"
quay_pull_user | Default Quay pull user | changeme
quay_pull_password | Default Quay pull secret | changeme
quay_admin_user | Default quay user | admin
quay_admin_password | Default Quay Admin  password | admin123
oc_version | Current OpenShift Version | 4.8 
delete_deployment | delete the quay deployment | false

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

**Quay 3.6 Install**
```
---
- hosts: localhost
  gather_facts: true
  connection: local


  tasks:
  - import_role:
      name: quay-installer-role
    vars:
      openshift_url: https://api.ocp4.example.com:6443
      openshift_token: sha256~xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
      insecure_skip_tls_verify: false
      delete_deployment: false 
      domain: ocp4.example.com
      quay_urlprefix: "quayecosystem-quay-{{ quay_project_name }}"
      quay_csv: "quay-operator.v3.6.0"
      quay_channel: "stable-3.6"
```

**Quay 3.5 Install**
```
---
- hosts: localhost
  gather_facts: true
  connection: local


  tasks:
  - import_role:
      name: quay-installer-role
    vars:
      openshift_url: https://api.ocp4.example.com:6443
      openshift_token: sha256~xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
      insecure_skip_tls_verify: Location of config files |false
      delete_deployment: Location of config files |false 
      domain: ocp4.example.com
      quay_urlprefix: "quayecosystem-quay-{{ quay_project_name }}.router-default"
      quay_csv: "red-hat-quay.v3.5.6"
      quay_channel: "quay-v3.5"
```

License
-------

BSD

Author Information
------------------
This role was created in 2021 by [Tosin Akinosho](https://github.com/tosin2013)
