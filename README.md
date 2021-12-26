# k3s role

An opinionated Ansible role, that install (and configures) k3s lightweight distribution of Kubernetes.

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
          version: "1.22.5+k3s1"
          url: https://node.example.org:6443 
          token: PjnYgQVXgMJecoDVP6kigghtLGIbuJIk9t9Ozg+quwPjnYgQVXgMJecoDVP6kigghtLGIbuJIk9t9Ozg+quwY
        k3s_s3:
          host: minio.example.org
          access_key: minioadmin
          secret_key: minioadmin
          region: neverland
          bucket: k3s
          folder: etcd
        k3s_registries: |
          mirrors:
            "registry.example.org:5000":
              endpoint:
                - "http://registry.example.org:5000"
```
