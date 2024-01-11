I have a domain and it is hosted on Cloudflare. I use pc3.xxxx.com as the IP for this machine and have configured the router for port forwarding. In additional, I have edit the crontab file will execute the .sh file every ten minutes.

```
*/10 * * * * /home/xxxx/cloudflare.sh 2>&1 | while read line; do echo "$(date) $line"; done >> /home/xxx/cloudflare.update.log
```
