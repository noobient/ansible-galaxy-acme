# bviktor.acme

## Synopsys

This role obtains HTTPS certificates using the ACME protocol from Let's Encrypt, the acme.sh utility, and the DNS-01 challenge.

## Parameters

| Name | Required | Example | Description |
|---|---|---|---|
| `domain` | true | `foobar.com` | Domain to obtain certificates for. |
| `provider` | true | `cf` | DNS provider to use. See [How to use DNS API](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) for details. E.g. if the command is `--dns dns_cf`, then this argument should be `cf`. |
| `credential` | true | See in Examples | Dictionary holding all your `export ...` variables, as explained on the above link. |
| `staging` | no | `true` | If `true`, uses staging servers instead of production. Use for testing. Defaults to `false`. |
| `wildcard` | no | `true` | If `true`, obtains not only the base certificate, but the wildcard certificate too, via SAN. E.g. if the domain is `foobar.com`, the certificate will be valid for `*.foobar.com` as well. Defaults to `false`. |
| `cronjob` | no | `true`| If `true`, deploy cronjob to automatically renew the certificate every month. Defaults to `false`. |
| `sleep` | no | `60` | Wait this many seconds for DNS updates to propagate. Defaults to `20`. |

## Examples

```yml
- include_role:
    name: bviktor.acme
  vars:
    domain: foo.com
    provider: cf
    credential:
      CF_Key: 'asdf1234'
      CF_Email: 'foo@bar.com'

- include_role:
    name: bviktor.acme
  vars:
    domain: bar.com
    provider: cf
    credential:
      CF_Token: 'asdf1234'
      CF_Account_ID: 'qwer5678'
      CF_Zone_ID: 'zxcv3456'
    staging: true
    wildcard: true
    cronjob: true
    sleep: 60
```

## Return Values

N/A

## Support

| Platform | Support | Status |
|---|---|---|
| Linter | ✅ | [![Lint](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/lint.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/lint.yml) |
| AlmaLinux 8 | ✅ | [![AlmaLinux 8](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/almalinux-8.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/almalinux-8.yml) |
| AlmaLinux 9 | ✅ | [![AlmaLinux 9](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/almalinux-9.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/almalinux-9.yml) |
| Fedora 37 | ✅ | [![Fedora 37](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/fedora-37.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/fedora-37.yml) |
| Ubuntu 18.04 | ✅ | [![Ubuntu 18.04](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/ubuntu-18.04.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/ubuntu-18.04.yml) |
| Ubuntu 20.04 | ✅ | [![Ubuntu 20.04](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/ubuntu-20.04.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/ubuntu-20.04.yml) |
| Ubuntu 22.04 | ✅ | [![Ubuntu 22.04](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/ubuntu-22.04.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-acme/actions/workflows/ubuntu-22.04.yml) |
