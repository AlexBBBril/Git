
### Working with remote repositories

* **git remote -v**
> Displaying a list of connected remote repositories
```
    origin  git@git.acc-name.com:project/name.git (fetch)
    origin  git@git.acc-name.com:project/name.git (push)
```

* **git remote add name git@git.acc-name.com:project/name.git**
> Add a new remote repository under an alias **name**

* **git remote show origin**  
> Remote repository inspection [link](https://git-scm.com/book/ru/v1/Основы-Git-Работа-с-удалёнными-репозиториями#Инспекция-удалённого-репозитория)

***

### Branch information
* **git branch  -a** 
> Displaying all branches of the repository, including remote ones

* **git branch -vv** 
> Displaying branches of the local repository with additional information such as their relationship to remote branches

* **git branch -vv | grep 'origin/.*]'**
> Displaying the branches of the local repository linked to the remote branches of the remote repository

***

### Branching in Git
* **git checkout -b local branch remote/tracked_branch** 
> (example: git checkout -b local_branch origin/remote_branch)
Will create a new local branch and make it a tracked remote branch.
[link](https://git-scm.com/book/ru/v1/Ветвление-в-Git-Удалённые-ветки)

* **git checkout --track -b local_branch remote/tracked branch** 
> Tracking by remote branch, local branch
[link](https://git-scm.com/book/ru/v1/Ветвление-в-Git-Удалённые-ветки#Отслеживание-веток)

* **git branch -u origin/remote_branch_name** 
> If you have a local branch and you need to set it up to a remote branch that has just been checked out, 
> or change the upstream branch that is being tracked
[link](https://git-scm.com/book/ru/v2/Ветвление-в-Git-Удалённые-ветки)

* **git push -u origin remote_branch** 
> Will create a new remote branch named remote_branch and link it back to the local branch this command was issued with
```
git checkout -b local_branch_name ### will create a local branch
git push -u origin remote_branch_name ### will create a remote branch and link it to the local branch from which the command was run
```

* **git push origin --all**
> Will create remote branches for all local branches that are not yet linked to remote branches and push data from local branches to remote ones

####  Deleting branches
* **git branch -d branch_name**
> Will delete the local branch branch_name
* **git push --delete <remote_name> <branch_name>**
> Will remove the remote branch branch_name from the repository
```
git push -d origin branch_name
```
#### Restoring branches
* **git branch branchName sha1**
> Rebuild the remote local branch with name **branchName** and hash **sha1**


#### Renaming a branch
* **git branch -m old_branch new_branch**
> Renames the local branch
  
#### Отмена изменений
* **git reset --soft a2f674b3b94060d3635bd41022626aff44411695**
> Откатить коммиты до определенного коммита (переданный хеш коммита)
* --soft отменяет коммиты с сохранением изменений
* --hard отменяет коммиты без сохранения изменений

#### Rebase (Перемещение веток)
* **git rebase toBranchName**
> Находится общий предок для двух веток (на которой вы находитесь сейчас **fromBranchName** и на которую вы выполняете перемещение **toBranchName**). Текущая ветка устанавливается на тот же коммит, что и ветка, на которую выполняется перемещение. Одно за другим применяются все изменения. Далее необходимо переключиться на ветку, куда выполнялось перемещение **git chekcout toBranchName** и выполнить процесс слияния. **git merge fromBranchName**. На данном этапе выполняется слияние перемотка(fast-forward merge), или иными словами git просто сдвигает указатель до необходимого коммита.

#### Подсчет веток
* **git branch | wc -l**
> Количество локальных веток

#### Подсчет коммитов
* **git cherry -v master**
> Какие коммиты прибавились по сравнению с веткой master
* **git cherry -v master | wc -l**
> Сколько коммитов прибавились по сравнению с веткой master

***

### Commit
* **git commit -am "commit message"** 
> Создать комит и задать сообщение для него, не вызывая vim

* **git commit --amend** 
> Изменить предыдуший комит с возможностью редактирования сообщения 

* **git commit --amend --no-edit** 
> Изменить предыдуший комит не редактируя сообщение комита 

* **git commit --allow-empty -m "empty commit"**
> Благ --allow-empty позволяет создать пустой комит, не добавляет измененния под контроль версий 

***

### Отслеживание файлов
* **git update-index --assume-unchanged file_name** 
> Git перестает отслеживание данного файла, не помещая его в .gitignore (для локальной ветки)

* **git update-index --no-assume-unchanged file_name** 
> Начать снова отслеживать файл гитом

* **git ls-files -v|grep '^h'** 
> Получить список файлов/директорий, которые являются неотслеживаемыми 

* **git ls-files --stage**
> Shows the contents of the index
 
* **git rm --cached <file>**
> Completely remove the file from the index

* **git rm --cached -r -f . **
> Completely remove all files from the index

***

### Просмотр истории коммитов
* **git log**
> Вывести список коммитов, данного репозитория, в обратном хронологическом порядке, вместе с его контрольной суммой SHA-1, именем и электронной почтой автора, датой создания и комментарием.
[git-scm.com](https://git-scm.com/book/ru/v1/Основы-Git-Просмотр-истории-коммитов)

* **git log --pretty=oneline**
> изменить формат вывода лога
* oneline - Каждый коммит в одну строку
* short, full, и fuller

* **git log --oneline**
> Короткий синтаксис, коммиgit log --onelineт в одну строку
***

### Уборка мусора

* **git gc**
> Удалить все неиспользуемые объекты

* **git remote prune origin**
> Удалить все ветки, которых нет во внешнем репозитории

Если даже на какой-либо объект нет явной ссылки, то на протяжении 30 дней на все объекты сохраняется ссылка в reflog. По этому когда производится уборка мусора все коммиты за последний месяц всё равно остаются в репозитории.

* **git reflog expire --expire=1.minute refs/heads/master**
* **git fsck –unreachable**
* **git gc**
> Чтобы избавиться от недоступных комитов
***

### Stash
> Спрятать изменения в грязном рабочем каталоге

* **git stash**
> Спрячет изменения из вашей ветки в stash

* **git stash list**
> Отобразит список спрятанных изменений в терминале

* **git stash apply**
> Вытащит из stash последнее положенное туда изменение

* **git stash drop**
> Удалил последнее добавленное изменение

* **git stash clear**
> Полностью очистит stash
