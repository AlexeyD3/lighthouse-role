ansible-lighthouse
=========
![GitHub tag (latest by date)](https://img.shields.io/badge/tag-1.0.0-blue)
[![Ansible Galaxy Lighthouse](https://img.shields.io/badge/role-AlexeyD3.lighthouse-blue.svg)](https://galaxy.ansible.com/AlexeyD3/lighthouse/)
[![Ansible Galaxy Clickhouse](https://img.shields.io/badge/role-AlexeyD3.clickhouse-yellow.svg)](https://galaxy.ansible.com/AlexeyD3/clickhouse/)
[![Ansible Galaxy Vector](https://img.shields.io/badge/role-AlexeyD3.vector-yellow.svg)](https://galaxy.ansible.com/AlexeyD3/vector/)

Роль для установки lighthouse.
- Устновка Git
- Скачивание lighthouse из репозитория
- Конфигурирование lighthouse

Requirements
------------
- Должен быть установлен git. Если его нет, роль произведёт его установку
- Требуется отдельная установка и настройка Nginx

Role Variables
--------------
Переменные для установки
default/main.yml:
```yaml
clickhouse_user: netology
clickhouse_password: netology
```

Переменные для скачивания lighthouse из git и конфигурационных файлов lighthouse/nginx
vars/main.yml
```yaml
lighthouse_vcs: https://github.com/VKCOM/lighthouse.git
lighthouse_dir: /var/lib/lighthouse
lighthouse_access_log_name: lighthouse_access
```

Dependencies
------------
Требуется роль [clickhouse-role](https://github.com/AlexeyD3/clickhouse-role)

Example Playbook
----------------
```yaml
hosts: lighthouse
roles:
  - role: lighthouse-role
```

Для вывода строки подключения к web-интерфейсу используется post_tasks:

```yaml
post_tasks:
  - name: Show connect URL lighthouse
    debug:
      msg: "http://{{ ansible_host }}/#http://{{ hostvars['clickhouse-01'].ansible_host }}:8123/?user={{ clickhouse_user }}"
```

Author Information
------------------
Alexey Dubrovin
