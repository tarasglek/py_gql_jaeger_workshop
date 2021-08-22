## 1. Docker for Postgres database

Launch standard docker container with latest version of postgres.
## 2. Docker for database-loading script
https://dmitryrck.com/import-imdb/

Dockerize steps described in ^

Last step needs to be adjusted to be something like:

`s32imdbpy.py --verbose datasets.imdbws.com postgresql://taras@localhost/taras`

## 3. Setup Graphql backend

https://github.com/kiendang/imdb-graphql

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

## 5. Modify graphql backend with opentracing such that it can report into jaeger

https://github.com/opentracing-contrib/python-sqlalchemy


## 6. Fix some slow query discovered above

