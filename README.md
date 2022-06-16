# Rancher

Install Rancher on a Kubernetes cluster.

## Requirements

### Localhost

The role is intended to run from the Ansible controller.  If the playbook is executed on a different host it will fail because the templates must be copied to the target host.

### Kube Config

The host and user running the playbook must have kube config configured.

### Helm

The host must have the Helm package manager installed.

## Role Variables

### rancher_hostname

Used to issue ssl certificates and ingress routes.  You should also have a DNS entry pointing to this hostname.

default: `rancher.{{ ansible_domain }}`

### rancher_bootstrap_password

Use this password to login to Rancher the first time.

default: `SuperSecretBootStrapPassword`

### rancher_tls

Use `external` if an external load balancer such as Traefik or NGINX will terminate tls.

default: `ingress`

### rancher_repo_name

Name of the Helm repository.

default: `rancher-stable`

### rancher_repo_url

Url pointing to the Helm repository.

default: `https://releases.rancher.com/server-charts/stable`

### rancher_repo_version

Chart version in the repository.

The default value is pinned to the latest version at the time of writing.  Use `helm search repo rancher-stable` to list all versions of the chart.

default: `2.6.5`

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
