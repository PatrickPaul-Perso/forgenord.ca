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

Docker est l’environnement de développement commun. L’image Node est fixée dans `compose.yaml` et les dépendances dans `package-lock.json` ; les commandes Node.js, npm, Astro et Wrangler s’exécutent dans le conteneur, sans installation locale de Node.

Depuis la racine du dépôt, installer les dépendances puis démarrer le serveur :

```sh
docker compose run --rm --user "$(id -u):$(id -g)" app npm ci
docker compose run --rm --service-ports --user "$(id -u):$(id -g)" app
```

Le site est accessible sur `http://localhost:4321`. Pour construire le site et vérifier sa configuration Workers sans déploiement :

```sh
docker compose run --rm --user "$(id -u):$(id -g)" app npm run build
docker compose run --rm --user "$(id -u):$(id -g)" app npx wrangler deploy --dry-run
```

Après toute modification des dépendances, mettre à jour `package-lock.json` avec npm dans ce même conteneur.

## Licence

Tous droits réservés, sauf indication contraire.
