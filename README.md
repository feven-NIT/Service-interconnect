Install the skupper operator in a all namespace

Create a YAML file defining the ConfigMap of the site you want to create.

For example, create skupper-site.yaml that provisions a site with a console:

```shell
apiVersion: v1
kind: ConfigMap
metadata:
  name: skupper-site
  namespace: todo-demo
data:
  console: "true"
  flow-collector: "true"
  console-user: "admin"
  console-password: "changeme"
```

Se connecter a la VM 

```shell
podman run --name postgres-db -e POSTGRES_USER=feven -e POSTGRES_PASSWORD=redhat -p 5432:5432 -d postgres
```

Se connecter au cluster opesnhift puis se mettre dans le namespace auquel on veut acceder

```shell
oc login 
oc project todo-demo
```


On configure ensuite la gateway

```shell
skupper gateway init --type podman
```

Puis on expose le backend
```shell
skupper service create backend 5432
```
