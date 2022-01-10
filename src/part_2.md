# Repo Structure

The whole cluster and the tweet application are installed, managed, deployed and configured using a GitOps approach.
The structure of the repo is as shown below:

```bash
kinder/
├── applications
├── bootstrap
├── components
```

## Bootstrap

The initial cluster bootstrap resides in the _bootstrap_ folder.
In this folder all the yaml files necessary to deploy ArgoCD on the cluster are stored.

## Applications

The chosen GitOps approach is the _AppOfApps_ approach. There is a main app called __cluster-config__
which itself manages all the ArgoCD application that configure the different application deployed on the cluster.

## Components

In this folder are stored all the yaml files which are needed to deployed the relevant application on the cluster.
ingress-nginx, cert-manager and the tweet app are all found here in their respective folders. These folders are
referenced by the ArgoCD applications defined in the components folder.
