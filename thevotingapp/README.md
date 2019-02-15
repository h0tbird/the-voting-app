#### Minikube:
```
minikube config set memory 4096
minikube config set cores 2
minikube start
minikube dashboard
```

#### Install the tiller:
```
helm init
```

#### Package:

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

#### Registry login:
```
helm registry login -u h0tbird quay.io
```

#### Publish:

```
helm registry push --namespace h0tbird --channel stable quay.io
```

#### List:
```
helm registry list -o h0tbird quay.io
```

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

From a registry:
```
helm registry install \
quay.io/h0tbird/thevotingapp -- \
--namespace thevotingapp \
--name thevotingapp \
--set environment=devel
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
