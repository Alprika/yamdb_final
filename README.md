# API_YAMDB
[![yamdb_final_workflow](https://github.com/Alprika/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)](https://github.com/Alprika/yamdb_final/actions/workflows/yamdb_workflow.yml)

Проверить доступность сервиса: http://

### Описание проекта API_YAMDB:

Проект собирает отзывы пользователей на произведения. Категории: «Книги», «Фильмы», «Музыка», 
которые раличаются по жанрам. Сами произведения в YaMDb не хранятся, здесь нельзя
посмотреть фильм или послушать музыку. Зарегистрированные пользователи могут
оставить отзывы и поставить оценку, из оценок формируется рейтинг
произведения. 


### Шаблон наполнения env-файла:

SECRET_KEY=<секретный ключ>

DB_ENGINE=<БД, с которой работаем>

DB_NAME=<имя базы данных>

POSTGRES_USER=<логин для подключения к базе данных>

POSTGRES_PASSWORD=<пароль для подключения к БД>

DB_HOST=<название сервиса (контейнера)>

DB_PORT=<порт для подключения к БД>


### Описание команд для запуска приложения в контейнерах:

Клонировать репозиторий и перейти в него в командной строке:

https://github.com/Alprika/infra_sp2.git

Перейти в каталог "infra":

cd infra

Запустить docker-compose:

docker-compose up -d --build
Применить миграции:

docker-compose exec web python manage.py migrate

Создать суперпользователя:

docker-compose exec web python manage.py createsuperuser

Собрать статику:

docker-compose exec web python manage.py collectstatic --no-input

### Описание команды для заполнения базы данными:


Создание фикстур для заполнения базы данных тестовыми данными:
docker-compose exec web python manage.py create_fixtures

Заполнения базы данных тестовыми данными из созданных фикстур:
docker-compose exec web python manage.py populate_fixtures

### Примеры выполнения запросов для API:
- Получаем JWT-токена(POST запрос)
api/v1/jwt/create/
Payload:

{
    "username": "string",
    "password": "string"
}

- Добавление нового отзыва(POST запрос)
(требуется Аутентификация)

api/v1/titles/{title_id}/reviews/
Payload:

{
    "text": "string",
    "score": 1
}