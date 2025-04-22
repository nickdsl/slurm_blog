# Deployment (manual approach)

## Environment

Operating system: Ubuntu 22.04
System user with sudo: sysadm

## Deployment gist
```
# update && upgrade system
sudo apt update
sudo apt upgrade
# install required packages
sudo apt install postgresql redis-server golang-go nodejs npm

# configuring postgresql
sudo su - postgres
psql
create database blog;
create user blog_user with password 'blog_user_password';
alter database blog owner to blog_user ;
\q

# working with backend
cd backend-service
cp .env.example .env
# (optionally) edit .env file for customizing purposes

# building backend
go build -o backend-service

# making System-D service
sudo cp backend-service.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now backend-service

# working with frontend service
cd ../frontend-service
cp .env.example .env
# (optionally) edit .env file for customizing purposes

npm install
npm audit fix --force
npm run build 

# making System-D service
sudo cp frontend-service.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now frontend-service.service
```