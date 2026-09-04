# Routine « Veille IA hebdo — opportunités PM »

Objectif : chaque lundi matin, un brouillon de message prêt à poster dans `#ressource-veille`, au format
du canal, sur les nouveautés IA réellement exploitables par un PM ou un designer.

---

## 1. Préparer le repo

Une routine a besoin d'au moins un repo GitHub, cloné à chaque run. Crée un repo privé `veille-ia` :

```
veille-ia/
├── format/
│   ├── template.md      ← le format du message (copie celui qu'on a construit)
│   └── criteres.md      ← les critères de sélection (section 4 ci-dessous)
└── archives/
    └── .gitkeep         ← un fichier par semaine, écrit par la routine
```

Le repo joue deux rôles : il porte le format (donc tu le modifies sans toucher au prompt) et il porte
la mémoire (la routine lit `archives/` pour ne pas resservir un sujet déjà traité).

Pense à installer la Claude GitHub App sur le repo, ou à accorder l'accès GitHub à ton compte.

## 2. Créer la routine

Sur `claude.ai/code/routines` → **New routine**. Ou en CLI : `/schedule veille IA hebdo le lundi à 8h`,
Claude pose les mêmes questions conversationnellement.

| Champ | Valeur |
| :-- | :-- |
| Nom | Veille IA hebdo — opportunités PM |
| Prompt | voir section 4 |
| Modèle | Opus (le tri éditorial est le vrai travail ici) |
| Repositories | `veille-ia` |
| Environnement | un env dédié, réseau **Custom** ou **Full** (voir section 3) |
| Connectors | **Slack uniquement** |
| Trigger | Schedule → Weekly, lundi 08:00 |

Deux points d'attention sur les connecteurs : tous tes connecteurs sont inclus par défaut, et pendant un
run Claude peut appeler n'importe quel outil d'un connecteur inclus, écritures comprises, sans demander
d'autorisation. Retire donc tout sauf Slack. Et les actions passent par tes comptes liés : le brouillon
Slack apparaîtra comme venant de toi.

## 3. Réseau

L'environnement Default est en **Trusted** : seule l'allowlist par défaut passe, le reste échoue en 403
avec `x-deny-reason: host_not_allowed`. Pour de la recherche web, duplique l'environnement et passe
**Network access** sur :

- **Custom** + liste de domaines si tu veux cadrer les sources (recommandé, ça force la qualité) :
  `claude.com`, `www.anthropic.com`, `openai.com`, `deepmind.google`, `blog.google`, `ai.meta.com`,
  `mistral.ai`, `www.microsoft.com`, `techcrunch.com`, `www.theverge.com`, `arxiv.org`,
  `digital-strategy.ec.europa.eu`, `www.cnil.fr`
- **Full** si tu préfères ne pas maintenir la liste

Le trafic des connecteurs passe par les serveurs d'Anthropic, donc Slack fonctionne sans rien ajouter à
l'allowlist.

## 4. Le prompt à copier

