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

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- SUSE Linux Enterprise 15<sup>1</sup>
- openSUSE Leap 15
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Ubuntu 24.04 LTS
- Fedora 39
- Fedora 40

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
