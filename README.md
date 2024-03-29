# cp-werkzeug

[![Docker Repository on Quay](https://quay.io/repository/tsombrero/cp-werkzeug/status "Docker Repository on Quay")](https://quay.io/repository/tsombrero/cp-werkzeug)

Cloud Pak tools

based on https://github.com/containers/podman/blob/main/contrib/podmanimage/stable/Containerfile
see also: https://github.com/noseka1/openshift-toolbox

Consider to use upstream image directly: quay.io/podman/stable

run like this

cli one-liner (removes after exit)
```bash
###k8s
kubectl run -i --tty tilo-toolbox --image=quay.io/tsombrero/cp-werkzeug -l vfowner=tilo --rm --restart=Never

##docker
docker run -it --entrypoint /bin/bash quay.io/tsombrero/cp-werkzeug
```

yaml file
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
```

or with cat
```bash
cat <<EOF | kubectl apply -f -
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
EOF
```
