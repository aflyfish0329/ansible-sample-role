# Role Name
## <roles_name>

# Usage
``` shell
export INVENTORY=</path>/<to>/<inventory>
export HN=<host_name>
export PLAYBOOK=<path>/<to>/<playbook>

ansible-playbook -i ${INVENTORY} -e "hn=${HN}" ${PLAYBOOK}
```

# Example Playbook
``` yaml
- hosts: '{{ hn }}'
  roles:
      - role: <roles_name>
```

# Example Inventory
``` ini
[<groupname>]
<hostname> ansible_user=xxxx
<hostname> ansible_user=xxxx
<hostname> ansible_user=xxxx
```

# Variable for use

* please see vars/mapping_variables.yml

# Useage
1. copy sample_roles to ur role name
``` shell
cp samples_roles golang
```

2. replace all <roles_name> to ur role name in

3. rename default distribution folder for tasks and roles
* tasks/distribution/distribution_name
* vars/distribution_name

``` shell
# if os == centos_7
mv golang/tasks/distribution/centos_7_x 
mv golang/vars/distribution_name golang/vars/centos_7_x
```

4. determine default variable u want to use
* vars/default_variables

5. copy variable to defaults/main.yml and add <roles_name> to the variable beginning, then use it.
* <roles_name>_<variable_name>
``` shell
---
golang_required_package:
- name: go
```

6. repeat 5 until all variable u want to use are ready

7. mapping the variables for global use to role variables in mapping_variables.yml
* vars/mapping_variables
``` shell
---
required_package: "{{ golang_required_package }}
```

8. test user role