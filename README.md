# postgres-cluster

![scheme](<img/scheme.jpg>)

## Стек

- Confd
- Etcd
- Grafana
- Haproxy
- Patroni
- Pgbouncer
- PostgreSQL 15
- Prometheus

## Конфиги

- [etcd1](configs/etcd1.yml)
- [etcd2](configs/etcd2.yml)
- [etcd3](configs/etcd3.yml)
- [haproxy](configs/haproxy.cfg)
- [pgbouncer1](configs/pgbouncer1.ini)
- [pgbouncer2](configs/pgbouncer2.ini)
- [pgsql-master](configs/pgsql-master.yml)
- [pgsql-replica-1](configs/pgsql-replica-1.yml)
- [pgsql-replica-2](configs/pgsql-replica-2.yml)
- [pgsql-replica-3](configs/pgsql-replica-3.yml)

## Примечание

  Во время тестов с 22:00 до 1:00 21.06.2023 сеть, возможно, сеть была забита, потому что на haproxy запросы шли, а до pgbouncer не доходили, соответственно, коннекты к бд не доходили, а потом все было нормально, время кончилось и нормально получилось сделать только первый тест.

  В некоторых скринах разный пользователь, но я прописывал:

  ``` sql
    grant all privileges on database rebrain_courses_db to rebrain_admin;
  ```

## Тест 1

Тут я насиловал бд, упёрся в ошибку, что haproxy обрубал коннекты, если их было больше 510, хотя в конфиге прописано 1024 <a>![haproxy](<img/test-1/Screenshot from 2023-06-22 02-35-05.png>)</a>

Результаты теста:

![test-result](<img/test-1/Screenshot from 2023-06-22 02-21-41.png>)

Общая нагрузка на тачку:
![node-exporter](<img/test-1/Screenshot from 2023-06-22 02-27-35.png>)

> Считаю, что можно было больше выжить, потому что загруженность остальных сервисов была слабая <a>![пример](<img/test-1/Screenshot from 2023-06-22 02-18-57.png>)</a>

Статистика по postgres:

уперлись в лимит в 300 tps

![postgres-exporter](<img/test-1/Screenshot from 2023-06-22 02-27-44.png>)

## Тест 2

тест идёт
![test](<img/test2/Screenshot from 2023-06-21 23-49-37.png>)

прокси работает (для 1 теста я повышал максимальное число коннектов)
![haproxy](<img/test2/Screenshot from 2023-06-21 23-44-24.png>)

ничего не происходит
![node-exporter](<img/test2/Screenshot from 2023-06-21 23-41-56.png>)
![postgres-exporter](<img/test2/Screenshot from 2023-06-21 23-42-04.png>)

## Тест 3

Переключение патрони:
![patroni](<img/test-3/Screenshot from 2023-06-22 00-16-31.png>)

тест идёт, шаблон confd на pgbouncer отработал, скрина не делал
![test](<img/test-3/Screenshot from 2023-06-22 00-16-50.png>)

коннектов нет
![connection](<img/test-3/Screenshot from 2023-06-22 00-29-13.png>)
