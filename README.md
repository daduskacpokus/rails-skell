FROM [docker/official](https://docs.docker.com/compose/rails/)
### Build the project

`docker-compose run web rails new . --force --no-deps --database=postgresql`

If you are running Docker on Linux, the files rails new created are owned by root.

`sudo chown -R $USER:users .`

### Connect the database

`echo "" > config/database.yml`

`vi config/database.yml`

Replace the contents of config/database.yml with the following:

```
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password:
  pool: 5

development:
  <<: *default
  database: myapp_development


test:
  <<: *default
  database: myapp_test
```

`docker-compose build`

Finally, you need to create the database. In another terminal, run:

`sudo chown -R $USER:users tmp/*`

`docker-compose run web rake db:create`

You can now boot the app with:

`docker-compose up`

