# Let's Encrypt

## Automatic

```bash
npm install -g gitlab-letsencrypt

gitlab-le --email kayraalat@gmail.com --token ... --domain pryma.io www.pryma.io --repository https://gitlab.com/Tigin/pryma-landing --production
```

[gitlab-letsencrypt](https://github.com/rolodato/gitlab-letsencrypt)

## Manual

``` bash
brew install certbot
sudo certbot certonly --standalone -d domain.com -d www.domain.com
```

[https://certbot.eff.org/lets-encrypt/osx-other](https://certbot.eff.org/lets-encrypt/osx-other)

