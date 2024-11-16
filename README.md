# certbot-dns-20i

20i DNS Authenticator plugin for certbot

This plugin automates the process of completing a dns-01 challenge by creating, and subsequently removing, TXT records using the 20i's reseller REST API.

## Installation

```shell
pip install git+https://github.com/yt-easytouch/certbot-dns-20i
```

## Credentials

Obtain an API key from 20i (https://my.20i.com/reseller/api).

You can use this in conjunction with a subuser username to restrict access to this subuser's scope.

Create a JSON credential file with 600 permissions for use by the plugin, and add a `username` if necessary:
```json
{
  "bearer": "BEARER TOKEN HERE"
}
```

This can then be passed as a command line argument: `--dns-20i-credentials=/etc/twentyi_creds.json`

## Examples

Requesting a certificate for *.example.com and example.com, waiting 5 seconds for the DNS changes to propagate

```shell
certbot certonly \
  --authenticator dns-20i \
  --dns-20i-credentials /etc/letsencrypt/.secrets/twentyi.json \  
  --dns-20i-propagation-seconds 5 \
  --agree-tos \
  -d 'example.com' \
  -d '*.example.com'
```