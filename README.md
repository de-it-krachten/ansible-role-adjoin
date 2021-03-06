[![CI](https://github.com/de-it-krachten/ansible-role-adjoin/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-adjoin/actions?query=workflow%3ACI)


# ansible-role-adjoin

Enrolls a Linux host into a Microsoft Active Directory Domain using Kerberos


## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# AD realm
ad_realm: example.com

# Command used for joing host to AD
adjoin_command: realm

# Kerberos Service Principal Name (SPN) to create (keytabs)
adjoin_spn:
  - nfs
  - cifs

# Configure AD connection using SSL/TLS
ad_tls: true

# Leave the AD realm before joining it
ad_leave: false

# Use AD provided UID/GID
ad_ldap_id_mapping: true
</pre></code>

### vars/family-RedHat.yml
<pre><code>
adjoin_packages:
  - sssd
  - realmd
  - oddjob
  - oddjob-mkhomedir
  - adcli
  - samba-common
  #- samba-common-tools
  - krb5-workstation
  - openldap-clients
  #- policycoreutils-python
</pre></code>

### vars/family-Debian.yml
<pre><code>
adjoin_packages:
  - realmd
  - libnss-sss
  - libpam-sss
  - sssd
  - sssd-tools
  - adcli
  - samba-common-bin
  - oddjob
  - oddjob-mkhomedir
  - packagekit
  - krb5-user
</pre></code>



## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'adjoin'
  hosts: all
  become: "{{ molecule['converge']['become'] | default('yes') }}"
  vars:
    ad_password: test
    ad_realm: example.com
    ad_user: test
  tasks:
    - name: Include role 'adjoin'
      include_role:
        name: adjoin
</pre></code>
