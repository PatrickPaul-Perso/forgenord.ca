# Forge Nord

Site principal de Forge Nord, une plateforme canadienne de projets numériques, IoT, prototypes, outils et créations locales.

Le site est développé avec Astro et sera déployé sur Cloudflare Workers.

## Projets

- `forgenord.ca` — site principal
- `nfc.forgenord.ca` — expériences et jeux NFC
- `labs.forgenord.ca` — prototypes, IoT et expérimentations
- `portfolio.forgenord.ca` — portfolio professionnel
- `giocoso.forgenord.ca` — projets de Giocoso Creation

## Développement

Le projet utilise Astro pour générer un site statique, servi sur Cloudflare Workers. Il faut Node.js 22.12 ou plus et npm, ou Docker pour exécuter les commandes sans installer Node sur la machine.

```sh
npm ci
npm run dev
npm run build
```

Avec Docker, depuis la racine du dépôt :

```sh
docker run --rm --user "$(id -u):$(id -g)" -e npm_config_cache=/tmp/npm-cache -v "$PWD:/app" -w /app node:24-bookworm-slim npm ci
docker run --rm --user "$(id -u):$(id -g)" -e npm_config_cache=/tmp/npm-cache -v "$PWD:/app" -w /app -p 4321:4321 node:24-bookworm-slim npm run dev -- --host 0.0.0.0
```

Le serveur local est accessible sur `http://localhost:4321`. Pour vérifier le paquet Workers sans le publier, exécuter `npm run build`, puis `npx wrangler deploy --dry-run` (directement ou dans le conteneur). Le déploiement réel utilise `npm run deploy` après configuration de l’accès Cloudflare.

## Licence

Tous droits réservés, sauf indication contraire.
