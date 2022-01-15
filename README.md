[![CI](https://github.com/de-it-krachten/ansible-role-adjoin/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-adjoin/actions?query=workflow%3ACI)


# ansible-role-adjoin

Enrolls a Linux host into a Microsoft Active Directory Domain using Kerberos


Platforms
--------------

Supported platforms

- CentOS 7
- CentOS 8
- RockyLinux 8
- AlmaLinux 8
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS



Role Variables
--------------
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


Example Playbook
----------------

<pre><code>
- name: Converge
  hosts: all
  vars:
    ad_password: test
    ad_realm: example.com
    ad_user: test
  tasks:
    - name: Include role 'ansible-role-adjoin'
      include_role:
        name: ansible-role-adjoin
</pre></code>
