# freeipa-on-openshift
Manifest files to install FREEIPA on OpenShift
## Define
oc apply -f freeipa-server-openshift.yml

## View
oc process --parameters freeipa-server
## Run
oc process freeipa-server \
    -p IPA_SERVER_HOSTNAME=<PUT IT HERE> \
    -p IPA_ADMIN_PASSWORD=RedHat123 \
    -p IPA_SERVER_IMAGE=freeipa-server:rhel-7 \
    -p TIMEOUT=1200 | oc create -f -

## Altogether
oc apply -f freeipa-server-openshift.yml
oc process freeipa-server \
    -p IPA_SERVER_HOSTNAME=<PUT IT HERE> \
    -p IPA_ADMIN_PASSWORD=RedHat123 \
    -p IPA_SERVER_IMAGE=freeipa-server:rhel-7 \
    -p TIMEOUT=1200 | oc create -f -

## Destroy
oc delete replicationcontroller/freeipa-server-1
oc delete service/freeipa-server
oc delete deploymentconfig.apps.openshift.io/freeipa-server
oc delete route.route.openshift.io/freeipa-server-https
oc delete pvc/freeipa-server
oc delete secret/freeipa-server-password
oc delete all -l free-ipa
