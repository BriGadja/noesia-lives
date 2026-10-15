# Pose ton premier hook

**École Noésia · live du jeudi 15 octobre 2026 · Brice Gachadoat**

Une consigne dans ton CLAUDE.md, Claude la suit s'il y pense. Un hook, Claude Code le fait à
chaque fois. C'est un capteur : quand quelque chose se passe, une action part.

Tu n'as pas à l'écrire. Tu le décris à Claude en français, il l'écrit, et tu le provoques une fois
pour le voir partir.

**Avant de commencer**

- Un projet bac à sable, jamais un vrai dossier client.
- Claude Code peut te demander l'autorisation de modifier ses réglages : c'est normal, ce dossier
  est protégé. Regarde ce qu'il propose, puis accepte.

## 1. Te prévenir : la sonnette

Colle cette phrase dans Claude Code :

```text
À chaque fois que tu as fini de me répondre, joue un son de mon ordinateur pour me prévenir. Choisis un son qui existe déjà sur ma machine, joue-le une fois pour que je l'entende, et montre-moi ce que tu as ajouté.
```

Puis provoque-la : pose une question simple, par exemple « Combien de fichiers y a-t-il dans ce
dossier ? ». Il répond, et ça sonne.

Si ça coince :

```text
Le son est coupé avant la fin : utilise une commande qui attend la fin du son.
```

```text
Je n'ai rien entendu à la fin de ta réponse. Cherche pourquoi et corrige le hook.
```

Pour la changer, ou savoir ce qui est en place :

```text
Sonne aussi quand tu attends mon autorisation.
```

```text
Quels hooks sont en place ? Explique-moi ce que fait chacun.
```

## 2. Vérifier que c'est fini : le juge de fin

Claude s'arrête quand il pense avoir fini, pas quand toi, tu considères que c'est fini. Écris ta
règle de « fini » à la place des crochets :

```text
Avant de t'arrêter, fais vérifier par un juge que [ta règle de « fini »]. Sinon, continue.
```

L'exemple du live : « que la date du jour est notée dans suivi.csv pour chaque client relancé ».

**Tape `/clear` avant de le tester.** Sinon Claude connaît déjà ta règle et la respecte de
lui-même : le juge n'a rien à juger. `/clear` efface la conversation, le hook reste en place.

Bon à savoir : le juge appelle un modèle chaque fois que Claude veut s'arrêter, c'est un coût. Et il
ne tourne pas en boucle : il relance Claude huit fois de suite au plus.

Si c'est trop lent :

```text
Remplace ce juge par un juge de type prompt, qui lit seulement ton dernier message.
```

## 3. Protéger : rien ne part sans toi

Si ton Claude Code est relié à Gmail par le connecteur :

```text
Mets en place un hook : bloque tout envoi de mail, aucun mail ne part sans ma relecture. Fais un brouillon à la place.
```

Tape `/clear`, puis provoque-le avec une adresse qui n'existe pas :

```text
Envoie un mail de test à contact@exemple.example avec Gmail.
```

L'envoi est bloqué avant de partir, et Claude passe au brouillon. Supprime ce brouillon ensuite.

Si le script plante :

```text
Fais ce blocage en une seule ligne, sans script.
```

**Même chose pour ton fichier de clés API.** Une consigne dans CLAUDE.md ne le protège pas. Une
règle de permission, si :

```text
Ajoute dans mes réglages d'ordinateur une règle de permission qui t'interdit de lire tout fichier .env, où qu'il soit : Read(//**/.env) dans permissions.deny. Montre-moi ce que tu as ajouté.
```

Le seul piège : un hook mal écrit ne bloque rien, il laisse tout passer. Le réflexe : demande à
Claude de le tester, puis provoque-le une fois.

## 4. Garder une trace : le journal

```text
Après chaque action, ajoute une ligne avec la date, l'heure et l'action dans journal-claude.log, à la racine du projet. Teste-le une fois.
```

Si le journal reste vide :

```text
Le journal reste vide après mes questions. Cherche pourquoi et corrige le hook.
```

## Bonus : jusqu'à ton téléphone

Un hook peut appeler ton n8n : Claude finit, ton téléphone vibre. Il te faut un workflow n8n qui
reçoit un webhook et t'envoie un message (Telegram, Slack...), protégé par un en-tête. La valeur de
cet en-tête va dans une variable d'environnement de ton ordinateur, jamais dans le prompt.

```text
À chaque fois que tu as fini de me répondre, envoie aussi ton dernier message à mon n8n, avec un hook de type http : POST sur [l'URL de ton webhook n8n], avec l'en-tête [le nom de ton en-tête] qui prend la valeur de ma variable d'environnement [LE_NOM_DE_TA_VARIABLE]. N'affiche jamais la valeur de cette variable.
```

## La carte complète

Un hook répond toujours à trois questions. Tu n'as pas à retenir la liste : demande à Claude
« Quels moments existent pour un hook, et lequel choisirais-tu pour... ? ».

| Quand ? (8 des 33 moments) | Il lance quoi ? (5 types) | Il décide quoi ? |
|---|---|---|
| Ta session s'ouvre · `SessionStart` | Une commande · `command` | Laisser passer |
| Tu lui écris · `UserPromptSubmit` | Un appel web · `http` | Bloquer et expliquer |
| Avant une action · `PreToolUse` | Un connecteur · `mcp_tool` | Te demander ton accord |
| Il demande l'accord · `PermissionRequest` | Un avis de Claude · `prompt` | Accepter à ta place |
| Après une action · `PostToolUse` | Un agent qui vérifie · `agent` | Renvoyer au travail |
| Il a besoin de toi · `Notification` | | Informer Claude |
| Il a fini · `Stop` | | Corriger l'action |
| Ta session se ferme · `SessionEnd` | | |

Deux ou trois hooks suffisent : un hook pour un problème qui revient, pas pour un problème qui
arrive une fois sur vingt.

## Passage à l'action

Sur un projet bac à sable, fais écrire par Claude deux hooks :

1. la sonnette de fin ;
2. un juge de fin avec **ta** règle de « fini ».

Rapporte deux captures, avec la phrase que tu as utilisée pour chacun : ce que Claude a ajouté pour
la sonnette, et Claude renvoyé au travail par le juge.

**Permanence Technique : vendredi 16 octobre, de 12h30 à 13h30.**

## La documentation officielle

- Le guide des hooks : https://code.claude.com/docs/en/hooks-guide
- La référence des hooks : https://code.claude.com/docs/en/hooks
- Les permissions : https://code.claude.com/docs/en/permissions
