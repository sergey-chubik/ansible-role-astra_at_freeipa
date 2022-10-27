Ansible Role: Astra Atestat FreeIPA
=========

Эта роль выполнит настройку нескольких АРМ на базе ОС Astra Linux SE версий 1.7, подключенных к локальной сети, в соответствии с требованиями безопасности для обработки конфеденциальной информации (аттестационные мероприятия). С помощью роли можно установить и настроить систему управления службой FreeIPA (контроллер домена и клиенты), создать общий сетевой репозиторий (main и update) на контроллере домена, установить оперативные обновления операционной системы с общего сетевого репозитория, создать пользователей в системе FreeIPA и настроить директории для хранения конфеденциальной информации с различным уровнем мандатного доступа, а также предоставить сетевой доступ клиентам FreeIPA в эту директорию. Предполагается что ISO-образы основного диска и диска с обновлениями расположены на контроллере домена в домашней директории пользователя в директории astra, параметр `astra_at_freeipa_iso_path: /home/user/astra`.

Requirements
------------

Для хоста, на котором запускается эта роль необходимы следующие требования:
```
sshpass
rsync
```

Role Variables
--------------

Доступные переменные перечислены вместе со значениями по умолчанию в файле **defaults/main.yml**.
Для установки службы FreeIPA необходимо создать репозиторий базового диска на сервере FreeIPA (по умолчанию `true`):
```
astra_at_freeipa_repo_main_local_create: true
```
Если необходимо установить оперативные обновления системы то нужно создать репозиторий диска с обновлениями на сервере FreeIPA (по умолчанию `false`). Переменные отвечающие за установку оперативных обновлений и обновление загрузчика grub (по умолчанию `false`):
```
astra_at_freeipa_repo_update_local_create: false
astra_at_freeipa_os_update: false
astra_at_freeipa_grub_edit: false
```
Выбор способа установки обновления (штатный способ `dist_upgrade` или через утилиту `astra_update`, рекомендуемую разработчиками Astra):
```
astra_at_freeipa_os_update_tool: astra_update
```
Переменные для создания пользователей FreeIPA (имя пользователя, группа, общий пароль и период действия пароля):
```
astra_at_freeipa_domain_users: 
  - [user1, user11]
  - [user2, user22]
astra_at_freeipa_domain_users_password: 1qaz!QAZ
astra_at_freeipa_domain_users_password_expiration: 20221101235959
```

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - astra_at_freeipa

License
-------

BSD

Author Information
------------------

Chubik Sergey.
