# Instructions pour Codex

## Workflow Git

- Partir d'une branche `main` à jour et créer une branche dédiée par tâche : `feature/<sujet>`, `fix/<sujet>` ou `docs/<sujet>`.
- Ne pas modifier directement `main`. Garder chaque branche centrée sur un seul objectif.
- Découper le travail en changements petits et cohérents. Chaque commit doit représenter une seule intention, rester compréhensible seul et laisser le projet dans un état valide.
- Éviter les refontes, renommages et changements de format sans lien avec la tâche. Si un travail indépendant apparaît, le traiter dans une autre branche.
- Avant chaque commit, examiner le diff, retirer les modifications accidentelles et exécuter les vérifications pertinentes. Signaler les vérifications impossibles à exécuter.
- Rédiger des messages de commit précis, à l'impératif, qui décrivent le changement réalisé.
- Présenter la branche dans une pull request avec un résumé, les vérifications effectuées et les limites connues. Ne pas fusionner dans `main` sans demande explicite.

## Travail dans le projet

- Respecter les conventions et outils déjà présents dans le dépôt.
- Préférer la solution la plus simple qui répond à la demande, sans ajouter de dépendance inutile.
- Mettre à jour la documentation et les tests lorsque le comportement concerné le justifie.
- Ne jamais inclure de secrets ou de fichiers générés dans un commit.
