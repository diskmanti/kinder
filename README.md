# Kinder

## Cluster Creation

This cluster is based on [kind](https://kind.sigs.k8s.io/). The config file that kind consumes,to create the cluster, is located in the root of the repo.

By using this file kind will create a 6 node cluster(1 master + 5 workers).

To create the cluster we run:

```bash
git clone https://github.com/diskmanti/kinder.git
cd kinder
kind crete cluster --config=kinder.yaml
```

## Cluster Bootstrap

The cluster is bootstraped using GitOps and the ArgoCD application.

First of all we need to install ArgoCD. All the required files for installing ArgoCD are located in the bootstrap folder.

ArgoCD is installed by running:

```bash
kubectl apply -k bootstrap/overlays
```

### AppOfApps

All the applications deployed on the cluster are managed using the AppOfApps approach.

The cluster configuration is kickstarted by the cluster-config application, which is also named cluster-config.

To create this ArgoCd application we apply the required yamls:

```bash
kubectl apply -k applictions/bases
```
