[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)

# ansible-role-adjoin

Enrolls a Linux host into a Microsoft Active Directory Domain using Kerberos




Role Variables
--------------

<sub>**variable**</sub> |<sub>**required**</sub> |<sub>**type**</sub> |<sub>**default**</sub> |<sub>**platform**</sub> |<sub>**description**</sub>
:--- |:--- |:--- |:--- |:--- |:---
<sub>adjoin_command<br></sub> |<sub>false<br></sub> |<sub>string<br></sub> |<sub>realm<br></sub> |<sub>all<br></sub> |<sub>Command to use for joining AD<br></sub>
<sub>adjoin_spn<br></sub> |<sub>false<br></sub> |<sub>list<br></sub> |<sub>- nfs<br>- cifs<br></sub> |<sub>all<br></sub> |<sub>Kerberos Service Principal Name (SPN) to create<br></sub>
<sub>ad_tls<br></sub> |<sub>false<br></sub> |<sub>boolean<br></sub> |<sub>true<br></sub> |<sub>all<br></sub> |<sub>Configure AD connection using SSL/TLS<br></sub>
<sub>ad_leave<br></sub> |<sub>false<br></sub> |<sub>boolean<br></sub> |<sub>false<br></sub> |<sub>all<br></sub> |<sub>Leave the AD realm before joining it<br></sub>
<sub>ad_ldap_id_mapping<br></sub> |<sub>false<br></sub> |<sub>boolean<br></sub> |<sub>true<br></sub> |<sub>all<br></sub> |<sub>Use AD provided UID/GID<br></sub>
<sub>adjoin_packages<br></sub> |<sub>false<br></sub> |<sub>list<br></sub> |<sub>- realmd<br>- libnss-sss<br>- libpam-sss<br>- sssd<br>- sssd-tools<br>- adcli<br>- samba-common-bin<br>- oddjob<br>- oddjob-mkhomedir<br>- packagekit<br>- krb5-user<br></sub> |<sub>family-Debian<br></sub> |<sub>null<br></sub>
<sub>adjoin_packages<br></sub> |<sub>false<br></sub> |<sub>list<br></sub> |<sub>- sssd<br>- realmd<br>- oddjob<br>- oddjob-mkhomedir<br>- adcli<br>- samba-common<br>- krb5-workstation<br>- openldap-clients<br></sub> |<sub>family-RedHat-7<br></sub> |<sub>null<br></sub>
<sub>adjoin_packages<br></sub> |<sub>false<br></sub> |<sub>list<br></sub> |<sub>- sssd<br>- realmd<br>- oddjob<br>- oddjob-mkhomedir<br>- adcli<br>- samba-common<br>- krb5-workstation<br>- openldap-clients<br></sub> |<sub>family-RedHat-8<br></sub> |<sub>null<br></sub>



Example Playbook
----------------



<pre><code>
- hosts: all
  roles:
    - ansible-role-adjoin
</pre></code>

