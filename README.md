# yasinozmeen.me

Personal landing page — [yasinozmeen.me](https://yasinozmeen.me)

## Stack

- Static HTML/CSS/JS — no framework, no build step
- Fonts: [Newsreader](https://fonts.google.com/specimen/Newsreader) + [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono)
- Served via nginx:alpine on Raspberry Pi 5, exposed through Cloudflare Tunnel

## Deploy

Build ARM64 image and push to Pi:

```bash
docker buildx build --platform linux/arm64 -t yasinozmeen-me:latest --load .
docker save yasinozmeen-me:latest | gzip -1 | ssh pi 'gunzip | sudo docker load'
ssh pi 'sudo docker rm -f yasinozmeen-me && sudo docker run -d --name yasinozmeen-me --restart always -p 127.0.0.1:3001:80 yasinozmeen-me:latest'
```
