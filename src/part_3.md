# Cluster Bootstrap

The cluster is bootstraped using GitOps and the ArgoCD application.

First of all we need to install ArgoCD. All the required files for installing ArgoCD are located in the bootstrap folder.

ArgoCD is installed by running:

```bash
kubectl apply -k bootstrap/overlays
```

## AppOfApps

All the applications deployed on the cluster are managed using the [AppOfApps](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/#app-of-apps) approach.

The cluster configuration is kickstarted by the cluster-config application, which is also named cluster-config.

To create this ArgoCd application we apply the required yamls:

```bash
kubectl apply -k applictions/bases
```

By creating this application nginx-ingress and cert-manager will be installed and configured in the cluster automatically.
