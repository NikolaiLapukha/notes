1. Сперва нужно установить Neovim:	

**Установка в Debian/Ubuntu:**
```bash
sudo apt install neovim
```

**Установка в Archlinux:**
```bash
sudo pacman -S neovim
```

2. Скопировать файлы конфигурации из репозитория  в `~/.config/nvim` , если нет папки `nvim` то создать ее:
```bash
~/.config/nvim ❯ pwd
/home/nl/.config/nvim
~/.config/nvim ❯ git clone https://github.com/NikolaiLapukha/nvim.git
```

3. Зайти в файл `init.vim` в папке `nvim` и провести установку плагинов командой `:PlugInstall`

4. Установить пакет `exuberant-ctags
**Установка в Debian/Ubuntu:**
```bash
sudo apt install exuberant-ctags
```

**Установка в Archlinux:**
```bash
sudo pacman -S ctags
```

5. Установить дополнительные библиотеки `nodejs`, `npm`:
**Установка в Debian/Ubuntu:**
```bash
sudo apt install nodejs npm
```

**Установка в Archlinux:**
```bash 
sudo pacman -S nodejs npm
```

6. Далее нужно перейти в директорию `~/.local/share/nvim/plugged/coc.nvim
`
и установить там `yarn`:
```bash
sudo npm install -g yarn
yarn install
yarn build
```

7. Замет нужно установить `python3-pip` и `jedi`:
**Установка в Debian/Ubuntu:**
```bash
sudo apt install python3-pip
pip3 install jedi
```

**Установка в Archlinux:**
```bash
sudo pacman -S python-pip
sudo pacman -S python-jedi
```

8. Далее нужно установить нужную языковую модель через `coc-nvim`:
`:CocInstall имя языковой модели `