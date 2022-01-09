# Kinder

## Cluster Creation

This cluster is based on [kind](https://kind.sigs.k8s.io/). The config file that kind consumes, to create the cluster, is located in the root of the repo.

By using this file kind will create a 6 node cluster(1 master + 5 workers).

To create the cluster we run:

```bash
git clone https://github.com/diskmanti/kinder.git
cd kinder
kind crete cluster --config=kinder.yaml
```

## Repo Structure

The whole cluster and the tweet application are installed, managed, deployed and configured using a GitOps approach.
The structure of the repo is as shown below:

```bash
kinder/
├── applications
├── bootstrap
├── components
```

### Bootstrap

The initial cluster bootstrap resides in the _bootstrap_ folder.
In this folder all the yaml files necessary to deploy ArgoCD on the cluster are stored.

### Applications

The chosen GitOps approach is the _AppOfApps_ approach. There is a main app called __cluster-config__
which itself manages all the ArgoCD application that configure the different application deployed on the cluster.

### Components

In this folder are stored all the yaml files which are needed to deployed the relevant application on the cluster.
ingress-nginx, cert-manager and the tweet app are all found here in their respective folders. These folders are
referenced by the ArgoCD applications defined in the components folder.

## Cluster Bootstrap

The cluster is bootstraped using GitOps and the ArgoCD application.

First of all we need to install ArgoCD. All the required files for installing ArgoCD are located in the bootstrap folder.

ArgoCD is installed by running:

```bash
kubectl apply -k bootstrap/overlays
```

### AppOfApps

All the applications deployed on the cluster are managed using the [AppOfApps](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/#app-of-apps) approach.

The cluster configuration is kickstarted by the cluster-config application, which is also named cluster-config.

To create this ArgoCd application we apply the required yamls:

```bash
kubectl apply -k applictions/bases
```

By creating this application nginx-ingress and cert-manager will be installed and configured in the cluster automatically.

## Linux_Tweet_App

All the source code for this app is located under linux_tweet_app folder.

This app was build using podman and pushed to dockerhub:

```bash
podman build -f /linux_tweet_app/Dockerfile --tag linux_tweet_app
podman tag localhost/linux_tweet_app diskmanti/linux_tweet_app:v1
podman push diskmanti/linux_tweet_app:v1
```

## The Reason Why?

- Kubernetes(Kind) - This is the chosen container orchestration app. Kind was chosen because
is a very lightweight and simple K8S distro to run locally for dev and test purposes.
- Automation - The automation tool chosen is ArgoCD. Since the platform were we are going to deploy the
app is K8S the best apprach, based on my POV, is the GitOps way. ArgoCD is one of the most reliable and
battle tested solution to implement GitOps workflow.
- Tools - The only tool used is Kustomize. Kustomize is a yaml patch engine that integrates very well with ArgoCD.