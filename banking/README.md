# Banking Spring Boot service

Run the application and PostgreSQL database from this directory:

```powershell
docker compose up -d --build
docker compose logs -f account-service
```

The `account-service` connects to `banking_db` through the `core-db` Compose
service and creates the `accounts` table on startup. PostgreSQL is also
available on port `5432`, and the service listens on port `8080`.

Create an account with `POST http://localhost:8080/api/accounts` and this JSON
body:

```json
{
  "accountNumber": "1000000001",
  "accountHolderName": "Nguyen Van A",
  "balance": 5000000.00
}
```

The service responds with `201 Created` and the saved account, including its
database-generated `id`. Retrieve accounts with `GET
http://localhost:8080/api/accounts` or one account with
`GET http://localhost:8080/api/accounts/{id}`. Account numbers must be unique
and balances cannot be negative.

The credentials in `docker-compose.yml` are for local exercise use only;
replace them before using this setup outside a local environment.

If host port `5432` is already in use, set `POSTGRES_HOST_PORT` to another
available port before starting Compose. The application still connects to
PostgreSQL internally on port `5432`.

Stop the containers with `docker compose down`. Add `-v` to also remove the
local PostgreSQL data volume.
