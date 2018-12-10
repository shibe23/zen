# Template Rails on Docker
- web: Rails
- db: MySQL
- server: nginx
- datastore: busybox

# Setup
- `docker-compose build`
- Add `gem 'unicorn'` and update Ruby version in Gemfile
- `docker-compose build` again
- `cp docker/rails/unicorn.rb config/`
- edit `config/database.yml`

```yml
default: &default
  adapter: mysql2
  encoding: utf8
  pool: 5
  username: root
  password: <%= ENV['MYSQL_ROOT_PASSWORD'] %>
  host: db
  socket: /tmp/mysql.sock
```
- `docker exec -it [web container name] bash`
- `rake db:create`

# Usage
- `docker-compose up`
- Access `localhost` or your docker-machine's IP

based on https://qiita.com/utahkaA/items/772cd80b893cd5367f38