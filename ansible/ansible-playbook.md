---
layout: default
parent: ANSIBLE
nav_order: 2
---
# Ansible Playbook

Ansible playbooks can be run using `ansible-playbook` command as follows:-

```shell
ansible-playbook -i <inventory_file/server_list> -u <user for ssh proxy> <playbook>
```

More cli options are listed [here.](https://docs.ansible.com/ansible/latest/cli/ansible-playbook.html)

## Example 1:-

Create a file `test.yml` with below code for ping module.

```yml
---
    - name: Test Playbook
      hosts: all
      gather_facts: false
      tasks:
        - name: Test task
          ping:
```

Now, run below command to execute the playbook

```shell
ansible-playbook -i ssh_server, -u ssh_user test.yml
```

## Example 2:-

Create a file `test.yml` with below code for `command` module. `ansible-playbook` does not print returned values. So, output is registered to a variable and printed.

{% raw %}
```yml
---
    - name: Test Playbook
      hosts: all
      gather_facts: false
      tasks:
        - name: Test task
          command: date
          register: cur_date

        - name: Print Output 2
          debug:
            msg: "{{cur_date.stdout}}"
```
{% endraw %}

Now, run below command to execute the playbook

```shell
ansible-playbook -i ssh_server, -u ssh_user test.yml
```
