# 💰 MyBank — Symfony + React (Vite)

MyBank is a simple web application for managing personal finances.

## Features

- User registration and login
- Adding, editing, and deleting operations
- Adding, editing, and deleting categories
- Filter operations by category
- Dashboard view with all operations

## Getting Started

### Prerequisites

- PHP >= 8.1
- Node.js >= 18
- Composer
- Mysql
- Docker

## Deploy with Docker (recommanded)

### Quick setup with Docker Compose

```bash
docker compose up --build -d
docker exec mybank_backend_container php bin/console doctrine:migrations:migrate --no-interaction
docker exec mybank_backend_container php bin/console lexik:jwt:generate-keypair
```

This will:

- Create a dedicated Docker network (if not exists)
- Start the backend and database services
- Start the frontend 


#### ⚠️ Possible Migration Error

When running the following command:

```bash
docker exec mybank_backend_container php bin/console doctrine:migrations:migrate --no-interaction
``` 

You might encounter the following error: `SQLSTATE[HY000] [2002] Connection refused`

This usually happens because the database container is not fully ready yet.
Solution: Simply wait a few seconds and re-run the command.

## Deploy locally

### Backend

#### Install the dependencies

```bash
cd MyBank_backend
php bin/console assets:install public
php bin/console importmap:install

```

#### Create the database and run the migrations:

```bash
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
php bin/console lexik:jwt:generate-keypair
```

#### Run the backend locally

```bash
symfony server:start
``` 

The backend will be available at: http://localhost:8082/


### Frontend

```bash
cd MyBank_frontend
npm install
npm run dev
```

The frontend will be available at: http://localhost:5173/

## Authentication

- JWT authentication is used.
- The token is stored in localStorage
- Axios interceptors are used to attach the token to every request.