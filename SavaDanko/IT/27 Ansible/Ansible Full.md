#### Ansible
**Ansible** — это инструмент автоматизации с открытым исходным кодом, который управляет конфигурацией, развертыванием и оркестрацией инфраструктуры.

Он работает по принципу «push» (управляющий узел → управляемые узлы), использует простой декларативный язык YAML (playbooks), и взаимодействует с системами по стандартным протоколам (SSH, WinRM, API), без установки агентов на целевых машинах.

Ключевые возможности:
- автоматизация настройки серверов и приложений    
- управление сетевым оборудованием и облаками
- оркестрация сложных процессов (CI/CD, multi-tier раскатки)
- масштабируемость от пары хостов до тысяч.

---
#### Ansible Ubuntu Installing
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
ansible --version
```

---
#### Ansible Control Node
**Control Node** — это машина, с которой запускается Ansible (например, ноутбук разработчика, сервер CI/CD или AWX/Controller).  
На ней установлены:
- `ansible-core`
- инструменты (`ansible`, `ansible-playbook`, `ansible-navigator`)
- inventory и playbooks

---
#### Ansible Managed Node
**Managed Node** — это целевой узел (сервер, контейнер, сетевое устройство), на котором Ansible выполняет задачи.
- На них не нужно ставить агента Ansible — взаимодействие идёт по SSH, WinRM или API.
- Единственное требование: должна быть возможность запустить нужный интерпретатор (чаще всего Python или PowerShell).

---
#### Ansible Inventory
[[Ansible Inventory]]

---
#### Ansible Playbook
[[Ansible Playbook]]

---
#### Ansible Play
**Play** — это блок внутри playbook, который связывает группу хостов (из inventory) с набором задач (tasks).
- Определяет контекст выполнения: какие хосты, под каким пользователем, с какими переменными.
- Может содержать роли, handlers, переменные.

---
#### Ansible Task
**Task** — это одна операция внутри play: вызов конкретного модуля Ansible с параметрами.
- Выполняется на всех хостах, указанных в play.
- Идемпотентен: повторный запуск не приведёт к изменению, если состояние уже достигнуто.

---
#### Ansible Module
**Ansible Module** — это минимальная единица работы Ansible: автономный кусок кода (обычно на Python, PowerShell или другом языке), который выполняет одну конкретную операцию на управляемом узле.

Примеры: установка пакета (`apt`, `yum`), управление пользователями (`user`), работа с файлами (`copy`, `template`), управление сервисами (`service`).
- Модули вызываются в tasks внутри playbook.
- Они идемпотентны: приводят систему в нужное состояние и не делают изменений, если оно уже достигнуто.
- Распространяются в составе коллекций и имеют полностью квалифицированные имена (FQCN), например: `ansible.builtin.copy`.

---
#### Ansible ad hoc command
**Ansible ad hoc command** — это одноразовая команда Ansible, выполняемая напрямую из CLI без написания playbook, чтобы быстро выполнить задачу на удалённых хостах.

Особенности:
- Использует синтаксис `ansible <pattern> -m <module> -a "<args>"`.    
- Подходит для быстрых операций: пинг хостов, копирование файлов, перезапуск сервисов.
- Не заменяет playbook, а служит для разовых или тестовых действий.
    
Пример
```bash
ansible all -m ping
```

Проверка доступности всех хостов.
```bash
ansible webservers -m shell -a "uptime"
```
Выполнить команду `uptime` на всех хостах группы `webservers`.


---
#### ansible cli
[ansible cli](https://docs.ansible.com/ansible/latest/cli/ansible.html)

---
#### ansible-config cli
[ansible-config cli](https://docs.ansible.com/ansible/latest/cli/ansible-config.html)

**`ansible-config`** — это утилита командной строки Ansible для работы с настройками конфигурации.
Возможности:
- Показывает активные параметры конфигурации и их источники (файл `ansible.cfg`, переменные окружения, значения по умолчанию).
- Позволяет проверить, какое значение применится на практике.
- Может выводить список всех доступных опций и их описание.

Примеры
```bash
ansible-config list
```
Показать все доступные параметры конфигурации.

```bash
ansible-config dump --only-changed
```
Вывести только изменённые настройки и их источник.

---
#### ansible-console cli
[ansible-console](https://docs.ansible.com/ansible/latest/cli/ansible-console.html)

**`ansible-console`** — это интерактивная командная оболочка Ansible, работающая в режиме REPL (read–eval–print loop), которая позволяет выполнять ad hoc команды в живом режиме без постоянного вызова `ansible` из CLI.

Особенности:
- Поддерживает те же модули, что и обычные ad hoc команды.
- Позволяет переключаться между группами хостов с помощью команды `cd <group>`.
- Удобна для тестирования и быстрой отладки задач.

Пример работы
```bash
ansible-console
```

Внутри:
```
Welcome to the ansible console.
Type help or ? to list commands.

