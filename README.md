# OneClick Compose Fixture

Public fixture repository for testing OneClickHost multi-node Compose deploy.

## Services

- `frontend`: static Nginx app on port `8080`; proxies same-origin `/api/*`
  requests to the internal `api:8000` Compose service.
- `api`: FastAPI app on port `8000`; checks PostgreSQL connectivity and stores
  a tiny visit counter.
- `db`: PostgreSQL 16 internal service. It must not be exposed publicly.

## OneClickHost Compose Config

Repository:

```text
https://github.com/tuankiet18-dev/oneclick-compose-fixture
```

Branch:

```text
main
```

Compose file:

```text
docker-compose.yml
```

Routes:

| Route slug | Service | Internal port |
|---|---|---:|
| `app` | `frontend` | `8080` |

Environment variables:

| Service | Key | Value | Secret |
|---|---|---|---|
| `api` | `DATABASE_URL` | `postgresql://oneclick:oneclick@db:5432/oneclick_fixture` | yes |

Expected checks:

```bash
curl http://app-<project>.<control-plane-ip>.sslip.io
curl http://app-<project>.<control-plane-ip>.sslip.io/api/health
curl http://app-<project>.<control-plane-ip>.sslip.io/api/db-check
```
