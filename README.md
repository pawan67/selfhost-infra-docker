# Selfhost Infra with Docker

This repository contains my personal **Docker Compose setup** for self-hosting applications on a VPS.
It uses **Traefik** as a reverse proxy and **Authelia** for authentication.

The stack is modular — you can add or remove services as you like.

---

## Prerequisites

- A VPS with Docker and Docker Compose installed
- Ports **80** and **443** open
- A domain or subdomains pointing to your VPS IP

  - Free domains from [DuckDNS](https://www.duckdns.org/) or [Afraid.org](https://afraid.org/) also work

- (Optional but recommended) Cloudflare for DNS — lets you use the included Cloudflare DDNS to automatically manage records

---

## Setup

1. Install Docker

   ```bash
   curl -fsSL https://get.docker.com | sh
   ```

2. Clone this repository

   ```bash
   cd /opt
   git clone https://github.com/pawan67/selfhost-infra-docker.git
   cd selfhost-infra-docker
   ```

3. Configure environment variables

   - Copy `.env.example` files into `.env` for each app you want to run
   - Edit values with your domain, secrets, tokens, etc.
   - Example using nano:

     ```bash
     nano apps/audiobookshelf/.env
     ```

4. Start the core services (**Traefik** + **Authelia**)

   ```bash
   docker compose --profile required up -d
   ```

5. Enable more services

   - Add them to the `COMPOSE_PROFILES` variable in the root `.env`
   - Or run them on demand with:

     ```bash
     docker compose --profile grafana --profile audiobookshelf up -d
     ```

6. Check your setup

   - Make sure you’re in the repo root (`pwd` should show `/opt/docker`)
   - Run all enabled profiles:

     ```bash
     docker compose up -d
     ```

---

## Notes

- If you’re not using Cloudflare DDNS, create the DNS A records for each service manually
- Some services need extra steps (like adding API keys or editing configs) — check their `README.md` inside `apps/{service}`
- Ports **80** and **443** must stay open
