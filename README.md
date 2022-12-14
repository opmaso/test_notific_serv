Сервис уведомлений
Тестовое задание для кандидатов-разработчиков
Тестовое задание – дополнительный способ для нас убедиться в вашей квалификации и понять, какого рода задачи вы выполняете эффективнее всего.
Расчётное время на выполнение тестового задания: 3-4 часа, время засекается нестрого. Приступить к выполнению тестового задания можно в любое удобное для вас время.
У текущего тестового задания есть только общее описание требований, конкретные детали реализации остаются на усмотрение разработчика. Решение по стеку технологий, которые необходимы для решения задачи, также принимает кандидат по своему усмотрению.
Задача :
Необходимо разработать сервис управления рассылками API администрирования и получения статистики.
Описание :
Необходимо реализовать методы создания новой рассылки, просмотра созданных и получения статистики по выполненным рассылкам.

Реализовать сам сервис отправки уведомлений на внешнее API.

Опционально вы можете выбрать любое количество дополнительных пунктов описанных после основного.
Для успешного принятия задания как выполненного достаточно корректной и рабочей реализации требований по основной части, но дополнительные пункты помогут вам продемонстрировать ваши навыки в смежных технологиях.
Критерии приёмки

Выполненное задание необходимо разместить в публичном репозитории на gitlab.com

Понятная документация по запуску проекта со всеми его зависимостями

Документация по API для интеграции с разработанным сервисом

Описание реализованных методов в формате OpenAPI

Если выполнено хотя бы одно дополнительное задание - написать об этом в документации, указав на конкретные пункты из списка ниже.
Основное задание
Спроектировать и разработать сервис, который по заданным правилам запускает рассылку по списку клиентов.
Сущность "рассылка" имеет атрибуты:

уникальный id рассылки

дата и время запуска рассылки

текст сообщения для доставки клиенту

фильтр свойств клиентов, на которых должна быть произведена рассылка (код мобильного оператора, тег)

дата и время окончания рассылки: если по каким-то причинам не успели разослать все сообщения - никакие сообщения клиентам после этого времени доставляться не должны
Сущность "клиент" имеет атрибуты:

уикальный id клиента

номер телефона клиента в формате 7XXXXXXXXXX (X - цифра от 0 до 9)

код мобильного оператора

тег (произвольная метка)

часовой пояс
Сущность "сообщение" имеет атрибуты:

уникальный id сообщения

дата и время создания (отправки)

статус отправки

id рассылки, в рамках которой было отправлено сообщение

id клиента, которому отправили
Спроектировать и реализовать API для:

добавления нового клиента в справочник со всеми его атрибутами

обновления данных атрибутов клиента

удаления клиента из справочника

добавления новой рассылки со всеми её атрибутами

получения общей статистики по созданным рассылкам и количеству отправленных сообщений по ним с группировкой по статусам

получения детальной статистики отправленных сообщений по конкретной рассылке

обновления атрибутов рассылки

удаления рассылки

обработки активных рассылок и отправки сообщений клиентам
Логика рассылки

После создания новой рассылки, если текущее время больше времени начала и меньше времени окончания - должны быть выбраны из справочника все клиенты, которые подходят под значения фильтра, указанного в этой рассылке и запущена отправка для всех этих клиентов.

Если создаётся рассылка с временем старта в будущем - отправка должна стартовать автоматически по наступлению этого времени без дополнительных действий со стороны пользователя системы.

По ходу отправки сообщений должна собираться статистика (см. описание сущности "сообщение" выше) по каждому сообщению для последующего формирования отчётов.

Внешний сервис, который принимает отправляемые сообщения, может долго обрабатывать запрос, отвечать некорректными данными, на какое-то время вообще не принимать запросы. Необходимо реализовать корректную обработку подобных ошибок. Проблемы с внешним сервисом не должны влиять на стабильность работы разрабатываемого сервиса рассылок.
API внешнего сервиса отправки
Для интеграции с разрабатываемым проектом в данном задании существует внешний сервис, который может принимать запросы на отправку сообщений в сторону клиентов.
OpenAPI спецификация находится по адресу: https://probe.fbrq.cloud/docs
В этом API предполагается аутентификация с использованием JWT. Токен доступа предоставлен вам вместе с тестовым заданием.
Дополнительные задания :
Опциональные пункты, выполнение любого количества из приведённого списка повышают ваши шансы на положительное решение о приёме
1 организовать тестирование написанного кода
2 обеспечить автоматическую сборку/тестирование с помощью GitLab CI
3 подготовить docker-compose для запуска всех сервисов проекта одной командой
4.написать конфигурационные файлы (deployment, ingress, …) для запуска проекта в kubernetes и описать как их применить к работающему кластеру

5 сделать так, чтобы по адресу /docs/ открывалась страница со Swagger UI и в нём отображалось описание разработанного API. Пример: https://petstore.swagger.io

6 реализовать администраторский Web UI для управления рассылками и получения статистики по отправленным сообщениям

## Установка и запуск

1. Клонировать репозиторий с Github:

````
git clone https://github.com/opmaso/test_notific_serv.git
````
2. Перейти в директорию проекта

3. Создать виртуальное окружение:

````
python -m venv venv
````

4. Активировать окружение: 

````
source\venv\bin\activate
````
5. В файле .evn заполнить необходимые данные: ```TOKEN = '<your token>'```
 
6. Установка зависимостей:

```
pip install -r requirements.txt
```

7. Создать и применить миграции в базу данных:
```
python manage.py makemigrations
python manage.py migrate
```
8. Запустить сервер
```
python manage.py runserver
```
9. Запустить celery
```
celery -A notification_service worker -l info
```
10. Запустить flower

```
celery -A notification_service flower --port=5555
```
***
### Запуск тестов
``` 
python manage.py test
```
***
## Установка проекта с помощью docker-compose


1. Склонировать репозиторий с Github
```
git clone git@github.com:Witaly3/notification_service.git
```
2. Перейти в директорию проекта
3. В файле .evn заполнить необходимые данные: ```TOKEN = '<your token>'```
4. Запустить контейнеры 
``` 
sudo docker-compose up -d
 ```
5. Остановка работы контейнеров 
```
sudo docker-compose stop
```
***
```http://0.0.0.0:8000/api/``` - api проекта

```http://0.0.0.0:8000/api/clients/``` - клиенты

```http://0.0.0.0:8000/api/mailings/``` - рассылки

```http://0.0.0.0:8000/api/mailings/fullinfo/``` - общая статистика по всем рассылкам

```http://0.0.0.0:8000/api/mailings/<pk>/info/``` - детальная статистика по конкретной рассылке

```http://0.0.0.0:8000/api/messages/``` - сообщения

```http://0.0.0.0:8000/docs/``` - docs проекта

```http://0.0.0.0:5555``` - celery flower

***
