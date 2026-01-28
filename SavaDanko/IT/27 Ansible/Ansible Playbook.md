**Ansible Playbook** — это YAML-файл, который описывает сценарий автоматизации: какие узлы (hosts) нужно задействовать, какие задачи (tasks) на них выполнить, какие роли и переменные использовать.

Простой пример `playbook.yml`
```yaml
- name: Настройка веб-сервера # <-- это Play
  hosts: web
  become: true
  tasks:
    - name: Установить Nginx # <-- список Tasks
      ansible.builtin.apt: # <-- Task: модуль apt
        name: nginx
        state: present
        update_cache: true

    - name: Запустить и включить Nginx
      ansible.builtin.service: # <-- Task: модуль service
        name: nginx
        state: started
        enabled: true

    - name: Вывести сообщение <- task
      ansible.builtin.debug:
        msg: "Nginx успешно установлен на {{ inventory_hostname }}"
```
Здесь:
- Play → применяется к группе хостов `web`    
- Tasks → установка пакета, запуск сервиса, вывод сообщения;
- Используются встроенные модули `apt`, `service`, `debug`.

---
#### Templating
**Ansible templating (шаблонизация в Ansible)** — это механизм использования движка Jinja2 для динамической подстановки значений переменных, фактов и данных во время выполнения задач и playbook’ов. Он позволяет создавать универсальные конфигурационные файлы, генерировать имена, условия, циклы и фильтровать данные в зависимости от окружения или состояния хоста.

Ключевые особенности:
- Основан на Jinja2 (поддержка выражений, фильтров, тестов, условий, циклов).
- Работает на управляющем узле, а на целевые хосты передаются уже готовые результаты.
- Используется в модуле template, а также внутри playbook’ов (например, в `vars`, `tasks`, `handlers`).
- Поддерживает Lookup плагины для получения данных из внешних источников (файлы, API, БД).

Пример использования шаблона в playbook:
```yaml
- name: Настройка конфигурации Nginx
  hosts: webservers
  tasks:
    - name: Скопировать конфигурацию из шаблона
      ansible.builtin.template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
```

Шаблон `nginx.conf.j2`:
```jinja2
server {
    listen 80;
    server_name {{ inventory_hostname }};
    root {{ web_root }};
}
```
Здесь переменные `inventory_hostname` и `web_root` будут автоматически подставлены при рендеринге.

---
#### Условия (`when`)
- Условие задаётся через ключевое слово `when`.
- Принимает любое выражение Jinja2 (с переменными, фактами, логическими операциями).
- Если условие false, задача пропускается (status = skipped).

Пример:
```yaml
- name: Установить nginx только на Ubuntu
  ansible.builtin.apt:
    name: nginx
    state: present
  when: ansible_facts['os_family'] == "Debian"
```

**Несколько условий**
Можно перечислить несколько условий, и они будут объединены через логическое И.
```yaml
- name: Установить nginx на Ubuntu 20.04
  ansible.builtin.apt:
    name: nginx
    state: present
  when:
    - ansible_facts['os_family'] == "Debian"
    - ansible_facts['distribution_version'] == "20.04"
```

**Условные блоки (`block` + `when`)**
`block` позволяет группировать задачи и применять условие ко всему блоку.

Пример:
```yaml
- name: Настройка для RedHat-систем
  block:
    - name: Установить httpd
      ansible.builtin.yum:
        name: httpd
        state: present

    - name: Запустить и включить httpd
      ansible.builtin.service:
        name: httpd
        state: started
        enabled: true
  when: ansible_facts['os_family'] == "RedHat"
```

---
#### Loop
**Простой цикл — `loop`**
Самый универсальный вариант. Задаётся список значений.
```yaml
- name: Создать несколько директорий
  ansible.builtin.file:
    path: "/opt/{{ item }}"
    state: directory
  loop:
    - logs
    - backups
    - tmp
```
Будут созданы директории: `/opt/logs`, `/opt/backups`, `/opt/tmp`.

**Цикл `with_items` (устаревший, заменён на `loop`)**
Старая форма, но до сих пор встречается.
```yaml
- name: Установить несколько пакетов
  ansible.builtin.apt:
    name: "{{ item }}"
    state: present
  with_items:
    - git
    - curl
    - htop
```

**Цикл с ключ-значение (`dict`)**
Позволяет работать с парами.
```yaml
- name: Создать пользователей
  ansible.builtin.user:
    name: "{{ item.key }}"
    state: present
    groups: "{{ item.value }}"
  loop: 
    - { key: "alice", value: "admins" }
    - { key: "bob", value: "developers" }
```

**Вложенные циклы (`with_nested` / `product`)**
Для перебора комбинаций значений.
```yaml
- name: Создать комбинации пользователей и групп
  debug:
    msg: "User {{ item.0 }} в группе {{ item.1 }}"
  with_nested:
    - [ "alice", "bob" ]
    - [ "admins", "devs" ]
```
Результат:
- `alice` в `admins`    
- `alice` в `devs`
- `bob` в `admins`
- `bob` в `devs`

**Циклы по файлам, словарям и последовательностям**
- `with_fileglob` → все файлы по шаблону.    
- `with_dict` → обход словаря.
- `with_sequence` → диапазон чисел или букв.
    
Пример `with_sequence`:
```yaml
- name: Создать пользователей user1, user2, user3
  ansible.builtin.user:
    name: "user{{ item }}"
  with_sequence: start=1 end=3
```

**Loop Control (управление циклом)**
Можно задать переменную цикла (не `item`, а своё имя), задержки и лимиты.
```yaml
- name: Установить пакеты с кастомным именем переменной
  ansible.builtin.apt:
    name: "{{ pkg }}"
    state: present
  loop:
    - vim
    - mc
  loop_control:
    loop_var: pkg
```
