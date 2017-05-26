#### Package:

```
helm package .
```

#### Install:

```
helm install --namespace thevotingapp --name thevotingapp .
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
