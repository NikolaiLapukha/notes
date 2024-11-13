1. Сперва нужно установить Neovim:	

**Установка в Debian/Ubuntu:**
```bash
sudo apt install neovim
```

**Установка в Archlinux:**
```bash
sudo pacman -S neovim
```

**Установка в Voidlinux**:
```bash
sudo xbps-install neovim
```

2. Скопировать файлы конфигурации из репозитория  в `~/.config/nvim` , если нет папки `nvim` то создать ее:
```bash
git clone https://github.com/NikolaiLapukha/nvim.git ~/.config/nvim
```

3. Зайти в файл `init.lua` в папке `nvim` и провести установку плагинов командой `:Lazy`

4. Установить пакет `exuberant-ctags
**Установка в Debian/Ubuntu:**
```bash
sudo apt install exuberant-ctags
```

**Установка в Archlinux:**
```bash
sudo pacman -S ctags
```

**Установка в voidlinux:**
```bash
sudo xbps-install ctags
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

**Установка в voidlinux:**
```bash
sudo xbps-install nodejs npm
```

6. Установка языковых моделей для `lspconfig`:

```bash
sudo npm i -g pyright
sudo npm install -g typescript typescript-language-server
sudo npm install -g emmet-ls
```
