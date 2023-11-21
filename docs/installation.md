# Installation

Clone and go to the `api/` folder. Once this is done, copy `.env-dist` to `.env`:

```bash
# clone the repository
git clone git@github.com:matro7sh/Smersh.git

# go to the api/ folder
cd Smersh/api

# the values in there are safe to change
cp .env-dist .env
```

## Using Docker

We are using an environment variable called DOMAIN declared in the `.env` file at the root of the project.
This variable is safe to override. Either way, you will need add some urls to the `/etc/hosts` file, like so:

```bash
# assuming your DOMAIN variable is the default one, this is what you will need to add
# if your DOMAIN is different, every `smersh.lan` should be replaced by the
# domain you selected

127.0.0.1    smersh.lan
127.0.0.1    api.smersh.lan
127.0.0.1    codimd.smersh.lan
127.0.0.1    bitwarden.smersh.lan
```

As we use træfik as reverse-proxy, you can refer to [their documentation](https://doc.traefik.io/traefik/contributing/documentation/) to learn how to customize this instance.

To start the install, you can just run `make initialize`.

If you are using the default setup, you will need to accept the generated SSL certificates for the API, before logging in.
Go to `https://api.smersh.lan` and accept the SSL certificates, then do the same for the [web client](https://smersh.lan).

If everything is working properly, you can go to [http://smersh.lan](http://smersh.lan) and use `jenaye:jenaye` to log in.
Other credentials are there by default, such as `admin:admin`, `pentester:pentester`, `manager:manager`, and `client:client`.

## Manually

### Running the API

```bash
docker-compose up  # when build is done do the next command
docker-compose exec php bin/console do:da:cr  # create database
docker-compose exec php bin/console do:sc:up --force # generation of tables
docker-compose exec php bin/console make:entity --overwrite #
docker-compose exec php bin/console doctrine:fixtures:load # load fake data

```

### Generating a JWT secret

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

## Accessing SMERSH from a Virtual Private Server

You have to create a file named `config` into the `.ssh/` folder of you current user (your host).

```bash
Host smersh
  Hostname <your-ip>
  Port <ssh-port>
  User <your-user>
  LocalForward 127.0.0.1:8000 127.0.0.1:8000
  LocalForward 127.0.0.1:4200 127.0.0.1:4200
  LocalForward 127.0.0.1:3000 127.0.0.1:3000
  LocalForward 127.0.0.1:8888 127.0.0.1:8888
```

Then you can run `ssh smersh` and go to [http://localhost:4200](http://localhost:4200).

