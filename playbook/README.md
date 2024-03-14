## Clickhouse-Vector Ansible-Playbook
Проект развёртывания инфраструктуры в docker контейнерах для сбора и анализа логов на основе Clickhouse и Vector

## Installation
Вам необходимо запустить два docker-контейнера c именами "сlickhouse" и "vector"

Для установки необходимо использовать образы "pycontribs/centos:7".

Для выбора версии и архитектуры замените в файлах `group_vars/clickhouse/clickhouse.yml` и `group_vars/vector/vector.yml` соответствующие переменные:
```
clickhouse_version: <"version">
clickhouse_arch: <"arch">
```
```
vector_version: <"version">
vector_arch: <"arch">
```
Конфигурация для vector содержится в tenplate файле vector.yaml.j2
### Run
Для запуска можно использовать следующую команду после того, как хосты были прописаны в `/inventory/prod.yml`:
```shell
ansible-playbook -i /inventory/prod.yml site.yml
```