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

## Déploiement Cloudflare Workers

Le site Astro est généré en fichiers statiques dans `dist/`. La configuration `wrangler.jsonc` définit le Worker `forgenord-ca`, sert ce répertoire et associe le domaine personnalisé `forgenord.ca`. Aucun adaptateur Astro côté serveur n’est nécessaire.

Après la fusion des changements dans `main`, dans le tableau de bord Cloudflare :

1. Ouvrir **Workers & Pages** → **Create application** → **Import a repository**.
2. Choisir le dépôt GitHub `PatrickPaul-Perso/forgenord.ca`, la branche `main` et la racine du dépôt (`/`). Nommer le Worker `forgenord-ca`.
3. Définir **Build command** à `npm run build` et **Deploy command** à `npx wrangler deploy`.
4. Vérifier ces paramètres, puis utiliser **Save and Deploy** pour lancer le premier déploiement depuis Workers Builds. Vérifier ensuite que le domaine `forgenord.ca` est actif dans **Domains & Routes**.

Cette liaison GitHub est une opération du tableau de bord Cloudflare ; les commandes Docker ci-dessus servent aux vérifications locales et ne déploient rien.

## Licence

Tous droits réservés, sauf indication contraire.
