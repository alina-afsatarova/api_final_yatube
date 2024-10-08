# Проект «API для Yatube»
YaTube - проект социальной сети. В рамках разработки REST API для Yatube были реализованы следующие возможности:
+ Создание, получение, редактирование и удаление публикаций;
+ Просмотр списка групп, получение информации о конкретной группе;
+ Создание, получение, редактирование и удаление комментариев к посту;
+ Аутентификация пользователей с помощью JWT-токенов;
+ Подписка на пользователей, получение информации о подписках пользователя.

## Как запустить проект
Клонировать репозиторий и перейти в него в командной строке:
```
git clone https://github.com/alina-afsatarova/api_final_yatube.git
```
```
cd api_final_yatube
```
Cоздать и активировать виртуальное окружение:
```
python3 -m venv env
```
```
source env/bin/activate
```
Установить зависимости из файла requirements.txt:
```
python3 -m pip install --upgrade pip
```
```
pip install -r requirements.txt
```
Выполнить миграции:
```
python3 manage.py migrate
```
Запустить проект:
```
python3 manage.py runserver
```

## Примеры запросов к API
После запуска проекта к API Yatube доступна докуменция по адресу `http://127.0.0.1:8000/redoc/`.

POST-запрос с токеном, добавление нового поста:
`http://127.0.0.1:8000/api/v1/posts/`
```
{
     "text": "Текст поста.",
     "group": 1
}
```
Пример ответа:
```
{
    "id": 1,
    "text": "Текст поста.",
    "author": "user123",
    "image": null,
    "group": 1,
    "pub_date": "2021-06-01T08:47:11.084589Z"
}
```

POST-запрос с токеном, добавление нового комментария к посту с id=1:
`http://127.0.0.1:8000/api/v1/posts/1/comments/`
```
{
    "text": "тест тест"
}
```
Пример ответа:
```
{
    "id": 4,
    "author": "user123",
    "post": 1,
    "text": "тест тест",
    "created": "2021-06-01T10:14:51.388932Z"
}
```

GET-запроc, получение информации о группе с id=2:
`http://127.0.0.1:8000/api/v1/groups/2/`
Пример ответа:
```
{
    "id": 2,
    "title": "Математика",
    "slug": "math",
    "description": "Посты на тему математики"
}
 ```

GET-запроc с токеном, получение информации о подписках пользователя, сделавшего запрос:
`http://127.0.0.1:8000/api/v1/follow/`
Пример ответа:
```
{
     "user": "user123",
     "following": "New_User"
}
```
