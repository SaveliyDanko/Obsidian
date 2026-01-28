**URI (Uniform Resource Identifier)** — это универсальный идентификатор ресурса.  
Он определяет как найти или обозначить некоторый ресурс в сети или системе.

Важно:
- **URL (Uniform Resource Locator)** — частный случай URI, указывающий местоположение ресурса.
- **URN (Uniform Resource Name)** — другой вид URI, задающий уникальное имя ресурса, без привязки к месту.
    
#### Общая структура URI
Формат (RFC 3986):
```
scheme:[//authority]path[?query][#fragment]
```

Компоненты:
1. scheme — схема, протокол (например: `http`, `https`, `ftp`, `mailto`).    
2. authority (опционально):
    - userinfo (логин/пароль, редко используется из-за небезопасности),
    - host (домен или IP),
    - port (номер порта).
3. path — путь к ресурсу на сервере.
4. query — строка запроса (параметры `ключ=значение`).
5. fragment — якорь (ссылка на часть документа, напр. `#section2`).
    
#### Пример URI
Возьмём:
```
https://user:pass@www.example.com:8080/articles/index.html?id=15&lang=ru#comments
```
Разбор:
- scheme: `https`    
- userinfo: `user:pass`
- host: `www.example.com`
- port: `8080`
- path: `/articles/index.html`
- query: `id=15&lang=ru`
- fragment: `comments`
