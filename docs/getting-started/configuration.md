---
title: Configuration
slug: configuration
sidebar_position: 2
---

Here you can see an example .env file:
```ini title=".env.example"
# Can be either 'prod' or 'dev'.
# In 'dev' mode, a reflection server is established.
MODE=dev

SERVER_HOST=localhost
SERVER_PORT=3000

# As for now, only PostgreSQL is supported
DATABASE_HOST=localhost
DATABASE_PORT=54321
DATABASE_USER=postgres
DATABASE_PASS=postgres
DATABASE_NAME=goipay_db

XMR_DAEMON_URL=http://node.monerodevs.org:38089
XMR_DAEMON_USER=
XMR_DAEMON_PASS=
```