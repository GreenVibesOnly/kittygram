#  Kittygram - сервис для публикации фотографий котиков :3
Киттиграм - сайт, на котором хозяева могут делиться фотографиями и достижениями своих котиков. Зарегистрированные пользователи могут создавать, просматривать, редактировать и удалять свои записи, а так же смотреть ленту с фотографиями котиков других пользователей.


## Технологии

- Python
- Django
- Djangorestframework
- React
- Djoser
- Gunicorn
- pytest
- Docker
- PostgreSQL

В проекте предусмотрена автоматическая упаковка частей проекта в образы с помощью Docker и размещение их 
в удаленном репозитории на DockerHub, а также автоматизация деплоя на удаленный сервер с помощью GitHub actions. На удаленном сервере установлена операционная система Ubuntu.
Перед деплоем предусмотрено автоматическое тестирование проекта.


## Локальный запуск проекта:


Клонировать репозиторий и перейти в него в командной строке:

```
git clone <SSH Key>
```

```
cd kittygram_final
```

Cоздать и активировать виртуальное окружение:

```
python3 -m venv venv
```

* Если у вас Linux/macOS

    ```
    source venv/bin/activate
    ```

* Если у вас windows

    ```
    source venv/scripts/activate
    ```
В корневой директории проекта создать файл .env и скопировать в него данные из .env.example .

Установить зависимости из файла requirements.txt:

```
python3 -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```

Провести миграции:

```
python3 manage.py migrate
```

Запустить локальный сервер:

```
python3 manage.py runserver
```

Проект будет доступен по адресу: [http://127.0.0.1:9000/](http://127.0.0.1:9000/)


## Запуск проекта на удалённом сервере через Docker:

Выполнить вход на удаленный сервер.

Установить Docker Compose на сервер:
```
sudo apt update
sudo apt install curl
curl -fSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
sudo apt-get install docker-compose-plugin
```

Создать папку kittygram:
```
sudo mkdir kittygram
```

В папке kittygram создать файл docker-compose.production.yml и скопировать туда содержимое файла docker-compose.production.yml из проекта:
```
cd kittygram
sudo nano docker-compose.production.yml
```

В файл настроек nginx добавить домен сайта:
```
sudo nano /etc/nginx/sites-enabled/default
```

Из дирректории kittygram выполнить команды:
```
sudo docker compose -f docker-compose.production.yml pull
sudo docker compose -f docker-compose.production.yml down
sudo docker compose -f docker-compose.production.yml up -d
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic --noinput
sudo docker system prune -a
```
Проект будет доступен по адресу домена.


## Автор проекта:

[Ксения Тетерчева](https://github.com/GreenVibesOnly)

Всем мяу! :cat2:
