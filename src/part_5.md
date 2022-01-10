# The Reason Why?

- Kubernetes(Kind) - This is the chosen container orchestration app. Kind was chosen because
is a very lightweight and simple K8S distro to run locally for dev and test purposes.
- Automation - The automation tool chosen is ArgoCD. Since the platform were we are going to deploy the
app is K8S the best apprach, based on my POV, is the GitOps way. ArgoCD is one of the most reliable and
battle tested solution to implement GitOps workflow.
- Tools - The only tool used is Kustomize. Kustomize is a yaml patch engine that integrates very well with ArgoCD
