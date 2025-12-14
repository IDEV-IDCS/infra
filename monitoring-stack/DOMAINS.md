# Domain Configuration for devcode.live

## Suggested Subdomains

Configure these domains in Dokploy for your monitoring stack:

### Primary Services
- `grafana.devcode.live` → grafana:3000 (Main dashboard)
- `umami.devcode.live` → umami:3000 (Web analytics)
- `posthog.devcode.live` → posthog:8000 (Session replays & analytics)

### Internal Services (Optional)
- `prometheus.devcode.live` → prometheus:9090 (Metrics)
- `loki.devcode.live` → loki:3100 (Logs)
- `alloy.devcode.live` → alloy:12345 (Collector)

## DNS Setup
Create A records pointing to your server IP:
```
grafana.devcode.live    → YOUR_SERVER_IP
umami.devcode.live      → YOUR_SERVER_IP
posthog.devcode.live    → YOUR_SERVER_IP
```

## Dokploy Configuration
1. Deploy the Docker Compose stack
2. In Dokploy dashboard, configure domains for each service
3. Enable SSL certificates (Let's Encrypt)
4. Traefik will handle routing automatically
