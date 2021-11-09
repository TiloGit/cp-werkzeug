# cp-werkzeug

[![Docker Repository on Quay](https://quay.io/repository/tsombrero/cp-werkzeug/status "Docker Repository on Quay")](https://quay.io/repository/tsombrero/cp-werkzeug)

Cloud Pak tools

based on https://github.com/containers/podman/blob/main/contrib/podmanimage/stable/Dockerfile
see also: https://github.com/noseka1/openshift-toolbox

Consider to use upstream image directly: quay.io/podman/stable

run like this
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: tilo-toolbox
  labels:
    vfowner: tilo
spec:
 containers:
   - name: tilo-toolbox
     image: quay.io/tsombrero/cp-werkzeug
     command:
       - sh
       - -c
       - while true ; do echo alive ; sleep 3600 ; done
     securityContext:
       privileged: true ##needed for podman