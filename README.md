# openshift-provision-example-0

A simple all-in-one declarative use case. This use case may be useful if you
intend to write your own automation to push changes to the configmap rather
than having the openshift-provision-manager pull updates from git.

## Installation

As a cluster administrator:

```
oc process -f install-template-admin.yaml | oc create -f -
```

If installing an a non-administrator:

```
PROVISIONER_NAMESPACE=example-provisioner
oc new-project $NAMESPACE
oc process  -f install-template-nonadmin.yaml \
 -p OPENSHIFT_PROVISION_NAMESPACE=$PROVISIONER_NAMESPACE \
| oc create -f -
```
