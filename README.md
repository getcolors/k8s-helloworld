# k8s-helloworld

Public GitOps desired state for the kubeadm cluster created by
[`getcolors/k8s`](https://github.com/getcolors/k8s).

Flux reconciles three ordered layers:

1. ingress-nginx, cert-manager, and ExternalDNS;
2. the Let's Encrypt HTTP-01 issuer;
3. a hardened, non-root hello-world application.

Endpoints:

- <https://hello.bigconfig.online/> — `Hello from kubeadm on DigitalOcean`
- <https://hello.bigconfig.online/healthz> — `ok`

ExternalDNS creates the Cloudflare record from the Ingress after DigitalOcean
CCM assigns the ingress-nginx LoadBalancer address. cert-manager obtains and
renews the TLS certificate. Provider credentials are injected by the Package
Skill into Kubernetes Secrets and never appear here.

```sh
kubectl kustomize clusters/k8s-digitalocean
kubectl kustomize infrastructure/controllers
kubectl kustomize infrastructure/config
kubectl kustomize apps/hello-world
```
