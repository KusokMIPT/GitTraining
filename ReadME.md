# Вопросы на 3.

1.	Создайте репозиторий на GitHub / GitLab по имени GitTraining


2.	Создайте локальную версию репозитория в некоторой папке через git init

```git init```

3.	Создайте файл readme.md, с содержимым: “My first Repo”, добавьте его в git
```

vim readme.md
git add --all
git commit -m 'first'
```

4.	Присоедините remote с именем origin к адресу репозитория
```
git remote add origin https://github.com/KusokMIPT/GitTraining
```
5.	Выполните команду “git push -u origin master” (-u необходимо, чтобы задать оригинальный - upstream repo)
```
git push -u origin master
```
6.	Создайте папку GitTraining.git вне папки с проектом
```
cd ..
mkdir GitTrainnig.git
cd GitTrainnig.git
```
7.	Создайте удаленную (remote) версию репозитория через “git init --bare”
```
git init --bare
```
8.	Сделайте “git remote add local <path to GitTraining.git>

```
git remote add local ../GitTraining.git
```

9.	Сделайте git push local master
```
git push local master
```
10.	Теперь мы умеем поднимать свой инстанс git

# Вопросы на 4.

1.	Создайте новую ветку my-new-branch
```
git checkout -b my-new-branch
```
2.	Сделайте изменения в новой ветке - напишите hello world.

```
vim readme.md 

hello world
```

3.	Закоммитьте изменения и залейте на удаленный сервер (GitHub, GitLab).
```
git add readme.md 
```

4.	После этого создайте новую ветку из ветки master на удаленном сервере (GitHub, GitLab) - my-remote-branch, создайте в нем файл readmes/readme.md.

5.	После этого выкачайте ветку my-remote-branch.

```
git branch -a
git checkout my-remote-branch

```
6.	Слейте ветку my-remote-branch в ветку my-new-branch.

```
git checkout my-new-branch
git merge me-remote-branch

```
7.	Какой граф изменений получился?

# Вопросы на 5.

1.	Начните изменять свой код в репозитории (создайте в master A.cpp, закоммитьте его, переключитесь в ветку my-new-branch, создайте A.cpp, не коммитьте)
```
vim A.cpp
git checkout my-new-branch
vim A.cpp
git checkout master

```
2.	Попытайтесь переключиться на другую ветку. Какое сообщение вы получите?

```
error: The following untracked working tree files would be overwritten by checkout:
	A.cpp
Please move or remove them before you switch branches.
Aborting
```

3.	Как можно решать эту проблему? Найдите хотя бы два решения этой проблемы

- Первый: **stash**
```
git stash
```

- Второй: **rename*
```
rename ...
```

4.	Откройте папку в среде разработки (Pycharm, IDEA). Какие файлы появились при этом?
```
        new file:   .idea/.gitignore
        new file:   .idea/inspectionProfiles/profiles_settings.xml
        new file:   .idea/misc.xml
        new file:   .idea/modules.xml
        new file:   .idea/vcs.iml
        new file:   .idea/vcs.xml

```

5.	Добавьте эти файлы в git при помощи git add.
6.	Как можно удалить эти файлы из git, но не из файловой системы?
```
	git rm --cached -r .idea/
```

7.	Как сделать так, чтобы эти файлы не добавлялись в git автоматически при команде git add --all?

используем `gitignore`

```
.gitignore:

> .idea/
```

# Вопросы на 6.

1.	Сделайте в ветке my-new-branch следующие пять файлов: a.py, b.py, c.py, d.py, e.py - лучше через веб интерфейс
2.	Скачайте изменения локально
```
git pull origin my-new-branc
```

3.	Выполните команду git rebase -i HEAD~5

4.	Изменим названия коммитов “Create b.py и d.py”

Меняем у соотвествующих коммитов `pick` на `reword`, после вместо _Create b.py_ напишем _ADD b.py_
5.	Выполняем git rebase --continue.
6.	Повторяем действие со вторым коммитом.
7.	Выполнится ли git push origin my-new-branch?

Нет, будет следующая ошибка:
```
To https://github.com/KusokMIPT/GitTraining.git
 ! [rejected]        my-new-branch -> my-new-branch (non-fast-forward)
error: failed to push some refs to 'https://github.com/KusokMIPT/GitTraining.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```
8.	Разберитесь с опцией squash - как слить все коммиты в один?

Сделаем `git rebase -i HEAD~5`. Заменим `Pick` на `s` у всех коммитов кроме первого. 

# Вопрос на 7.

1.	Создайте коммит с созданным python-файлом, закоммитьте в ветку master. Как запушить только этот коммит в local remote? Продемонстрируйте это.

Создадим файлики `7_task_1.py` и `7_task_2.py`. Для каждого из них сделаем отдельный коммит и с помощью `git rebase -i HEAD~2` найдем их идентификаторы. в local запушим лишь один из них с помощью команды:

```
git push local ec8931a:master
```

![](https://i.imgur.com/LGTc9QF.png)


# Вопрос на 8.

2.	Расскажите, как из отдельной папки можно выделить отдельный репозиторий, как затем подключить эту зависимость к исходному проекту? Продемонстрируйте на примере: https://github.com/tensorflow/tensorflow/tree/r1.14 - выпиливаем contrib в отдельный репозиторий, причем делаем его как git-submodule

