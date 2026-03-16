Public Internet
                 │
         YourDomain.com / Subdomains
                 │
           Public IP (Contabo)
                 │
           ┌────────────┐
           │  Host OS   │  <-- Ubuntu or Debian
           └────────────┘
                 │
         ┌───────┴────────┐
         │ Docker Engine  │
         └───────┬────────┘
                 │
   ┌─────────────┴─────────────┐
   │                             │
┌────────────┐             ┌─────────────┐
│ Production │             │ Staging     │
│ Container  │             │ Container   │
│ (App live) │             │ (Testing)   │
└────────────┘             └─────────────┘
       │                           │
       └────────────┬──────────────┘
                    │
          ┌─────────┴─────────┐
          │ NGINX Reverse     │
          │ Proxy Container   │
          └─────────┬─────────┘
                    │
        Routes traffic based on:
   production.yourdomain.com → Production Container
   staging.yourdomain.com    → Staging Container





compose

┌───────────────┐
                 │   Browser /   │
                 │   Client UI   │
                 └───────┬───────┘
                         │ HTTP Requests
                         ▼
                 ┌───────────────┐
                 │   Django App  │  ←─ Code runs inside 'web' container
                 │  (web service)│
                 └───────┬───────┘
                         │ ORM Queries
                         ▼
                 ┌───────────────┐
                 │   Postgres    │  ←─ 'db' container stores persistent data
                 └───────────────┘

Django also sends async tasks to Celery via Redis:
                         │
                         │ Celery Task Message
                         ▼
                 ┌───────────────┐
                 │    Redis      │  ←─ 'redis' container as message broker
                 └───────┬───────┘
                         │ Task Delivery
                         ▼
                 ┌───────────────┐
                 │   Celery      │  ←─ 'celery' container processes tasks
                 │   Worker      │
                 └───────────────┘
                         │ Writes results
                         ▼
                 ┌───────────────┐
                 │   Postgres    │  ←─ Tasks can update DB or trigger events
                 └───────────────┘







   