root@all (3)[f:5]$ ping
root@all (3)[f:5]$ shell uptime
root@webservers (2)[f:5]$ cd dbservers
root@dbservers (2)[f:5]$ yum name=httpd state=latest
```

---
#### ansible-doc
[ansible-doc](https://docs.ansible.com/ansible/latest/cli/ansible-doc.html)

**`ansible-doc`** — это утилита командной строки Ansible для просмотра встроенной документации по модулям, плагинам и коллекциям прямо из терминала.

Основные возможности:
- Показывает описание модуля или плагина, его параметры, примеры использования.
- Может выводить список всех доступных модулей.
- Удобен для быстрого справочника без обращения к онлайн-документации.

Примеры
```bash
ansible-doc -l
```
Вывести список всех доступных модулей.

```bash
ansible-doc ping
```
Показать документацию по модулю `ping`.

```bash
ansible-doc -t plugin inventory
```
Показать список доступных inventory-плагинов.

---
#### ansible-galaxy
[ansible-galaxy](https://docs.ansible.com/ansible/latest/cli/ansible-galaxy.html)

**`ansible-galaxy`** — это утилита командной строки Ansible для работы с контентом из Ansible Galaxy и других источников (репозитории Git, локальные архивы).

Основные возможности:
- скачивание и установка ролей и коллекций (`install`)    
- обновление уже установленных (`collection install --upgrade`)
- публикация собственных ролей и коллекций (`publish`)
- создание шаблона для новой роли или коллекции (`init`)

Примеры
```bash
ansible-galaxy collection install community.postgresql
```
Установить коллекцию `community.postgresql`.

```bash
ansible-galaxy role init myrole
```
Создать структуру новой роли `myrole`.

```bash
ansible-galaxy collection list
```
Показать список установленных коллекций.

---
#### ansible-inventory
[ansible-inventory](https://docs.ansible.com/ansible/latest/cli/ansible-inventory.html)

**`ansible-inventory`** — это утилита командной строки Ansible для работы с inventory-источниками (списком хостов и групп).

Основные возможности:
- показывает, как Ansible видит inventory после обработки (с учётом плагинов, переменных, групп),
- выводит список хостов, групп и их переменных в разных форматах (YAML, JSON, граф),
- помогает отладить статические и динамические inventory.
    
Примеры
```bash
ansible-inventory -i inventory.ini --list
```
Показать все хосты и группы в формате JSON.

```bash
ansible-inventory -i inventory.yml --graph
```
Вывести иерархию групп и хостов в виде дерева.

```bash
ansible-inventory -i inventory/ --host web1.example.com
```
Показать переменные конкретного хоста.

---
#### ansible-playbook
**`ansible-playbook`** — это основная CLI-утилита Ansible для запуска playbook’ов.

Основные возможности:
- выполняет один или несколько playbook’ов на выбранных хоста
- позволяет задавать inventory, переменные, теги и лимиты хостов
- поддерживает dry-run режим (`--check`) и вывод изменений (`--diff`)
- интегрируется с callback-плагинами для детального логирования

Примеры
```bash
ansible-playbook site.yml -i inventory.ini
```
Запуск playbook `site.yml` с inventory `inventory.ini`.

```bash
ansible-playbook deploy.yml --check --diff
```
Проверка (dry-run) и показ отличий без фактического применения изменений.

```bash
ansible-playbook site.yml --tags "install,configure"
```
Выполнить только задачи с тегами `install` и `configure`.

---
#### ansible-pull
[ansible-pull](https://docs.ansible.com/ansible/latest/cli/ansible-pull.html)

**`ansible-pull`** — это утилита командной строки Ansible, которая запускает playbook на самом managed node, подтягивая их из удалённого репозитория (например, Git).

В отличие от стандартного подхода (push-модель), где control node «толкает» конфигурацию на хосты, `ansible-pull` реализует pull-модель:
- сам хост инициирует выполнение,
- скачивает playbook (обычно из Git),
- применяет его локально

Пример
```bash
ansible-pull -U https://github.com/org/configs.git site.yml
```
Хост скачает playbook `site.yml` из репозитория и выполнит его локально.

---
#### ansible-vault
[ansible-vault](https://docs.ansible.com/ansible/latest/cli/ansible-vault.html)

**`ansible-vault`** — это утилита Ansible для защиты чувствительных данных (пароли, ключи, токены) с помощью шифрования.

Основные возможности:
- шифрует и расшифровывает файлы (например, `group_vars`, `host_vars`)
- позволяет создавать и редактировать зашифрованные файлы
- поддерживает как полный, так и частичный (inline) режим шифрования переменных
- работает с разными бэкендами для хранения паролей (файл, prompt, сторонние менеджеры)

Примеры
Создать зашифрованный файл:
```bash
ansible-vault create secrets.yml
```

Зашифровать существующий файл:
```bash
ansible-vault encrypt vars.yml
```

Расшифровать:
```bash
ansible-vault decrypt vars.yml
```

Запуск playbook с использованием vault:
```bash
ansible-playbook site.yml --ask-vault-pass
```

---

#### Ansible Role
**Role** — это каталог со строгой структурой, который группирует всё необходимое для автоматизации определённой функции:
- `tasks/` — список задач (главное содержимое роли)
- `handlers/` — обработчики (обычно перезапуск сервисов)
- `files/` — статические файлы, которые можно копировать на хост
- `templates/` — шаблоны Jinja2 для конфигов
- `vars/` — переменные с высоким приоритетом
- `defaults/` — переменные по умолчанию (низший приоритет)
- `meta/` — метаинформация о роли (зависимости, поддерживаемые платформы)
Каждая роль отвечает за одну задачу инфраструктуры: например, «nginx», «postgresql», «deploy_app».

Пример структуры роли `nginx`:
```
roles/
└── nginx/
    ├── defaults/
    │   └── main.yml
    ├── files/
    │   └── index.html
    ├── handlers/
    │   └── main.yml
    ├── meta/
    │   └── main.yml
    ├── tasks/
    │   └── main.yml
    ├── templates/
    │   └── nginx.conf.j2
    ├── vars/
    │   └── main.yml
