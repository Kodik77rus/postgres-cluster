# postgres-cluster

![sceme](<img/scheme.jpg>)

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
  Во время тестов с 22:00 до 1:00 21.06.2023 сеть, возможно, сеть была забита, потому что на haproxy запросы шли, а до pgbouncer не доходили, соотвественно коннекты к бд не доходили, а потом все было нормально, время кончлось и нормально получилось сделать только первый тест.

## Тест 1
Тут я насиловал бд, упёрся в ошибку, что либо pgbouncer обрубал коннекты, либо haproxy обрубал коннекты

Результаты теста:

![test-result](<img/test-1/Screenshot from 2023-06-22 02-21-41.png>)

Считаю, что можно было больше выжить, потому что загруженность остальных сервисов была слабая [](<img/test-1/Screenshot from 2023-06-22 02-27-20.png>)

![sceme](<img/test-1/Screenshot from 2023-06-22 02-27-35.png>)


## Тест 2

## Тест 3
