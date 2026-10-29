# Akindev-database
Sunucunun Datasını Yedeğini Alan Sistem SQL

Belirli aralikla MySQL/MariaDB yedegi alir (`sql/` klasorune `.sql.gz`), istenirse Discord'a gonderir.

## Kurulum (server.cfg)

```cfg
# Webhook'u config.json yerine buraya yazin
set akindev_db_webhook "https://discord.com/api/webhooks/ID/TOKEN"

# Istege bagli: oxmysql kullaniyorsaniz mysql_connection_string otomatik okunur.
# Yedek icin ayri kullanici kullanmak isterseniz:
# set akindev_db_connection "mysql://yedek:SIFRE@localhost:3306/akindev"

ensure Akindev_database
```

## Yedek kullanicisi (root yerine)

```sql
CREATE USER 'yedek'@'localhost' IDENTIFIED BY 'GUCLU_SIFRE';
GRANT SELECT, SHOW VIEW, TRIGGER, LOCK TABLES ON akindev.* TO 'yedek'@'localhost';
FLUSH PRIVILEGES;
```

## Ayarlar (config.json)

- `interval.time`: dakika (en az 5, varsayilan 60)
- `backup.keepLast`: sunucuda saklanacak yedek sayisi
- `backup.runOnStart`: true ise kaynak acilir acilmaz ilk yedegi alir
- `discord.maxUploadMB`: bundan buyuk yedekler Discord'a yuklenmez, sadece bildirim gider
