## Run Backend tests with Phpunit

Backend tests are written using PHPUnit and API Platform testing tools.

### Setup Backend test environment

```bash
cd MyBank_backend
composer install --no-scripts'
php bin/console assets:install public'
php bin/console importmap:install'
docker compose -f compose.test.yaml up -d

```

### Run tests
```bash
docker exec mybank_backend_container php bin/console doctrine:migrations:migrate --env=test --no-interaction
docker exec mybank_backend_container php bin/console doctrine:fixtures:load --env=test --no-interaction
docker exec mybank_backend_container php bin/console lexik:jwt:generate-keypair --env=test
docker exec mybank_backend_container php bin/phpunit
```

### Clean up test environment

```bash
docker compose -f compose.test.yaml down --volumes
```

## Run Frontend tests 

Frontend tests are written using Vitest and React Testing Library.

### Setup the Frontend

```bash
cd MyBank_frontend
npm install
npm run test
```