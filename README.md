# Go API Boilerplate


## Folders structure

- `command/`: Console commands.
- `controller/`: Controllers for web requests processing.
- `db/`: Migrations.
- `dic/`: Dependency Injection Container.
- `doc/`: Swagger documentation.
- `docker/`: Docker containers description.
- `install/`: Scripts for environment preparing.
- `logger/`: Logger and client for Sentry.
- `model/`: Business logic.
- `model/db/`: DB connection.
- `model/entity/`: GORM entities.
- `model/repository/`: Repositories for access to storage.
- `model/service/`: Business logic.
- `route/`: Web requests routes.
- `test/`: Unit tests.
- `vendor/`: Packages used in application.
- `.env`: Environment variables for current environment.
- `base.env`: Base environment variables.


## How to use


### Prepare environment for Go projects if you do not done it early

```bash
sudo apt update
sudo apt upgrade
# See last version here: https://golang.org/dl/
wget https://dl.google.com/go/go1.11.1.linux-amd64.tar.gz
sudo tar -xvf go1.11.1.linux-amd64.tar.gz
sudo mv go /usr/local
sudo mcedit /etc/profile
```

And add last line:

```bash
export PATH=$PATH:/usr/local/go/bin
```

Update environment variables:

```bash
source /etc/profile
```

Check Go version:

```bash
go version
```

Now create folder for Go projects:

```bash
mkdir ~/go
cd ~/go
touch init.sh
mcedit init.sh
```

Paste next code into this file:

```bash
#!/bin/bash

export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```

Execute file:

```bash
chmod +x init.sh
source init.sh
```


### Install necessary packages

```bash
./install/install.sh
```


### Clone repo

```bash
git clone git@github.com:zubroide/go-api-boilerplate.git
cd go-api-boilerplate
```


### Create and edit config


```bash
cp .env.example .env
mcedit .env
```


### Download vendor packages

```bash
govendor sync
```


### Run migrations

Create database `go-api-boilerplate`.

And run migrations:

```bash
gorm-goose up
```


### Run application

```bash
gin -i run server
```

Or:

```bash
go run main.go server --port=8080
```

Check http://localhost:8080


### Run tests

Run all tests:

```bash
go test ./... -v -coverpkg=./... -coverprofile=coverage.out
go tool cover -html=coverage.out
```

Run test for one package:

```bash
go test go-api-boilerplate/test/unit -v -coverpkg=./... -coverprofile=coverage.out
```

Run one test:

```bash
go test test/unit/user_service_test.go -v -coverpkg=./... -coverprofile=coverage.out
```


### Generate Swagger documentation

Generate swagger.json:

```bash
swagger generate spec -o doc/swagger.json
```

Documentation must be available at url http://localhost:8080/swagger/index.html


## Support version
  - Go 1.11
