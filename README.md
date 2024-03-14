# Домашнее задание к занятию 2 «Работа с Playbook»

4 -
```bash
SSH password: 
BECOME password[defaults to SSH password]: 
[WARNING]: Found both group and host with same name: vector
[WARNING]: Found both group and host with same name: clickhouse

PLAY [Install Clickhouse] ****************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Get clickhouse distrib 1] **********************************************************************************************************************************************************************************************
ok: [clickhouse] => (item=clickhouse-client)
ok: [clickhouse] => (item=clickhouse-server)
failed: [clickhouse] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 5, "gid": 0, "group": "root", "item": "clickhouse-common-static", "mode": "0777", "msg": "Request failed", "owner": "root", "response": "HTTP Error 404: Not Found", "size": 246310036, "state": "file", "status_code": 404, "uid": 0, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib 2] **********************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Install clickhouse packages] *******************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Flush handlers] ********************************************************************************************************************************************************************************************************

TASK [Create database] *******************************************************************************************************************************************************************************************************
ok: [clickhouse]

PLAY [Install Vector] ********************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************************************************
ok: [vector]

TASK [Get vector distrib] ****************************************************************************************************************************************************************************************************
ok: [vector]

TASK [Install vector packages] ***********************************************************************************************************************************************************************************************
ok: [vector]

TASK [Configure Vector | Ensure config directory exists] *********************************************************************************************************************************************************************
ok: [vector]

TASK [Configure Vector | Template config] ************************************************************************************************************************************************************************************
ok: [vector]

TASK [Vector | change systemd unit] ******************************************************************************************************************************************************************************************
ok: [vector]

PLAY RECAP *******************************************************************************************************************************************************************************************************************
clickhouse                 : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0   
vector                     : ok=6    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
5 -   
Так и не смог побороть одну ошибку:   
```bash
user@study:~/home_work/ansible/ansible-02-playbook$ ansible-lint ./playbook/site.yml 
WARNING  Listing 1 violation(s) that are fatal
name[missing]: All tasks should be named.
playbook/site.yml:11 Task/Handler: block/always/rescue 

Read documentation for instructions on how to ignore specific rule violations.

              Rule Violation Summary              
 count tag           profile rule associated tags 
     1 name[missing] basic   idiom                

Failed: 1 failure(s), 0 warning(s) on 1 files. Last profile that met the validation criteria was 'min'.
```
6 -   
```bash
user@study:~/home_work/ansible/ansible-02-playbook$ ansible-playbook -i ./playbook/inventory/prod.yml ./playbook/site.yml --check -kK
SSH password: 
BECOME password[defaults to SSH password]: 
[WARNING]: Found both group and host with same name: vector
[WARNING]: Found both group and host with same name: clickhouse

PLAY [Install Clickhouse] ****************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Get clickhouse distrib 1] **********************************************************************************************************************************************************************************************
ok: [clickhouse] => (item=clickhouse-client)
ok: [clickhouse] => (item=clickhouse-server)
failed: [clickhouse] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "gid": 0, "group": "root", "item": "clickhouse-common-static", "mode": "0777", "msg": "Request failed", "owner": "root", "response": "HTTP Error 404: Not Found", "size": 246310036, "state": "file", "status_code": 404, "uid": 0, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib 2] **********************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Install clickhouse packages] *******************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Flush handlers] ********************************************************************************************************************************************************************************************************

TASK [Create database] *******************************************************************************************************************************************************************************************************
skipping: [clickhouse]

PLAY [Install Vector] ********************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************************************************
ok: [vector]

TASK [Get vector distrib] ****************************************************************************************************************************************************************************************************
ok: [vector]

TASK [Install vector packages] ***********************************************************************************************************************************************************************************************
ok: [vector]

TASK [Configure Vector | Ensure config directory exists] *********************************************************************************************************************************************************************
ok: [vector]

TASK [Configure Vector | Template config] ************************************************************************************************************************************************************************************
ok: [vector]

TASK [Vector | change systemd unit] ******************************************************************************************************************************************************************************************
ok: [vector]

