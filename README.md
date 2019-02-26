# openshift-provision-example-0

This repository shows a simple all-in-one declarative use of the
openshift-provision ansible role using the openshift-provision-manager. In
this example all configuration is given directly in the config map vars and
so no external integration with git is required.  This use case may be useful
if you intend to write your own automation to push changes to the configmap
rather than having the openshift-provision-manager pull updates from git.

## Installation

As a cluster administrator:

```
oc process -f install-template-admin.yaml | oc create -f -
```

If installing as a non-administrator with the openshift-provision-manager
deployed in the namespace "example-provisioner":

```
PROVISIONER_NAMESPACE=example-provisioner
oc process  -f install-template-nonadmin.yaml \
 -p OPENSHIFT_PROVISION_NAMESPACE=$PROVISIONER_NAMESPACE \
| oc create -f -
```

## Local Testing

An Ansible playbook, `playbook.yaml`, is provided for testing outside of
openshift-provision-manager. To use this playbook you will need to have the
[openshift-provision](https://github.com/gnuthought/ansible-role-openshift-provision)
ansible module installed locally. To run the playbook, first login to your
cluster with `oc login` and then run:

```
ansible-playbook playbook.yaml
```

To run in check mode and collect a change record:

```
ansible-playbook playbook.yaml --check -e openshift_provision_change_record=changes.yaml
```
