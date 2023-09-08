[![CI](https://github.com/de-it-krachten/ansible-role-adjoin/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-adjoin/actions?query=workflow%3ACI)


# ansible-role-adjoin

Enrolls a Linux host into a Microsoft Active Directory Domain using Kerberos



## Dependencies

#### Roles
None

#### Collections
- community.general
- ansible.windows

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
- Debian 10 (Buster)<sup>1</sup>
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 37
- Fedora 38

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




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'adjoin'
  hosts: all
  become: "yes"
  vars:
    ad_password: test
    ad_realm: example.com
    ad_user: test
  tasks:
    - name: Include role 'adjoin'
      ansible.builtin.include_role:
        name: adjoin
</pre></code>
