# Deployment (docker approach)

## Environment

Operating system: Linux with docker installed

## Deployment gist
```
cp frontend-service/.env.example frontend-service/.env
# (edit frontend-service/.env)
# edit environment variables for docker-compose file
docker compose up -d
```