# Prompt de la routine

À copier dans le champ **Instructions** sur [claude.ai/code/routines](https://claude.ai/code/routines).
Ce fichier est la copie de référence : si tu modifies le prompt dans la routine, reporte-le ici.

---

```
Tu prépares la veille IA hebdomadaire d'un cabinet de conseil en product management et design.
Le livrable est UN message Slack en français, prêt à poster dans #ressource-veille.

ÉTAPE 1 — Contexte
Lis format/template.md et format/criteres.md dans le repo. Ils font autorité sur le format et sur le
tri : en cas de doute, applique-les plutôt que ton propre jugement.
Lis TOUS les fichiers de archives/, pas seulement les récents : c'est ta seule source de vérité sur ce
qui a déjà été partagé dans le canal. Aucun sujet déjà traité ne revient, sauf évolution majeure, et
dans ce cas dis explicitement ce qui a changé depuis.

ÉTAPE 2 — Recherche
Balaie les 30 derniers jours. Un sujet plus ancien reste éligible s'il n'apparaît dans aucun fichier de
archives/ : ce qui compte, c'est que le sujet soit nouveau POUR LE CANAL, pas qu'il soit nouveau dans
l'absolu. À qualité égale, privilégie le plus récent. Si tu retiens quelque chose qui a plus d'un mois,
ne fais pas semblant que c'est une nouveauté : présente-le comme un sujet qu'on n'avait pas encore
couvert.
Les périmètres à couvrir sont listés dans format/criteres.md.

ÉTAPE 3 — Tri
Applique les critères de format/criteres.md. Retiens 2 à 3 sujets maximum. Si un seul passe le filtre,
n'en publie qu'un. Si rien ne passe, écris-le franchement en une ligne plutôt que de remplir.
Pour chaque sujet retenu, vérifie la source primaire en ouvrant la page : si tu ne peux pas y accéder,
le sujet ne passe pas.

ÉTAPE 4 — Rédaction
Respecte strictement format/template.md, y compris la limite de 20 lignes et l'exemple de référence
qu'il contient.
Pour chaque sujet : ce que c'est en une phrase, pourquoi ça compte pour un PM, et UNE chose concrète à
tester cette semaine. La section « à prendre avec des pincettes » n'est jamais vide.

ÉTAPE 5 — Livraison
1. Crée un BROUILLON Slack dans #ressource-veille avec le message. Ne poste pas directement.
2. Écris le même texte dans archives/AAAA-MM-JJ.md, avec en tête la liste des sujets écartés et la
   raison en une ligne chacun, puis pousse sur une branche claude/veille-AAAA-MM-JJ et ouvre une PR.

SUCCÈS = un brouillon Slack de 20 lignes maximum, 2 à 3 sujets sourcés en primaire, aucun doublon avec
les archives, et le fichier d'archive commité. Si tu ne peux pas atteindre ça, explique précisément ce
qui a bloqué au lieu de livrer un message dégradé.
```

---

## Réglages de la routine

| Champ | Valeur |
| :-- | :-- |
| Nom | Veille IA hebdo — opportunités PM |
| Modèle | Opus |
| Repositories | `veille-ia` |
| Connectors | Slack uniquement — retire tous les autres |
| Trigger | Schedule → Weekly, lundi 08:00 |
| Environnement | accès réseau Custom (liste ci-dessous) ou Full |

Domaines à autoriser si tu choisis Custom : `claude.com`, `www.anthropic.com`, `openai.com`,
`deepmind.google`, `blog.google`, `ai.meta.com`, `mistral.ai`, `www.microsoft.com`, `techcrunch.com`,
`www.theverge.com`, `arxiv.org`, `digital-strategy.ec.europa.eu`, `www.cnil.fr`.

Le trafic du connecteur Slack passe par les serveurs d'Anthropic, il n'a pas besoin d'être allowlisté.