PLAY RECAP *******************************************************************************************************************************************************************************************************************
clickhouse                 : ok=3    changed=0    unreachable=0    failed=0    skipped=1    rescued=1    ignored=0   
vector                     : ok=6    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
7 -   
```bash
user@study:~/home_work/ansible/ansible-02-playbook$ ansible-playbook -i ./playbook/inventory/prod.yml ./playbook/site.yml --check -kK
SSH password: 
BECOME password[defaults to SSH password]: 
[WARNING]: Found both group and host with same name: vector
[WARNING]: Found both group and host with same name: clickhouse

PLAY [Install Clickhouse] ****************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Get clickhouse distrib 1] **********************************************************************************************************************************************************************************************
ok: [clickhouse] => (item=clickhouse-client)
ok: [clickhouse] => (item=clickhouse-server)
failed: [clickhouse] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "gid": 0, "group": "root", "item": "clickhouse-common-static", "mode": "0777", "msg": "Request failed", "owner": "root", "response": "HTTP Error 404: Not Found", "size": 246310036, "state": "file", "status_code": 404, "uid": 0, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib 2] **********************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Install clickhouse packages] *******************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Flush handlers] ********************************************************************************************************************************************************************************************************

TASK [Create database] *******************************************************************************************************************************************************************************************************
skipping: [clickhouse]

PLAY [Install Vector] ********************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************************************************
ok: [vector]

TASK [Get vector distrib] ****************************************************************************************************************************************************************************************************
ok: [vector]

TASK [Install vector packages] ***********************************************************************************************************************************************************************************************
ok: [vector]

TASK [Configure Vector | Ensure config directory exists] *********************************************************************************************************************************************************************
ok: [vector]

TASK [Configure Vector | Template config] ************************************************************************************************************************************************************************************
ok: [vector]

TASK [Vector | change systemd unit] ******************************************************************************************************************************************************************************************
ok: [vector]

PLAY RECAP *******************************************************************************************************************************************************************************************************************
clickhouse                 : ok=3    changed=0    unreachable=0    failed=0    skipped=1    rescued=1    ignored=0   
vector                     : ok=6    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

user@study:~/home_work/ansible/ansible-02-playbook$ ansible-playbook -i ./playbook/inventory/prod.yml ./playbook/site.yml --diff -kK
SSH password: 
BECOME password[defaults to SSH password]: 
[WARNING]: Found both group and host with same name: vector
[WARNING]: Found both group and host with same name: clickhouse

PLAY [Install Clickhouse] ****************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Get clickhouse distrib 1] **********************************************************************************************************************************************************************************************
ok: [clickhouse] => (item=clickhouse-client)
ok: [clickhouse] => (item=clickhouse-server)
failed: [clickhouse] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "gid": 0, "group": "root", "item": "clickhouse-common-static", "mode": "0777", "msg": "Request failed", "owner": "root", "response": "HTTP Error 404: Not Found", "size": 246310036, "state": "file", "status_code": 404, "uid": 0, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib 2] **********************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Install clickhouse packages] *******************************************************************************************************************************************************************************************
ok: [clickhouse]

TASK [Flush handlers] ********************************************************************************************************************************************************************************************************

TASK [Create database] *******************************************************************************************************************************************************************************************************
ok: [clickhouse]

PLAY [Install Vector] ********************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************************************************
ok: [vector]

TASK [Get vector distrib] ****************************************************************************************************************************************************************************************************
ok: [vector]

TASK [Install vector packages] ***********************************************************************************************************************************************************************************************
ok: [vector]

TASK [Configure Vector | Ensure config directory exists] *********************************************************************************************************************************************************************
ok: [vector]

TASK [Configure Vector | Template config] ************************************************************************************************************************************************************************************
ok: [vector]

TASK [Vector | change systemd unit] ******************************************************************************************************************************************************************************************
ok: [vector]

PLAY RECAP *******************************************************************************************************************************************************************************************************************
clickhouse                 : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0   
vector                     : ok=6    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
8 -  
Повторный вывод аналогичен:   
```bash
PLAY RECAP *******************************************************************************************************************************************************************************************************************
clickhouse                 : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0   
vector                     : ok=6    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
9 -   
Ссылка на README.md-файл плейбука: https://github.com/suntsovvv/ansible-02-playbook/blob/main/playbook/README.md
