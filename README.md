## Golang Simple Jenkins

## Run Project

```bash
go run main.go
```

## Run Test

```bash
GIN_MODE=release go test -v
```

## Docker Compose Run

```bash
DB_HOST=product-db DB_PORT=5433 DB_NAME=postgres DB_USER=postgres DB_PASSWORD=P@ssw0rd API_PORT=8888 docker compose up
```
