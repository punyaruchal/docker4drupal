# PHP container

PHP is used with Nginx via PHP-FPM. 

## Drush

PHP container has installed drush. When running drush make sure to open the shell as user 82 (www-data) to avoid access problems in the web server, which is running as user 82, too:
```bash
$ docker-compose exec --user 82 php drush
```

Also, you can use preconfigured drush alias @dev:
```bash
$ docker-compose exec --user 82 php drush @dev
```

## Composer

PHP container has installed composer. Example:
```bash
$ docker-compose exec --user 82 php composer update
```

## Drupal Console

PHP container has installed drupal console. Example:
```bash
$ docker-compose exec --user 82 php drupal list
```

## Xdebug

If you want to use Xdebug, uncomment this line to enable it in the compose file before starting containers:
```yml
PHP_XDEBUG: 1                 # Enable Xdebug extension
PHP_XDEBUG_DEFAULT_ENABLE: 1  # Comment out to disable (default).
```

If you would like to autostart xdebug, uncomment this line:
```yml
PHP_XDEBUG_REMOTE_AUTOSTART: 1     # Comment out to disable (default).
```

## Xdebug on Mac OS X

There are two more things that need to be done on macOS in order to have Xdebug working (because there's no docker0 interface). Enable Xdebug as described in the previous section and uncomment the following two lines:

```yml
PHP_XDEBUG_REMOTE_CONNECT_BACK: 0         # Disabled for remote.host to work (enabled by default)
PHP_XDEBUG_REMOTE_HOST: "10.254.254.254"  # Setting the host (localhost by default)
```

You also need to have loopback alias with IP from above. You need this only once and that settings stays active until logout or restart.

```bash
sudo ifconfig lo0 alias 10.254.254.254
```

For more details see the issue with [Xdebug in Mac OS](https://github.com/Wodby/drupal-php/issues/1).

## Customization

See the list of environment variables available for customization at [wodby/drupal-php](https://github.com/wodby/drupal-php).