```

`tasks/main.yml`
```yaml
- name: Установить Nginx
  ansible.builtin.apt:
    name: nginx
    state: present
    update_cache: true

- name: Скопировать конфигурацию
  ansible.builtin.template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
  notify: Перезапустить nginx
```

`handlers/main.yml`
```
- name: Перезапустить nginx
  ansible.builtin.service:
    name: nginx
    state: restarted
```

`defaults/main.yml`
```
nginx_port: 80
```

Использование роли в playbook:
```
- name: Настройка веб-сервера
  hosts: web
  become: true
  roles:
    - nginx
```
Ansible сам найдёт каталог `roles/nginx/` и подтянет все `tasks`, `handlers`, `templates` и переменные.

---
#### Ansible Handler
**Ansible Handler** — это особый тип задачи (task) в Ansible, которая выполняется только тогда, когда её вызвала другая задача через директиву `notify`.

Используется для действий, которые нужно запускать только при изменениях (например, перезапуск сервиса после изменения конфигурации).  
Handlers определяются в секции `handlers` внутри playbook или роли.  
Выполняются в конце play (чтобы сервис перезапускался один раз, даже если несколько задач его изменили).

Пример использования handler
```yaml
- name: Настройка Nginx
  hosts: web
  become: true
  tasks:
    - name: Скопировать конфигурацию Nginx
      ansible.builtin.template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify: Перезапустить Nginx

  handlers:
    - name: Перезапустить Nginx
      ansible.builtin.service:
        name: nginx
        state: restarted
```

---
#### Ansible Plugin
**Ansible Plugin** — это расширение Ansible, которое добавляет или изменяет поведение движка автоматизации.

В отличие от модулей (которые выполняют действия на управляемых узлах), плагины работают внутри Ansible и влияют на то, как выполняются задачи, подключаются хосты, обрабатываются данные или выводятся результаты.

**Основные типы плагинов**
- Connection plugins — управляют подключением (SSH, WinRM, Docker, Kubernetes API).
- Inventory plugins — динамически генерируют список хостов (AWS, GCP, K8s).
- Callback plugins — определяют формат вывода (yaml, json, timer, profile_tasks).
- Filter plugins — добавляют новые фильтры для Jinja2-шаблонов.
- Lookup plugins — подтягивают данные из внешних источников (файлы, Vault, API).
- Strategy plugins — меняют стратегию выполнения (linear, free, debug).

---
#### Ansible Collection
**Ansible Collection** — это формат распространения и организации контента Ansible, который объединяет в единый пакет:
- modules
- plugins
- roles
- playbooks
- документацию и тесты.

Коллекции публикуются и распространяются через Ansible Galaxy или частные репозитории, устанавливаются командой `ansible-galaxy collection install`.

---
#### Ansible Execution Environment (EE)
**Ansible Execution Environment (EE)** — это контейнерный образ, внутри которого упакованы:
- `ansible-core` и `ansible-runner`
- Python и системные зависимости
- коллекции, роли и плагины Ansible
- дополнительные библиотеки, нужные для автоматизации (например, `psycopg2` для PostgreSQL или `boto3` для AWS).
    
EE выполняет роль управляющего узла в контейнере: playbook запускается внутри него, что обеспечивает предсказуемость, переносимость и изоляцию автоматизации.

---
#### ansible-builder
**ansible-builder** — это официальный инструмент Ansible, который автоматически собирает Execution Environment (EE) — контейнерный образ с `ansible-core`, коллекциями, ролями, Python-библиотеками и системными зависимостями.

Он использует декларативный файл `execution-environment.yml`, где указываются коллекции и пакеты, а затем формирует Dockerfile/Podmanfile и создаёт единый предсказуемый контейнер, пригодный для запуска playbook’ов в AWX/Automation Controller, CI/CD и локально через ansible-navigator.

---
#### ansible-navigator
**ansible-navigator** — это официальный CLI-инструмент Ansible для работы с Execution Environments (EE) и запуска автоматизации в контейнерах.

Он предоставляет единый интерфейс для:
- выполнения playbook’ов внутри EE (`ansible-navigator run`)
- интерактивного просмотра задач, модулей, логов и артефактов
- управления коллекциями и зависимостями
- отладки и анализа результатов в удобном формате (TUI или JSON/YAML).