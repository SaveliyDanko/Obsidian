#linux 

---
**Установка zsh:**
```bash
sudo apt install zsh
zsh --version
```

**Сделать zsh оболочкой по умолчанию и перезапустить систему:**
```bash
chsh -s $(which zsh)
```

Установка Oh My Zsh:
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Установка темы Powerlevel10k:
```bash
sudo apt install git fonts-powerline
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"
```

В `~/.zshrc` меняем строку:
```.zshrc
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Запуск настройки p10k:
```bash
p10k configure
```

**Установка дополнительных плагинов:**
zsh-autosuggestions (подсказывает команды по истории):
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
```

zsh-syntax-highlighting (подсвечивает синтаксис):
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```

Добавляем плагины в `.zshrc` файл:
```
plugins = (git zsh-syntax-highlighting zsh-autosuggestions)
```

Применяем изменения:
```bash
source ~/.zshrc
```