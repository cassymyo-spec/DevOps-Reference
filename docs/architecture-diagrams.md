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
