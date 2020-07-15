# Docker-email
Why don't we use docker container for mail service?

```bash
curl -s https://raw.githubusercontent.com/theraw/docker-email/theraw-beta1/dopemail.yml > dopemail.yml; nano dopemail.yml

docker-compose -f dopemail.yml up -d

# Create rabbitmq user
1. docker exec -it rabbitmq bash
2. bash /root/user.sh; exit

# Generate SSL certificate for your domain and create dashboard user
3. docker stop postal; docker start postal; docker exec -it postal bash
4. nano /bin/ssl (fill required details cloudflare api key/ email these are required only for ssl certificate generation you can bypass this step if you already have a ssl cert)
5. ssl yourdomain.com
6. postal make-user

# Update nginx/postal config (replace domain name)
7. perl -pi -e 's/rawmail.nl/YOURDOMAIN.COM/g' /etc/nginx/sites-enabled/default
8. perl -pi -e 's/rawmail.nl/YOURDOMAIN.COM/g' /opt/postal/config/postal.yml
9. exit
10. docker stop postal; docker start postal

Visit https://yourdomain.com
```
