[![CI](https://github.com/de-it-krachten/ansible-role-adjoin/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-adjoin/actions?query=workflow%3ACI)


# ansible-role-adjoin

Enrolls a Linux host into a Microsoft Active Directory Domain using Kerberos



## Dependencies

#### Roles
None

#### Collections
None

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- Red Hat Enterprise Linux 10<sup>1</sup>
- RockyLinux 8
- RockyLinux 9
- RockyLinux 10
- OracleLinux 8
- OracleLinux 9
- OracleLinux 10
- AlmaLinux 8
- AlmaLinux 9
- AlmaLinux 10
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)
- Debian 13 (Trixie)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Ubuntu 24.04 LTS
- Fedora 41
- Fedora 42

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# AD realm
# adjoin_realm: example.com

# Command used for joing host to AD
adjoin_command: realm

# Kerberos Service Principal Name (SPN) to create (keytabs)
adjoin_spn: []
# adjoin_spn: [ nfs, cifs ]

# Configure AD connection using SSL/TLS
adjoin_tls: true

# Leave the AD realm before joining it
adjoin_leave: false

# Use AD provided UID/GID
adjoin_ldap_id_mapping: true

# SSSD template to use
adjoin_sssd_template: sssd.conf.j2
</pre></code>

### defaults/family-Debian.yml
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

### defaults/family-RedHat.yml
<pre><code>
adjoin_packages:
  - sssd
  - realmd
  - oddjob
  - oddjob-mkhomedir
  - adcli
  - samba-common
  # - samba-common-tools
  - krb5-workstation
  - openldap-clients
  # - policycoreutils-python
</pre></code>

### defaults/family-Suse.yml
<pre><code>
adjoin_packages:
  - krb5-client
  - realmd
  - adcli
  - sssd
  - sssd-ldap
  - sssd-ad
  - sssd-tools
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'adjoin'
  hosts: all
  become: 'yes'
  vars:
    adjoin_password: test
    adjoin_realm: example.com
    adjoin_user: test
  tasks:
    - name: Include role 'adjoin'
      ansible.builtin.include_role:
        name: adjoin
</pre></code>
