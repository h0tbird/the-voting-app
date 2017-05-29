#### Package:

```
helm package .
```

#### Login:

```
helm registry login -u <user> quay.io
```

#### Publish:

```
helm registry push --namespace <namespace> --channel <channel> quay.io
```

#### Install:

From current directory:
```
helm install --namespace thevotingapp --name thevotingapp .
```

From a registry:
```
helm registry install quay.io/<namespace>/thevotingapp
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
