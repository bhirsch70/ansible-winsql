ansible-winsql
===============
Install Microsoft SQLserver 2014 Express

Summary
--------
This playbook will install SQLServer 2014 Express on a AWS EC2 Windows 2016 server

Prerequisities
----------------
- Creation of an ansible-vault encrypted string to seed the `admin_pass` variable.  See [ansible-vault encrypt_string](https://docs.ansible.com/ansible/2.4/vault.html#use-encrypt-string-to-create-encrypted-variables-to-embed-in-yaml)
- This encrypted string must match the `Administrator` password on the target node

Example Playbook execution
-------------------------
`ansible-playbook site.yml -e @extra_vars.yml --ask-vault-pass`

extra variables
---------------
This playbook expects an extra variables file so that a user of this playbook can create their own `Administrator` password (as required).

|Varible Name | Description | default|
|-------------|-------------|--------|
|ansible_password:|Password for the Windows Server Administrator account| "{{ admin_pass }}"
|admin_pass:|`encrypted_string`|N/A|

group_vars
-----------
|Variable | Description | Default |
|----|-------------|---------|
|ansible_user: |Account ansible will use to login| Administrator|
|ansible_port: |Port for ansible connection |5986|
|ansible_connection: | ansible connection method| winrm|
|ansible_winrm_server_cert_validation:| Method to skip using certs| ignore|

role
--------
This playbook uses a role from ionut-maxim to install SQLserver 2014 Express
[ionut-maxim.win_sqlexpress2014](https://galaxy.ansible.com/ionut-maxim/win_sqlexpress2014/)


Example playbook
-----------
```
---
- name: Install Microsoft SQL Express 2014
  hosts: all

  roles:
    - ionut-maxim.win_sqlexpress2014
```

License
-------
BSD
