Create `api_key.yml` YAML file
```yml
myapp_api_key: "Pass@123"
```

Encrypt password in `api_key.yml`
```
ansible-vault encrypt vars/api_key.yml
```

Edit password in `api_key.yml`
```
ansible-vault edit vars/api_key.yml
```

Change password in `api_key.yml`
```
ansible-vault rekey vars/api_key.yml
```

Create `main.yml` YAML file
```yml
---
- hosts: localhost
  connection: local
  gather_facts: no

  vars_files:
    - vars/api_key.yml

  tasks:
    - name: Echo API key
      shell: echo $API_KEY
      environment:
        API_KEY: "{{ myapp_api_key }}"
      register: echo_result

    - name: show result
      debug: var=echo_result.stdout
```

Run `main.yml` playbook
```
ansible-playbook main.yml --ask-vault-pass
```

Encrypt `Pass@123` string with the name password
```
ansible-vault encrypt_string "Pass@123" --name password

ansible-playbook --ask-vault-password playbook.yml
```