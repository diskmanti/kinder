# Cluster Creation

This cluster is based on [kind](https://kind.sigs.k8s.io/). The config file that kind consumes, to create the cluster, is located in the root of the repo.

By using this file kind will create a 6 node cluster(1 master + 5 workers).

To create the cluster we run:

```bash
git clone https://github.com/diskmanti/kinder.git
cd kinder
kind crete cluster --config=kinder.yaml
```
