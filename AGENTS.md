# CLAUDE.md

This public repository is the Flux source for `getcolors/k8s` and the
`k8s-digitalocean` deployment. It contains no credentials and receives no
kubeconfig.

`clusters/k8s-digitalocean/` creates three ordered Flux Kustomizations:
controllers, configuration, and applications. Controllers install pinned
 ingress-nginx, cert-manager, and ExternalDNS releases. Configuration creates a
Let's Encrypt HTTP-01 issuer. The application serves
`https://hello.bigconfig.online` and `/healthz`.

Keep the workload non-root, capability-free, read-only, and resource-bounded.
ExternalDNS references the `cloudflare-api-token` Secret bootstrapped by the
Package Skill; never add plaintext secrets. The ingress-nginx LoadBalancer is
owned by Kubernetes and must remain deletable before cluster infrastructure.

Validate every Kustomize root and keep CD pull-based.
