# Cloudflare Tunnel x Docker Compose

This repository is a non-production (seriously don't use it in production) example of how to route traffic through a
Cloudflare tunnel. It contains a docker compose specification for running:
- A single [Cloudflare tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/)
- A [Traefik Proxy](https://traefik.io/traefik/) instance to which the tunnel is routing
exposed traefik with 3
- Three instances of a dummy service ([whoami](https://hub.docker.com/r/traefik/whoami)) which are proxied & load-balanced by Traefik.

## Quickstart

- Create a tunnel in your Cloudflare account through https://one.dash.cloudflare.com/<your-account>/networks/tunnels.
- In the creation process, select `cloudflared` (the utility we're using in Docker to create and operate the tunnel).
- Select Docker in the installation process, you should have a token available from the command that's given for running `cloudflared` in Docker.
- If you're prompted to provide a URL your tunnel should route to, it should be `http://proxy:80`.
- Copy/Paste the `.env.example` file to `.env` and put your token there on the appropriate env variable.
- In your Docker compose specification, replace `foo.bar` by the hostname you're running your tunnel under.
- `docker compose up` & :tada:. You should be set !

## What do I have access to

- On the domain routed to your tunnel, you should have access to Traefik routing to your three `whoami` instances.
  Let's say I'm routing my tunnel from `tunnel.crossbone.cc`, you can reach `tunnel.crossbone.cc/whoami`.
- On your local machine, you can access Traefik's dashboard on http://127.0.0.1:8080/dashboard/.

## Issues

If you have an issue you can just create an issue, I'll do my best to reply to it.
