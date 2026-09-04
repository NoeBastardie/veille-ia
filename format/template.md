# Format du message

Le message final fait **20 lignes maximum**, en français, en mrkdwn Slack.

## Règles de forme

- Gras Slack : une seule astérisque, `*comme ceci*`. Jamais de double astérisque.
- Emojis en code court : `:wave:`, `:warning:`, `:page_facing_up:`, `:point_right:`.
- Pas de titre de type « # ». Le canal fonctionne en messages, pas en articles.
- Pas de tableau, pas de bloc de code sauf si le sujet l'exige vraiment.
- Ton direct et sobre. Bannis : « révolutionnaire », « game changer », « incontournable »,
  « ça change tout ». Une info dont tu n'es pas sûr est une info que tu ne mets pas.

## Structure

```
Salut à tous :wave:

[1 à 2 phrases : ce qui est sorti, et pourquoi ça atterrit dans ce canal. Pas de mise en scène.]

[Pour chaque sujet retenu, 2 ou 3 maximum :]
:emoji: *[Nom du sujet]* — [ce que c'est, en une phrase]
[Pourquoi ça compte pour un PM ou un designer, en une phrase]
• [une chose concrète à tester cette semaine]
• [une deuxième, seulement si elle apporte autre chose]

:warning: À prendre avec des pincettes : [stade de déploiement, disponibilité par plan, coût,
limites de périmètre, ce qui n'est pas encore vérifié. Cette section n'est jamais vide.]

:point_right: [Question ouverte ou proposition concrète pour lancer le thread. Engage-toi
personnellement plutôt que de demander à la cantonade.]

:page_facing_up: [Source primaire 1] : [url]
:page_facing_up: [Source primaire 2] : [url]
```

## Exemple de référence

C'est le calibre à viser, en ton comme en densité.

```
Salut à tous :wave:

Anthropic a sorti les *routines* dans Claude Code : une automatisation qu'on configure une seule fois
(un prompt + un ou plusieurs repos + des connecteurs) et qui se relance ensuite toute seule. Ça tourne
sur l'infra web de Claude Code, donc plus besoin de cron, de serveur ou de laisser sa machine ouverte.

Trois déclencheurs possibles, combinables sur une même routine :
• *Planning* — horaire, nocturne ou hebdo
• *Appel API* — chaque routine a son endpoint et son token, on la branche sur du monitoring ou un
  hook de déploiement
• *Événement GitHub* — une session par PR qui matche les filtres

Les usages qui nous concernent directement côté produit :
• triage du backlog chaque nuit : labels, assignation, et résumé posté dans Slack
• dérive documentaire : scan hebdo des PR mergées, ouverture des PR de mise à jour
• revue de PR sur checklist maison avec commentaires inline avant le passage d'un humain

:warning: À prendre avec des pincettes : encore en research preview, dispo sur Pro / Max / Team /
Enterprise avec Claude Code on the web activé. Ça consomme le quota comme une session interactive,
avec un plafond quotidien (5 en Pro, 15 en Max, 25 en Team/Enterprise).

:point_right: Je pars sur un test de triage de backlog sur une mission et je partage le retour ici.

:page_facing_up: Annonce : https://claude.com/blog/introducing-routines-in-claude-code
:page_facing_up: Doc : https://code.claude.com/docs/en/routines
```
