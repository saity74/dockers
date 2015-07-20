# Use with docker-compose
```ruby
joomla:
  command: php-fpm --allow-to-run-as-root
  image: buyanov/joomla-php5.6-fpm
  volumes:
    - fpm.conf:/usr/local/etc/php-fpm.conf
  links:
   - mysql
mysql:
  command: mysqld --user=root --verbose
  image: mysql
  volumes:
    - .mysql:/var/lib/mysql
    - mysql.cnf:/etc/mysql/my.cnf
  environment:
    MYSQL_DATABASE: joomla_db
    MYSQL_USER: joomla_user
    MYSQL_PASSWORD: joomla
    MYSQL_ALLOW_EMPTY_PASSWORD: yes
nginx:
  image: nginx
  volumes:
    - nginx.conf:/etc/nginx/conf.d/default.conf
    - html:/var/www/html
  ports:
   - "80:80"
  links:
   - joomla
```
