Build the project
`docker-compose run web rails new . --force --no-deps --database=postgresql`
If you are running Docker on Linux, the files rails new created are owned by root.
`sudo chown -R $USER:$USER .`
Now that you’ve got a new Gemfile, you need to build the image again
`docker-compose build`
Connect the database
Replace the contents of config/database.yml with the following:
`default: &default
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
  database: myapp_test`
You can now boot the app with `docker-compose up`
