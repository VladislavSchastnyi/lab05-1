## Laboratory work V

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```ShellSession
$ open https://travis-ci.org
```

## Tasks

- [ ] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
- [ ] 2. Создать публичный репозиторий с названием **lab05** на сервисе **GitHub**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
- [ ] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
- [ ] 6. Получить фрагмент вставки значка сервиса **Travis CI** в формате **Markdown**
- [ ] 7. Установить [**Travis CLI**](https://github.com/travis-ci/travis.rb#installation)
- [ ] 8. Выполнить инструкцию учебного материала
- [ ] 9. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

Присваиваем значения перменным GITHUB_USERNAME и GITHUB_TOKEN

```ShellSession
$ export GITHUB_USERNAME=VladislavSchastnyi
$ export GITHUB_TOKEN=e3fbbd60c28cbc06728165fe106210ca230c78ea
```

Клонируем lab04 в Lab05, переходим в Lab05

```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab04 Lab05 #Клонируем
Cloning into 'Lab05'...
remote: Counting objects: 25, done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 25 (delta 4), reused 25 (delta 4), pack-reused 0
Unpacking objects: 100% (25/25), done.
$ cd Lab05 #Переходим в Lab05
$ git remote remove origin 
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab05 #Соединяем с репозиторием на сервере

```
Создаем .travis.yml и заполняем его

```ShellSession
$ cat > .travis.yml <<EOF
language: cpp
EOF
```

```ShellSession
$ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```

```ShellSession
$ cat >> .travis.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```
Заходим в travis

```ShellSession
$ travis login --github-token ${GITHUB_TOKEN}
Shell completion not installed. Would you like to install it now? |y| y
Successfully logged in as VladislavSchastnyi!
```

Включаем отображение предупреждений

```ShellSession
$ travis lint
Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping
```

```ShellSession
$ [![Build Status](https://travis-ci.com/VladislavSchastnyi/lab05.svg?branch=master)](https://travis-ci.com/VladislavSchastnyi/lab05)
```
Выкладываем всё в репозиторий

```ShellSession
$ git add .travis.yml # Добавляем файл для коммита
$ git add README.md # Добавляем файл для коммита
$ git commit -m"added CI" # Коммитим с комментарием "added CI"
$ git push origin master # Выкладываем в репозиторий на сервер
```

Работаем с travis

```ShellSession
$ travis lint #Отображаем предупреждения
$ travis accounts #Отображаем аккаунт
$ travis sync #Синхронизируемся
$ travis repos #Отображаем, какие репозитории доступны, а какие нет
$ travis enable #Подключаем проект
$ travis whatsup #Отоброжаем, что изменилось в проекте
$ travis branches #Отоброжаем обновленную версию проекта
$ travis history #Отоброжаем историю проекта
$ travis show #Отображаем проект
```


## Report

```ShellSession
$ popd
$ export LAB_NUMBER=05
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [Travis Client](https://github.com/travis-ci/travis.rb)
- [AppVeyour](https://www.appveyor.com/)
- [GitLab CI](https://about.gitlab.com/gitlab-ci/)

```
Copyright (c) 2017 Братья Вершинины
```
