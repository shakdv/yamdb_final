![Yamdb Workflow Status](https://github.com/shakdv/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?branch=master&event=push)
# Проект: CI и CD для «API для YaMDb»

Реализация docker-compose и CI/CD для приложения «API для YaMDb»,
о котором более подробно расписано тут: [«API для YaMDb»](https://github.com/shakdv/api_yamdb) 

Проект доступен по адресу: http://51.250.22.246/redoc/

## Реализовано в CI/CD
* автоматический запуск тестов
* обновление образов на Docker Hub
* автоматический деплой на боевой сервер при пуше в главную ветку (master или main)
* отправка сообщения в Telegram через бота об успешном деплое

## Технологии
* Python 3.7
* Django 2.2
* DRF
* JWT
* Docker
* Docker-Compose
* Nginx
* PostreSQL
* GitHub Actions

## Установка и запуск

Клонировать репозиторий:
```bash
git clone https://github.com/shakdv/yamdb_final.git
```

Перейти в каталог:
```bash
cd yamdb_final/infra
```

Добавить файл .env в котором хранится SECRET_KEY и настройки БД:
```bash
echo "SECRET_KEY=YourSecretKey 
DB_ENGINE=django.db.backends.postgresql 
DB_NAME=postgres 
POSTGRES_USER=postgres 
POSTGRES_PASSWORD=postgres 
DB_HOST=db DB_PORT=5432" > .env
```
Пример заполнения файла .env:
```
SECRET_KEY=i8n#^u!c+u95k0b2*uraj)8b00(%p3ip9f*ze7s&+%8$r4bi5m
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql 
DB_NAME=postgres # имя базы данных 
POSTGRES_USER=postgres # логин для подключения к базе данных 
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой) 
DB_HOST=db # название сервиса (контейнера) 
DB_PORT=5432 # порт для подключения к БД 
```
Запустить контейнеры:
```bash
docker-compose up -d --build
```
Выполнить миграции:
```bash
docker-compose exec web python manage.py makemigrations
```
```bash
docker-compose exec web python manage.py migrate
```

Создать суперпользователя:
```bash
docker-compose exec web python manage.py createsuperuser
```
Собрать статику:
```bash
docker-compose exec web python manage.py collectstatic --no-input
```
Документация по приложению доступна по адресу: http://localhost/redoc/

Проект можно наполнить тестовыми данными:
```bash
docker-compose exec web python manage.py loaddata fixtures.json
```
Админка доступна по адресу: http://localhost/admin/

## Остановка и удаление
Остановить контейнеры:
```bash
docker-compose stop
```
Остановить контейнеры с последующим их удалением:
```bash
docker-compose down -v
```


Автор: [Dmitry Shakhlin](https://github.com/shakdv)