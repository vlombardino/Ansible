Encrypt `Pass@123` string with the name password
```
ansible-vault encrypt_string "Pass@123" --name password

ansible-playbook --ask-vault-password playbook.yml
```