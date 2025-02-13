# Ansible role - k3s

This deploys a turnkey cluster, with all components, hardening and observability required by my use-case. This role is heavily optimized for the following environment:

- Multiple non-HA clusters, because the primary goal of this role is efficiency and resiliciency (along with horizontal scaling), not high-availability.
- Intel based nodes with core i3 gen 8 (or better / newer)
  - One NIC
  - Integrated GPU
  - Two drives (NVMe, SATA)
- Internal CA and local DNS, using RouterOS DNS
- Log collector via Vector.dev protocol
- Metric collector via remote write api
- IPv4-only, with IPv6 being disabled only in sysctl, not in kernel parameters, as disabling it at kernel level causes a myriad of annoying problems

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
  - Trivy reports
  - CoreDNS query logs
  - System logs of the nodes
  - ....
