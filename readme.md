### поднять контейнер
`docker-compose up -d`

### опустить контейнер
`docker-compose down`

---

### сайт доступен по ссылке 
#### `http://localhost`

### для битрикса
заменить содержимое конфига nginx на `_docker/config/nginx/nginx_bitrix.conf`

---

### войти в bash
`docker exec -it project_app bash`

### перезагрузить nginx, не входя в bash
`docker exec project_nginx nginx -s reload`

---

### в .env указывать
`DB_CONNECTION=mysql`
`DB_HOST=db` - имя контейнера с бд
`DB_PORT=3306`
`DB_DATABASE=db`
`DB_USERNAME=root`
`DB_PASSWORD=root`

---

### в sequel указывать
`type: tcp/ip`
`host: localhost`
`user: root`
`password: root`
`port: 8886`

---

### в adminer http://localhost:8080 указывать
`Сервер: db` - имя контейнера с бд
`Имя: root`
`Пароль: root`

---

### подключение к эластику
`$client = Elastic\Elasticsearch\ClientBuilder::create()->setHosts(['project_elasticsearch:9200'])->build();
echo $client->info()['version']['number']; // 8.10.3`

#### в postman:
http://localhost:9200

---

### memcache
`$memcache = new Memcache();
$memcache->connect('project_memcached', 11211);
dump($memcache->getStats());`

#### bitrix .settings.php:
'cache' => [
    'value' => [
    'sid' => $_SERVER['DOCUMENT_ROOT'] . '#dev.local',
    'type' => 'memcache',
        'memcache' => [
            'host' => 'project_memcached',
            'port' => '11211',
        ],
    ],
],

#### bitrix dbconn.php:
`define('BX_CACHE_TYPE', 'memcache');
define('BX_CACHE_SID', $_SERVER['DOCUMENT_ROOT'] . '#dev.local');
define('BX_MEMCACHE_HOST', 'project_memcached');
define('BX_MEMCACHE_PORT', '11211');`

---

### smtp
#### в .env указать:
`MAIL_HOST=smtp.yandex.ru
MAIL_PORT=587
MAIL_USERNAME=почта@yandex.ru
MAIL_PASSWORD=пароль_приложения
MAIL_ENCRYPTION=tls`