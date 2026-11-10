# newry deployment

This fork tracks `cmliu/edgetunnel` and provides the edgetunnel 2.1 management panel.

- Worker: `newry`
- Production URL: `https://newry.jkcgroup.com.au`
- Management panel: `https://newry.jkcgroup.com.au/admin`
- Entry point: `_worker.js`
- KV binding: `KV`, using the existing newry namespace

## Cloudflare Workers Builds

Connect `righttang/edgetunnel` with these settings:

- Production branch: `main`
- Root directory: `.`
- Build command: `npm run build`
- Deploy command: `npm run deploy`
- Preview branch builds: disabled (this deployment uses production KV)

Pushes to `main` build and deploy this Worker. Runtime secrets are stored in Cloudflare and preserved on later deployments. Never commit `ADMIN`, `UUID`, or local `.dev.vars` files.

## Local deployment

```sh
npm install
npm run build
npm run deploy
```

For a fresh Worker, supply `ADMIN` and `UUID` together using `wrangler deploy --secrets-file .dev.vars`. The ignored `.dev.vars` file holds local credentials and must be kept private.

## Upstream updates

Merge `cmliu/edgetunnel:main` into this fork's `main`, retaining `wrangler.toml` for the newry domain and KV binding. Push the reviewed update to trigger deployment.
