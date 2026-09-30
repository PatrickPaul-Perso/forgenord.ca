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

Astro génère un site statique dans `dist/`. Le fichier `wrangler.jsonc` configure le Worker `forgenord-ca`, sert ces fichiers et associe `forgenord.ca` comme domaine personnalisé. Il ne faut ni script Worker ni adaptateur Astro côté serveur pour ce site statique.

Le déploiement de production passe par [Workers Builds](https://developers.cloudflare.com/workers/ci-cd/builds/), déclenché depuis GitHub. Après la fusion de cette configuration dans `main` :

1. Dans le compte Cloudflare qui contient la zone active `forgenord.ca`, ouvrir **Workers & Pages** → **Create application** → **Import a repository**.
2. Autoriser l’accès GitHub si nécessaire, puis sélectionner `PatrickPaul-Perso/forgenord.ca` et créer le Worker avec les paramètres suivants :

   | Paramètre | Valeur |
   | --- | --- |
   | Worker name | `forgenord-ca` |
   | Production branch | `main` |
   | Root directory | `/` |
   | Build command | `npm run build` |
   | Deploy command | `npx wrangler deploy` |

3. Vérifier les paramètres, puis choisir **Save and Deploy**. Cette action lance le premier build et déploiement sur Cloudflare ; les prochains commits sur `main` déclencheront les suivants.
4. Vérifier que le build réussit, que **Domains & Routes** affiche `forgenord.ca` comme domaine personnalisé du Worker et que `https://forgenord.ca` répond. La déclaration `routes` dans `wrangler.jsonc` permet à Wrangler de créer l’association du [domaine personnalisé](https://developers.cloudflare.com/workers/configuration/routing/custom-domains/) lors du déploiement.

Le nom du Worker dans Cloudflare doit correspondre exactement au champ `name` de `wrangler.jsonc`. Les commandes Docker de la section Développement servent aux vérifications locales ; `--dry-run` ne publie rien.

## Licence

Tous droits réservés, sauf indication contraire.
