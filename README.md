# k3s role

An opinionated Ansible role, that install (and configures) k3s lightweight distribution of Kubernetes. Following snippet is an example play(book).

```yaml
---

- name: example deployment of k3s role
  hosts: seven-dwarfes
  become: yes
  serial: 1 # so that the quorum is not broken
  roles:
    - role: k3s
      vars:
        k3s:
          version: "1.25.7+k3s1"
          url: https://node.example.org:6443 
          token: PjnYgQVXgMJecoDVP6kigghtLGIbuJIk9t9Ozg+quwPjnYgQVXgMJecoDVP6kigghtLGIbuJIk9t9Ozg+quwY
        k3s_san: 
          - k3s.example.org
```

## Changelog

There are two tagged versions of this role, `v1` which is what I originally relased and `v2` which includes the changes I made after using k3s for almost 2 years. Here is a brief list of differences between the two versions:

  * Fedora support was removed
  * S3 backups support was remove
    * In small scale deployments it's likely that full cluster re-deployment will be easier than recovery when all nodes are lost. If all nodes are not lost, you can use local snapshots on the surviving nodes.
  * NetworkPolicies logging was added (using `ulogd2` and JSON format)
  * Implemented [k3s hardening recommendations](https://docs.k3s.io/security/hardening-guide)
    * Kernel parameter tunning
    * k3s configuration
    * Enabled audit logging
    * Pod Security Standards enable (but lenient for now)
    * *Secret encryption is not enabled for now*
  * Added support TLS SAN parameter
  * Added support for node taints
