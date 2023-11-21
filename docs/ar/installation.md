# تثبيت

: انسخ المجلد على جهازك ثم قم بتشغيل الاوامر التالية 
 
```bash
# clone the repository
git clone git@github.com:matro7sh/Smersh.git

# go to the api/ folder
cd Smersh/api

# the values in there are safe to change
cp .env-dist .env
```

## استعمال docker

نحن نستخدم متغير يسمى المجال المعلن في ملف في جذر المشروع. هذا المتغير آمن

```bash
127.0.0.1    smersh.lan
127.0.0.1    api.smersh.lan
127.0.0.1    codimd.smersh.lan
127.0.0.1    bitwarden.smersh.lan
```


:لبدء التثبيت، قم بتشغيل الامر التالي 

`make initialize`.

عند اكتمال التثبيت، ستتمكن من تسجيل الدخول باستخدام المعرفات التالية

```bash
jenaye:jenaye
admin:admin
pentester:pentester
manager:manager
client:client
``` 

## يدويا

### تشغيل مشغل البرامج

```bash
docker-compose up  # when build is done do the next command
docker-compose exec php bin/console do:da:cr  # create database
docker-compose exec php bin/console do:sc:up --force # generation of tables
docker-compose exec php bin/console make:entity --overwrite #
docker-compose exec php bin/console doctrine:fixtures:load # load fake data

```

### إنشاء مفاتيح سرية

```bash
docker-compose exec php sh -c '
    set -e
    apk add openssl
    mkdir -p config/jwt
    jwt_passphrase=${JWT_PASSPHRASE:-$(grep ''^JWT_PASSPHRASE='' .env | cut -f 2 -d ''='')}
    echo "$jwt_passphrase" | openssl genpkey -out config/jwt/private.pem -pass stdin -aes256 -algorithm rsa -pkeyopt rsa_keygen_bits:4096
    echo "$jwt_passphrase" | openssl pkey -in config/jwt/private.pem -passin stdin -out config/jwt/public.pem -pubout
    setfacl -R -m u:www-data:rX -m u:"$(whoami)":rwX config/jwt
    setfacl -dR -m u:www-data:rX -m u:"$(whoami)":rwX config/jwt
'
```

## تكوين مشغل البرامج الخارج عن الشركة

```bash
# in .ssh (config file)
Host smersh
  Hostname <your-ip>
  Port <ssh-port>
  User <your-user>
  LocalForward 127.0.0.1:8000 127.0.0.1:8000
  LocalForward 127.0.0.1:4200 127.0.0.1:4200
  LocalForward 127.0.0.1:3000 127.0.0.1:3000
  LocalForward 127.0.0.1:8888 127.0.0.1:8888
```