```
Tu prépares la veille IA hebdomadaire d'un cabinet de conseil en product management et design.
Le livrable est UN message Slack en français, prêt à poster dans #ressource-veille.

ÉTAPE 1 — Contexte
Lis format/template.md et format/criteres.md dans le repo.
Lis TOUS les fichiers de archives/, pas seulement les récents : c'est ta seule source de vérité sur ce
qui a déjà été partagé dans le canal. Aucun sujet déjà traité ne revient, sauf évolution majeure, et
dans ce cas dis explicitement ce qui a changé depuis.

ÉTAPE 2 — Recherche
Balaie les 30 derniers jours. Un sujet plus ancien que 30 jours reste éligible s'il n'apparaît dans
aucun fichier de archives/ : ce qui compte, c'est que le sujet soit nouveau POUR LE CANAL, pas qu'il
soit nouveau dans l'absolu. À qualité égale, privilégie le plus récent. Si tu retiens quelque chose
qui a plus d'un mois, ne fais pas semblant que c'est une nouveauté : présente-le comme un sujet qu'on
n'avait pas encore couvert.

Sujets à couvrir :
- nouvelles capacités agentiques dans les outils grand public et pro (automatisation, connecteurs,
  usage d'ordinateur)
- outillage de discovery, de recherche utilisateur, de prototypage et de design
- sorties de modèles, uniquement sous l'angle « qu'est-ce que ça change dans la pratique »
- réglementation et conformité européenne (AI Act, CNIL) quand ça impacte un cadrage produit
- retours d'expérience chiffrés en entreprise

ÉTAPE 3 — Tri (le plus important)
Retiens 2 à 3 sujets maximum. Un sujet ne passe que s'il coche TOUT :
- un PM ou un designer peut le tester lui-même dans les 2 semaines, sans dépendre d'une équipe de dev
- il existe une source primaire : blog éditeur, doc officielle, texte de régulateur. Jamais un
  agrégateur, jamais un thread LinkedIn, jamais un article qui commente un article
- ça change une façon de travailler, pas seulement un benchmark

Écarte : les levées de fonds, les guerres de benchmarks, les annonces d'infrastructure, les rumeurs,
les partenariats commerciaux sans effet sur la pratique.
Si un seul sujet passe le filtre, n'en publie qu'un. S'il n'y a rien, écris-le franchement en une
ligne plutôt que de remplir.

ÉTAPE 4 — Rédaction
Respecte strictement format/template.md. Contraintes :
- 20 lignes maximum, gras Slack avec une seule astérisque, emojis en code court (:wave:)
- pour chaque sujet : ce que c'est en une phrase, pourquoi ça compte pour un PM, et UNE chose concrète
  à tester cette semaine
- une section « :warning: À prendre avec des pincettes » avec les vraies limites : stade de
  déploiement, disponibilité par plan, coût, ce qui n'est pas encore vérifié
- les liens en fin de message, préfixés de :page_facing_up:, uniquement des sources primaires
- une question ouverte en clôture pour lancer le thread
- ton direct et sobre, pas de superlatifs, pas de « révolutionnaire », pas de « game changer ».
  Une info dont tu n'es pas sûr est une info que tu ne mets pas.

ÉTAPE 5 — Livraison
1. Crée un BROUILLON Slack dans #ressource-veille avec le message. Ne poste pas directement.
2. Écris le même texte dans archives/AAAA-MM-JJ.md, avec en tête la liste des sujets écartés et la
   raison en une ligne chacun, puis pousse sur une branche claude/veille-AAAA-MM-JJ et ouvre une PR.

SUCCÈS = un brouillon Slack de 20 lignes maximum, 2 à 3 sujets sourcés en primaire, aucun doublon
avec les archives, et le fichier d'archive commité. Si tu ne peux pas atteindre ça, explique
précisément ce qui a bloqué au lieu de livrer un message dégradé.
```

## 5. Tester et surveiller

Clique **Run now** sans attendre lundi. Puis ouvre le run et lis la transcription : un statut vert
signifie seulement que la session a démarré et s'est terminée sans erreur d'infra, pas que la tâche a
réussi. Les requêtes réseau bloquées, les outils de connecteur manquants et les échecs de tâche
apparaissent dans la transcription, pas dans l'indicateur.

Ce qu'il faut vérifier sur les premiers runs :
- les sources sont-elles primaires, ou la routine s'est-elle rabattue sur des agrégateurs
- le filtre « testable par un PM en 2 semaines » tient-il, ou tout finit-il par passer
- la longueur : si ça dépasse, resserre à 2 sujets dans le prompt
- avec la fenêtre à 30 jours, la routine ne se contente-t-elle pas de ressortir du vieux : si les
  sujets sont systématiquement anciens, c'est le signe que la recherche est trop peu profonde

Garde le brouillon pendant un mois ou deux. Quand la qualité est stable, remplace l'étape 5.1 par un
post direct — mais tant que tu relis, tu gardes la main sur ce qui sort sous ton nom.

Les premières semaines, le repo est vide donc le filtre anti-doublon ne joue pas et tu risques un
message un peu large. C'est normal, ça se resserre au fur et à mesure que archives/ se remplit. Tu peux
accélérer en committant à la main les 3 ou 4 derniers messages du canal comme archives de départ.

Les runs planifiés peuvent démarrer quelques minutes après l'heure prévue, le décalage est constant
pour une routine donnée. Un run hebdo consomme ton quota comme une session interactive et compte dans
le plafond quotidien de ton plan, donc aucun risque de saturation à cette cadence.

## Sources

- Annonce : https://claude.com/blog/introducing-routines-in-claude-code
- Documentation : https://code.claude.com/docs/en/routines
