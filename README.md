# Rancher

Install Rancher on a Kubernetes cluster.

[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-rancher-blue.svg)](https://galaxy.ansible.com/ui/standalone/roles/rmasters270/rancher)

## Requirements

### Localhost

The role is intended to run from the Ansible controller.  If the playbook is executed on a different host it will fail because the templates must be copied to the target host.

### Kube Config

The host and user running the playbook must have kube config configured.

### Helm

The host must have the Helm package manager installed.

## Role Variables

| Variable                   | Required | Default                                             | Choices             | Comments                                             |
| -------------------------- | -------- | --------------------------------------------------- | ------------------- | ---------------------------------------------------- |
| heimdall_namespace         | yes      | heimdall                                            |                     | Kubernetes namespace                                 |
| rancher_repo_name          | yes      | rancher-stable                                      |                     | Helm repository name                                 |
| rancher_repo_url           | yes      | <https://releases.rancher.com/server-charts/stable> | Helm repository URL |                                                      |
| rancher_repo_version       | yes      | 2.7.6                                               |                     | Helm chart version                                   |
| rancher_hostname           | yes      | rancher.{{ ansible_domain }}                        |                     | For ssl certificates and ingress routes              |
| rancher_tls                | no       | ingress                                             | ingress, external   | Use `external` if a load balancer will terminate TLS |
| rancher_bootstrap_password | no       | SuperSecretBootStrapPassword                        |                     | Password to login to Rancher the first time          |

## Dependencies

Use `rmasters270.helm` role or install `kubernetes cli` and `helm` manually on the host.

Setup `kube config` for the user account and host.

## Example Playbook

```yaml
- hosts: localhost

  vars:
    rancher_bootstrap_password: your-random-password

  roles:
    - rmasters270.helm
    - rmasters270.rancher
```

## License

MIT

## Author Information

Ryan Masters
