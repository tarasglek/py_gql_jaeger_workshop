## 1. Docker for Postgres database

Launch standard docker container with latest version of postgres.
## 2. Docker for database-loading script

https://dmitryrck.com/import-imdb/

Dockerize steps described in ^

Last step needs to be adjusted to be something like:

`s32imdbpy.py --verbose datasets.imdbws.com postgresql://taras@localhost/taras`

After loading the db, follow instructions in https://github.com/tarasglek/imdb-graphql/blob/master/src/postgres/README.md to enable search queries.

## 3. Docker for Graphql backend

Stand up https://github.com/tarasglek/imdb-graphql

Notes on how to start app in https://github.com/tarasglek/imdb-graphql/tree/master/src/python

** TODO: @1mehal setup backend using hasura

## 4. Run jaeger docker

```
    docker run -d --name jaeger \
  -e COLLECTOR_ZIPKIN_HOST_PORT=:9411 \
  -p 5775:5775/udp \
  -p 6831:6831/udp \
  -p 6832:6832/udp \
  -p 5778:5778 \
  -p 16686:16686 \
  -p 14268:14268 \
  -p 14250:14250 \
  -p 9411:9411 \
  jaegertracing/all-in-one:1.25
```
UI will be accessible at
http://localhost:16686/

## 5. Modify graphql backend with opentracing such that it can report into jaeger

https://github.com/opentracing-contrib/python-sqlalchemy


## 6. Fix some slow query discovered above

## 7. Package all of ^ in docker-compose

`docker-compose up` should be able to bring up following containers

1. Postgres
2. Conditional data-loader
3. Graphql api server
4. Jaeger tracing UI

## 8. Bring up or down ^ in AWS/Kubernetes/etc with single command
