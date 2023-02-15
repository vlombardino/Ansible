Create folders in Windows
```yaml
---
- name: WinVm
  hosts: win
  connection: winrm
  vars:
    user: build
  tasks:
  - name: Create folder in winvm.
    win_file:
      path: C:\Users\admin\test
      state: directory

  - name: Show folder in vm home directory.
    win_shell: ls C:\Users\{{ user }}\
    register: show_tables
  - debug: msg="{{ show_tables.stdout_lines }}"
```