proxmox_lxc
=========

Install a [Proxmox](https://www.proxmox.com/) based [LXC](https://linuxcontainers.org/) container.

Requirements
------------

Run this role on your Proxmox server(s) as host. If you specify a group of multiple servers, the LXC container will only be installed once due to `run_once: true` in all tasks.

Role Variables
--------------

*vars/main.yaml* contains
* `debiantemplate`
* `ubuntultstemplate`
* `ubuntutemplate`
* `fedoratemplate`

Change the values of these variables to the paths to the different LXC templates.

Example:
```YAML
debiantemplate: '{{ cttemplatestor }}:vztmpl/debian-11-standard_11.0-1_amd64.tar.gz'
```

Look at *defaults/main.yaml* for variables to use in your playbooks.

* `distribution` The distribution. Choose from **debian**, **ubuntu**, **ubuntults** or **fedora**. Defaults to **debian**.
* `proxmoxhost` The (**not FQDN**) hostname of your Proxmox server. This can be the server 
* `proxmoxdomain`: 'alvin.be'
* `cttemplatestor`: 'shai-hulud'
* `ostemplate`: "{{ ubuntutemplate if distribution == 'ubuntu' else ubuntultstemplate if distribution == 'ubuntults' else debiantemplate if distribution == 'debian' else fedoratemplate if distribution == 'fedora'}}"
* `storage`: 'local-zfs'
* `notes`: 'Ansible node on {{ distribution }}'
* `cpuunits`: '1024' # Default: 1024
* `vlan`: '4'
* `mknod`: false            # set mknod to true and unprivileged to no when e.g. OpenConnect is needed
* `ppp`: false              # allow ppp for openfortivpn
* `unprivileged`: true      # 'no' or 'yes'
* `nesting`: false          # 'no' or 'yes' (only when unprivileged=0)
* `ct_password`: "{{ proxmox_password }}"
* `permitrootlogin`: no
* `lxcdomain`: 'howest.serverhamster.be'
* `netif`: '{"net0":"name=eth0,ip=dhcp,ip6=auto,bridge=vmbr0,tag={{ vlan }}"}'
* `lxcnameserver`: '192.168.104.2'
* `memory`: '1024'
* `swap`: '256'
* `cores`: '1'
* `disksize`: '4'           # disk Size of the root filesystem in Gigabytes


Example Playbook
----------------

    - hosts: proxmox
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

This role was created in 2021 by Alvin Demeyer.
