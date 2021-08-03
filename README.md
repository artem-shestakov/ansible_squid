Ansible Squid role
=========

Ansible role to install Squid proxy on Debian/Red Hat OS family.
GitLab [role repository](https://gitlab.com/ansible_code/squid_install).

Requirements
------------
None

Inventory Variables
--------------

* `interface` interface for inside_network, bound by vrrp

Role Variables
--------------

* `http_port` 
  - `port` The socket addresses where Squid will listen for HTTP client request. Default: 3128.
  - `modes`
    - `ssl-bump`
      - `generate-host-certificates` Dynamically create SSL server certificates for the destination hosts of bumped CONNECT requests. Boolean
      - `dynamic_cert_mem_cache_size` Approximate total RAM size spent on cached generated certificates. In MB
* `tmp_directory` - Temporary directory for exchanging certificates between local and remote hosts. Default `/tmp`.


Example Playbook
----------------
Example of setup Squid proxy.

```yaml
---
- name: Install Squid
  hosts: proxy
  remote_user: vagrant
  become: true
  roles:
    - artem-shestakov.squid

```
Squid proxy with ssl-bump
```yaml
---
- name: Install Squid
  hosts: proxy
  remote_user: vagrant
  become: true
  roles:
    - artem-shestakov.squid
  vars:
    http_port:
      port: 3128
      modes:
        ssl-bump:
          generate-host-certificates: true
          dynamic_cert_mem_cache_size: 4MB

```
Inventory file:
```ini
[proxy]
10.0.3.31
```

License
-------
BSD, MIT


Author Information
------------------
Artem Shestakov (artem.s.shestakov@gmail.com)
