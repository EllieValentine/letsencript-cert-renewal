# A guide to issuing certificates for Let’s Encrypt using Docker.


## <a href="./http-01-challenge">HTTP Challenge</a>

This is the most common challenge type today. Let’s Encrypt gives a token to your ACME client, and your ACME client puts a file on your web server at http://{DOMAIN>}.well-known/acme-challenge/{TOKEN}. <a href="https://letsencrypt.org/docs/challenge-types/#http-01-challenge">More</a>.

## Use

1. Provide a valid email address and specify the required domains in <a href="./http-01-challenge/docker-compose.yml">docker compose file</a>.

2. In accordance with the specified data, change the <a href="./http-01-challenge/server/default.conf">settings for Nginx</a>.

<hr>

## <a href="./dns-01-challenge">DNS-01 challenge (DigitalOcean)</a>

This challenge asks you to prove that you control the DNS for your domain name by putting a specific value in a TXT record under that domain name. It is harder to configure than HTTP-01, but can work in scenarios that HTTP-01 can’t. It also allows you to issue <strong>wildcard certificates</strong>. <a href="https://letsencrypt.org/docs/challenge-types/#dns-01-challenge">More</a>.

The example uses certbot <a href="https://hub.docker.com/r/certbot/dns-digitalocean">image</a> for DigitalOcean DNS. <a href="https://eff-certbot.readthedocs.io/en/stable/install.html#running-with-docker">Find out more</a>.


## Use

1. <a href="./dns-01-challenge/certbot/conf/.env">Specify access keys</a> for DigitalOcean API.

2. Provide a valid email address and specify the required domains in <a href="./dns-01-challenge/docker-compose.yml">docker compose file</a>.

<hr>

## Notes
Please note that certificates will not renew themselves. You need to do it manually or modify the examples or use Jenkins or other CI/CD tools.

It is recommended (including by  Let’s Encrypt itself) to issue certificates on a separate server and then forward them to the servers that will use them. Therefore, the HTTP challenge does not seem to be the best solution in the case, preference should be given to DNS challenge. Also, if possible, use SAN instead of Wildcard.