### В данном разделе описаны полезные хуки для системы контроля версий Git

#### С более подробной информацией, можно ознакомиться [тут](https://git-scm.com/book/ru/v1/Настройка-Git-Перехватчики-в-Git)

#### Для использования механизма git hooks, необходимо:
* В директории проекта, в директорию .git/hooks/ добавить файл с хуками.  
> pre-commit
* Сделать его исполняемым
> chmod +x pre-commit
* Добавить скрипт.

##### Пример
```
mkdir test && cd test && git init && echo "echo 'Git pre-commit hook'" > .git/hooks/pre-commit && chmod +x .git/hooks/pre-commit
```

* Сделать комит
> git commit --allow-empty -m "pre-commit hook"
В терминал будет выведено 
> Git pre-commit hook
---
Механизм хуков поддерживает множество языков программирования
