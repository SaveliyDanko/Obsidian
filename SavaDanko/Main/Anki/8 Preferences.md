### [Appearance](https://docs.ankiweb.net/preferences.html#appearance)
#### [General](https://docs.ankiweb.net/preferences.html#general) 
- Language
- Video driver
#### [User Interface](https://docs.ankiweb.net/preferences.html#user-interface)
- Theme
- User Interface Size
- Reset Windows Sizes
#### [Distractions](https://docs.ankiweb.net/preferences.html#distractions)
- Hide the top and bottom bar during reviews
- Enable the "minimalist" mode, making the interface more compact/less fancy.
- Reduce motion, to disable some transitions/animations.
- Switching between native styling and the Anki theme (only on Mac/Linux).

### [Review](https://docs.ankiweb.net/preferences.html#review)
#### [Scheduler](https://docs.ankiweb.net/preferences.html#scheduler)
- Next day starts at
- Learn ahead limit
- Timebox time limit

#### [Review](https://docs.ankiweb.net/preferences.html#review-1)
- Show play buttons on cards with audio
- Interrupt current audio when answering
- Show remaining card count
- Show next review time above answer buttons
- Spacebar (or enter) also answers card

### [Editing](https://docs.ankiweb.net/preferences.html#editing)
#### [Editing](https://docs.ankiweb.net/preferences.html#editing-1)
- Paste clipboard images as PNG ✅
- Paste without Shift strips formatting ✅
- Default deck (When adding, default to current deck) ✅

#### [Browsing](https://docs.ankiweb.net/preferences.html#browsing)
- Default search text
- Ignore accents in search (slower)

### [Syncing](https://docs.ankiweb.net/preferences.html#syncing)
#### [Synchronisation](https://docs.ankiweb.net/preferences.html#synchronisation)
- Synchronize audio and images too
- Automatically sync on profile open/close
- Periodically sync media
- On next sync, force changes on one direction

#### [AnkiWeb Account](https://docs.ankiweb.net/preferences.html#ankiweb-account)

#### [Self-hosted Sync Server](https://docs.ankiweb.net/preferences.html#self-hosted-sync-server)
Anki позволяет продвинутым пользователям использовать **собственный сервер синхронизации**, вместо AnkiWeb. Это может быть полезно, если вы не хотите хранить данные в облаке Anki или у вас есть особые требования к конфиденциальности и контролю над данными.
#### Что важно знать:
1. **Это продвинутая функция**
    - Требуются **знания работы с сетями и командной строкой**.
    - Если возникнут проблемы (настройка, сеть, брандмауэр), вам придётся решать их самостоятельно.

2. **Синхронизация может перестать работать после обновления**    
    - Anki периодически обновляет **протокол синхронизации**.
    - Если вы обновите Anki на своих устройствах, но **не обновите сервер**, синхронизация может сломаться.

3. **Существуют сторонние серверы, но они ненадёжны**    
    - Некоторые пользователи создают **альтернативные серверы**, но они **не тестируются** разработчиками Anki.
    - Они могут долго обновляться после изменений в Anki, поэтому их использование **не рекомендуется**.

4. **Anki всё равно будет писать "AnkiWeb" в сообщениях**    
    - Даже если у вас настроен **свой сервер**, в ошибках и уведомлениях всё равно будет появляться название "AnkiWeb". Например, если ваш сервер недоступен, Anki может показать: **"Cannot connect to AnkiWeb"**, хотя речь идёт о вашем сервере.

### Backups
#### **Автоматическое резервное копирование в Anki**
Anki автоматически создаёт резервные копии ваших данных, включая **текст карточек** и **информацию о расписании повторений**. Однако **изображения и звуковые файлы не включаются** в эти копии.

### **Зачем это нужно?**
Автоматические резервные копии помогают восстановить данные, если вы случайно удалили или испортили карточки. **Но они хранятся только на вашем устройстве**, поэтому **не защитят вас**, если компьютер сломается или будет утерян. Поэтому **лучше дополнительно делать ручные копии** (например, экспортировать данные и сохранять их в облаке или на внешнем диске).

### **Как восстановить данные из резервной копии**
1. Откройте Anki и выберите **Switch Profile** (Сменить профиль) в меню **File**.
2. Нажмите кнопку **Open Backup** (Открыть резервную копию).
3. Выберите нужную копию для восстановления.

**Важно:**
- Все изменения, сделанные после создания этой копии, **будут утеряны**.
- После восстановления Anki **отключает автоматическую синхронизацию и создание новых копий**.
- Чтобы вернуть Anki в нормальный режим, **перезапустите программу**.

### **Когда создаются резервные копии?**
Anki создаёт копии **периодически**. По умолчанию это происходит **каждые 30 минут**, но этот интервал можно изменить в настройках.

Некоторые действия **принудительно создают резервную копию**, даже если время ещё не истекло:
- **Односторонняя загрузка данных при синхронизации**
- **Импорт файла .colpkg через File > Import**
- **Использование Tools > Check Database (Проверить базу данных)**

**Удаление старых копий:**
- Если копия старше **2 дней**, Anki начнёт **автоматически удалять** самые старые версии.
- Вы можете настроить, **сколько** ежедневных, недельных и месячных копий нужно сохранять.

### **Совместимость версий**
Если резервная копия была создана в версии **Anki 2.1.50 или новее**, её **нельзя будет импортировать в старые версии Anki**.
