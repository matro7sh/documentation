# Tests

## Run behat test 
```
make reset-db
docker-compose exec php sh
./vendor/bin/behat
```

>you can specify scenario like this `./vendor/bin/behat --name="Impact API testing"
