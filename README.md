#  Deployment Notes

## Recommended shape

Browser -> HTTPS load balancer/reverse proxy -> Node.js app instances -> managed PostgreSQL + object storage + email provider + payment provider.

The included SQLite database is for development/small testing only. For a real multi-instance launch, implement the PostgreSQL repository/migration layer before scaling horizontally.

## Docker

Build:
`docker build -t habeshan-dating-v7 .`

Run:
`docker run --env-file .env -p 3000:3000 habeshan-dating-v7`

## Provider adapters

V7 intentionally does not pretend to have live credentials or a live merchant account. The environment variables document the integration boundary. Select providers based on current availability, pricing, business registration/KYC requirements and your target customers, then implement and test signed webhooks and failure/retry handling.