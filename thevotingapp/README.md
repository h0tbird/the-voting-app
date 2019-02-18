Minikube
--------

#### Create:
```
minikube config set memory 4096
minikube config set cores 2
minikube start
minikube addons enable ingress
minikube mount ${PWD}:/git/the-voting-app
minikube dashboard
```

#### Install the tiller:
```
helm init
```

GKE
---

#### Create:
```
gcloud beta container \
--project "john-brown" \
clusters create "kube-1" \
--zone "europe-north1-a" \
--cluster-version "1.11.7-gke.4" \
--machine-type "n1-standard-2" \
--image-type "COS" \
--disk-type "pd-standard" \
--disk-size "30" \
--scopes \
"https://www.googleapis.com/auth/devstorage.read_only",\
"https://www.googleapis.com/auth/logging.write",\
"https://www.googleapis.com/auth/monitoring",\
"https://www.googleapis.com/auth/servicecontrol",\
"https://www.googleapis.com/auth/service.management.readonly",\
"https://www.googleapis.com/auth/trace.append" \
--preemptible \
--num-nodes "1" \
--no-enable-cloud-logging \
--no-enable-cloud-monitoring \
--no-enable-basic-auth \
--no-issue-client-certificate \
--enable-ip-alias \
--network "projects/john-brown/global/networks/default" \
--subnetwork "projects/john-brown/regions/europe-north1/subnetworks/default" \
--metadata disable-legacy-endpoints=true \
--default-max-pods-per-node "110" \
--addons HorizontalPodAutoscaling,HttpLoadBalancing \
--no-enable-autoupgrade \
--no-enable-autorepair
```

#### Install the tiller:
```
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
helm init --service-account tiller --upgrade
```

Packaging
---------

#### Package the Helm Chart:

```
helm package .
```

#### Install the Helm Registry plugin:
```
mkdir -p ~/.helm/plugins
cd ~/.helm/plugins
git clone https://github.com/app-registry/appr-helm-plugin.git registry
helm registry --help
```

#### Helm registry login:
```
helm registry login -u h0tbird quay.io
```

#### Publish the Helm Chart:

```
helm registry push --namespace h0tbird --channel stable quay.io
```

#### List Helm Charts from h0tbird org:
```
helm registry list -o h0tbird quay.io
```

Install
-------

#### Install (deploy to k8s):

From the current directory:
```
helm install \
--namespace thevotingapp \
--name thevotingapp .
```

Same but setting the environment to `devel`:
```
helm install \
--namespace thevotingapp \
--name thevotingapp \
--set environment=devel .
```

From the registry:
```
helm registry install \
quay.io/h0tbird/thevotingapp -- \
--namespace thevotingapp \
--name thevotingapp
```

Same but setting the environment to `devel`:
```
helm registry install \
quay.io/h0tbird/thevotingapp -- \
--namespace thevotingapp \
--name thevotingapp \
--set environment=devel
```

#### Upgrade:

```
helm upgrade thevotingapp . \
--set postgres.image.tag=aaa \
--set redis.image.tag=eee \
--set results.image.tag=iii \
--set voting.image.tag=ooo \
--set worker.image.tag=uuu
```

#### Delete:

```
helm delete --purge thevotingapp
```
