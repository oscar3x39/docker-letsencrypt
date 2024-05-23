# Automatic SSL Certificate Renewal with Certbot

This Docker Compose configuration is designed to assist you in automatically renewing SSL certificates using Certbot. Certbot is a tool for automatically managing SSL/TLS certificates, making it easy to set up HTTPS on your server.

## Usage:

1. Clone or download this repository to your server.

2. Create a file named .env in the root directory of the project and add the following content:

```
CERTBOT_EMAIL=test@example.com
CERTBOT_DOMAIN=test.example.com
WEB_ROOT=/var/www/html
```

Replace CERTBOT_EMAIL and CERTBOT_DOMAIN with your email address and domain name, and WEB_ROOT with the path to your web root directory.

3. Run the following command to start the Docker containers:
```
docker-compose up -d
```

This will start the Certbot container and generate SSL certificates for your domain.

4. When your certificates are nearing expiration, Certbot will attempt to renew them automatically. You can find the certificate files in the /etc/letsencrypt/live/<your-domain>/ directory.

5. Scheduling Automatic Renewal:

To schedule the execution of docker-compose up -d and removal of containers at the end of each month, you can use cron jobs on your server:

- Edit your crontab file by running:

```
crontab -e
```

- Add the following line to the crontab file:

```
59 23 28-31 * * cd /path/to/your/project && docker-compose up -d && docker-compose down
```

This cron job will execute the entire command at 23:59 (11:59 PM) on the 28th, 29th, 30th, and 31st day of each month.
