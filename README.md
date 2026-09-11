# parking-lot

A single static page that answers "there is nothing here yet" for every domain I own
but have not built anything on. Every request — including `/` — returns HTTP **404**
while rendering the page, so search engines and monitoring tools are not fooled.

Domains are pointed at it by adding the hostname as a domain on the Dokploy
application that deploys this repo (git source, Dockerfile build). One container
serves any number of hostnames; the page reads its own host from the browser.

```sh
bun install && bun run build          # static output in build/
docker build -t parking-lot .
docker run --rm -p 8080:80 parking-lot
curl -i localhost:8080/               # 404 + the page
curl -i localhost:8080/healthz        # 200 ok
```

MIT licensed.

## Deployment

Deployed by Dokploy from `main` (Dockerfile build, auto-deploy on push). Health check: `GET /healthz`.
