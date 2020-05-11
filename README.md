# ocp4-install
'''
export BUILDNUMBER=$(curl -s https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest/release.txt | grep 'Name:' | awk '{print $NF}')
export BUILDNUMBER=$(curl -s https://mirror.openshift.com/pub/openshift-v4/clients/ocp/stable/release.txt | grep 'Name:' | awk '{print $NF}')

echo ${BUILDNUMBER}

https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/latest/latest/



https://docs.openshift.com/container-platform/4.4/installing/install_config/installing-restricted-networks-preparations.html

- 4.3 ---------------------------------------------------------------------
export OCP_RELEASE=4.3.13-x86_64
export LOCAL_REGISTRY='registry.mwocp.com:5000'
export LOCAL_REPOSITORY='ocp4/openshift4'
export PRODUCT_REPO='openshift-release-dev'
export LOCAL_SECRET_JSON='/root/pull-secret-2.json'
export RELEASE_NAME="ocp-release"

 
oc adm -a ${LOCAL_SECRET_JSON} release mirror \
--from=quay.io/${PRODUCT_REPO}/${RELEASE_NAME}:${OCP_RELEASE} \
--to=${LOCAL_REGISTRY}/${LOCAL_REPOSITORY} \
--to-release-image=${LOCAL_REGISTRY}/${LOCAL_REPOSITORY}:${OCP_RELEASE 
---------------------------------------------------------------------
Success
Update image:  registry.mwocp.com:5000/ocp4/openshift4:4.3.13-x86_64
Mirror prefix: registry.mwocp.com:5000/ocp4/openshift4

To use the new mirrored repository to install, add the following section to the install-config.yaml:

imageContentSources:
- mirrors:
  - registry.mwocp.com:5000/ocp4/openshift4
  source: quay.io/openshift-release-dev/ocp-release
- mirrors:
  - registry.mwocp.com:5000/ocp4/openshift4
  source: quay.io/openshift-release-dev/ocp-v4.0-art-dev


To use the new mirrored repository for upgrades, use the following to create an ImageContentSourcePolicy:

apiVersion: operator.openshift.io/v1alpha1
kind: ImageContentSourcePolicy
metadata:
  name: example
spec:
  repositoryDigestMirrors:
  - mirrors:
    - registry.mwocp.com:5000/ocp4/openshift4
    source: quay.io/openshift-release-dev/ocp-release
  - mirrors:
    - registry.mwocp.com:5000/ocp4/openshift4
    source: quay.io/openshift-release-dev/ocp-v4.0-art-dev


- 4.4 ---------------------------------------------------------------------
export OCP_RELEASE=4.4.0-x86_64
export LOCAL_REGISTRY='registry.mwocp.com:5000'
export LOCAL_REPOSITORY='ocp4/openshift44'
export PRODUCT_REPO='openshift-release-dev'
export LOCAL_SECRET_JSON='/root/pull-secret-2.json'
export RELEASE_NAME="ocp-release"


oc adm -a ${LOCAL_SECRET_JSON} release mirror \
--from=quay.io/${PRODUCT_REPO}/${RELEASE_NAME}:${OCP_RELEASE} \
--to=${LOCAL_REGISTRY}/${LOCAL_REPOSITORY} \
--to-release-image=${LOCAL_REGISTRY}/${LOCAL_REPOSITORY}:${OCP_RELEASE}
---------------------------------------------------------------------
Success
Update image:  registry.mwocp.com:5000/ocp4/openshift44:4.4.0-x86_64
Mirror prefix: registry.mwocp.com:5000/ocp4/openshift44

To use the new mirrored repository to install, add the following section to the install-config.yaml:

imageContentSources:
- mirrors:
  - registry.mwocp.com:5000/ocp4/openshift44
  source: quay.io/openshift-release-dev/ocp-release
- mirrors:
  - registry.mwocp.com:5000/ocp4/openshift44
  source: quay.io/openshift-release-dev/ocp-v4.0-art-dev


To use the new mirrored repository for upgrades, use the following to create an ImageContentSourcePolicy:

apiVersion: operator.openshift.io/v1alpha1
kind: ImageContentSourcePolicy
metadata:
  name: example
spec:
  repositoryDigestMirrors:
  - mirrors:
    - registry.mwocp.com:5000/ocp4/openshift44
    source: quay.io/openshift-release-dev/ocp-release
  - mirrors:
    - registry.mwocp.com:5000/ocp4/openshift44
    source: quay.io/openshift-release-dev/ocp-v4.0-art-dev
---------------------------------------------------------------------

openshift-install create manifests --dir=/root/mwocp-install/
openshift-install create ignition-configs --dir=/root/mwocp-install
#openshift-install --dir=/root/mwocp-install/ create cluster
openshift-install --dir=/root/mwocp-install wait-for bootstrap-complete --log-level=debug

---------------------------------------------------------------------
openssl s_client -connect api-int.mwocp.com:6443 | openssl x509 -noout -text
openssl s_client -connect api.mwocp.com:6443 | openssl x509 -noout -text
openssl s_client -connect localhost:6443 | openssl x509 -noout -text
---------------------------------------------------------------------

https://docs.openshift.com/container-platform/4.3/machine_management/adding-rhel-compute.html


  nodePlacement:
    nodeSelector:
      matchLabels:
        node-role.kubernetes.io/infra: ""

https://docs.openshift.com/container-platform/4.4/machine_management/creating-infrastructure-machinesets.html        
'''
