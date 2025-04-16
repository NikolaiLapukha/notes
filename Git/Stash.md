Чтобы добавить изменения которые не должны попасть в коммит и не должны быть отслеживаемые можно использовать команду `git stash`:

```bash
touch FILE.md
git add FILE.md
git status

On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    new file:   FILE.md

# Прячем файлы
# После этой команды пропадут все измененные файлы
# независимо от того, добавлены они в индекс или нет
git stash

Saved working directory and index state WIP on main: e7bb5e5 update README.md

git status

On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

Проще говоря команда `git stash` временно прячет файлы от git.

Команды `git stash pop` - снова делает файлы видимыми для git.

