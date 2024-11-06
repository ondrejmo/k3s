# Ansible role - k3s

This deploys a turnkey cluster, with all components, hardening and observability required by my use-case. This role is heavily optimized for the following environment:

- Single-node, but multi-cluster. It works for multi-node single-master as well, though without my regular testing. HA use-cases would require additional ETCD initialization step and adjustments in some / many of the components to be truly HA.
- Intel based nodes with core i3 gen 8 (or better / newer)
- Internal CA and local DNS, using RouterOS DNS
- Log collector via Vector.dev protocol
- Metric collector via remote write api

The highlights of the features are:

- Both local and distributed block storage (with CSI snapshots)
- Metric based monitoring (based on [kube-prometheus v0.14.0](https://github.com/prometheus-operator/kube-prometheus/releases/tag/v0.14.0))
- Trivy image and cluster vulnerability scanning
- Automatic DNS records (via [external-dns-provider-mikrotik](https://github.com/mirceanton/external-dns-provider-mikrotik/pkgs/container/external-dns-provider-mikrotik))
- LoadBalancer with L2 annoucements
- Intel GPU operator
- Traefik v3
- Log collection, including:
  - Flows dropped by network policies
  - Kubernetes API audit logs
  - Kubernetes events
  - Kubermetes pod logs
  - CoreDNS query logs
  - System logs of the nodes

## Roadmap

- [ ] add longhorn encrypt storageclass
- [ ] add hostfirewall to cilium
- [ ] make vector-events more extensible (and add trivy webhook)
- [ ] release the [helm charts](https://github.com/ondrejmo/charts) for services in the cluster
- [x] release the [core role](https://github.com/ondrejmo/core) that serves as baseline for k3s nodes (and other use-cases)
- [x] add clis for in cluster components (hubble, ...)
