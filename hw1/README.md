# MongoDB
Докер был уже скачан:

<img src="pics/1-docker.png" alt="drawing" width="200"/>

Далее был скачан образ MongoDB

<img src="pics/2-mongo-image.png" alt="drawing" width="500"/>

И запушен с маунтом директории в которой будут лежать данные, чтобы они не потеряли.

<img src="pics/3-start-container.png" alt="drawing" width="500"/>

Загрузим данные для тестов: датасет аналитики (customers, accounts, transactions).

```sh
docker cp customers.json mongodb:/data/db/customers.json
docker exec -it mongodb bash 
mongoimport --db analytics --collection customers --file /data/db/customers.json
```
<img src="pics/4-data.png" alt="drawing" width="500"/>

Далее для взаимодеиствия внутри контейнера перейдем в интерактивный режим и посмотрим, что мы насоздавали: видим базы данных analytics с созданными коллекциями.

<img src="pics/5-mongosh.png" alt="drawing" width="500"/>

Рассмотрим данные подробнее с помощью команды `db.collection_name.find()`.

`db.accounts.find()`
<img src="pics/6-accounts.png" alt="drawing" width="500"/>

`db.customers.find()`
<img src="pics/7-customers.png" alt="drawing" width="500"/>

`db.transactions.find()`
<img src="pics/8-transactions.png" alt="drawing" width="500"/>

Так же можем задать фильтры, в данном случае по лимиту у аккаунты (меньше 1000).
<img src="pics/9-limit.png" alt="drawing" width="500"/>

## Теперь сделаем несколько CRUD:

### Create:
<img src="pics/10-create.png" alt="drawing" width="500"/>

### Read:
<img src="pics/11-read.png" alt="drawing" width="500"/>

### Update:
<img src="pics/12-update.png" alt="drawing" width="500"/>
<img src="pics/13-update.png" alt="drawing" width="500"/>

### Delete:
<img src="pics/14-delete.png" alt="drawing" width="500"/>

## Производительность

Для этого нужен датасет побольше, так как здесь операции выполняются за 1мс. [Возьмем этот](https://www.kaggle.com/datasets/shrashtisinghal/mongo-db-datsets?resource=download). Здесь представлены различные публикации, пример одного объекта ниже.

<img src="pics/20-publ-obj.png" alt="drawing" width="400"/>

<img src="pics/15-big-data.png" alt="drawing" width="500"/>

Размер дата сета:

<img src="pics/16-data.png" alt="drawing" width="150"/>

Тогда попробуем сделать запрос по номеру книги. Время: 233мс.

<img src="pics/17-no.png" alt="drawing" width="500"/>

Теперь с индексами. Время: 233мс.
<img src="pics/18-indexes.png" alt="drawing" width="500"/>

Казалось, что такие индексы увеличат производительность, однако прибавки не заметно. Хотя каждая публикация имеет номер и казалось бы, что это поле  должно быть хорошим для индексации.

# Выводы 
В целом удобная достаточно быстро развертываемая база данных. Есть множество интерфейсов взаимодействия на все вкусы. Опыт использования положительный.