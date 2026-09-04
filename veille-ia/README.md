# veille-ia

Repo support de la routine Claude Code « Veille IA hebdo — opportunités PM ».

La routine tourne chaque lundi matin, clone ce repo, et s'en sert pour deux choses :

- **`format/`** : le format du message et les critères de sélection. Modifie ces fichiers pour ajuster
  la routine sans rééditer son prompt.
- **`archives/`** : un fichier par semaine. C'est la mémoire de la veille — la routine lit tout le
  dossier pour ne jamais resservir un sujet déjà partagé dans le canal.

## Fonctionnement

1. La routine lit `format/` et `archives/`
2. Elle balaie les 30 derniers jours, en écartant tout ce qui apparaît déjà dans `archives/`
3. Elle crée un brouillon Slack dans `#ressource-veille`
4. Elle écrit le message dans `archives/AAAA-MM-JJ.md` et ouvre une PR

## Boucle de calibrage

Chaque fichier d'archive commence par la liste des sujets **écartés** avec la raison. C'est le levier
principal : si tu vois en « écarté » des choses que tu aurais gardées, corrige `format/criteres.md`.
Si le message est trop long ou trop mou, corrige `format/template.md`.

## Configuration de la routine

Le prompt est versionné dans `routine-prompt.md`. Si tu le modifies ici, reporte-le dans la routine sur
[claude.ai/code/routines](https://claude.ai/code/routines) — le prompt vit dans la routine, pas dans le
repo.

Réglages : modèle Opus, repo `veille-ia`, connecteur Slack uniquement, trigger Weekly lundi 08:00,
environnement avec accès réseau Custom ou Full.
