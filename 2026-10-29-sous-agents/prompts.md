# Le cadeau : délègue à des sous-agents

**École Noésia · live du jeudi 29 octobre 2026 · Brice Gachadoat**

Tu n'écris rien à la main. Tu copies une phrase, tu la colles dans Claude Code, et tu remplaces
ce qui est entre crochets. Claude fait le reste.

## 1. Cinq réflexes, aucun fichier à écrire

**Regarde ce qui remplit ta conversation.** Tape `/context`. La ligne des messages grossit à
chaque fichier lu et à chaque recherche, et tout ce qui y reste repart avec chacun de tes
messages suivants.

**Confie une lecture lourde.** Quand il faut lire beaucoup pour n'en garder qu'une conclusion :

```text
Confie la lecture de [ce dossier] à trois sous-agents au plus, chacun sur un lot
de fichiers. Chacun me rend cinq lignes, avec le fichier d'où vient chaque fait.
Ne lis aucun fichier toi-même.
```

**Une question sur ce qui a déjà été dit** : `/btw [ta question]`. Il voit toute la
conversation, n'utilise aucun outil, et sa réponse ne reste pas dans l'historique. Inutile de
lancer un agent pour ça.

**Une tâche à côté, sans rien réexpliquer** : `/subtask [la tâche]`. Ce sous-agent emporte
toute la conversation, travaille pendant que tu continues, et te rend le résultat. Si la
commande n'existe pas chez toi, essaie `/fork`.

**Au retour, demande la trace, pas le résumé** :

```text
Montre-moi la preuve : pour chaque fait, le fichier et la phrase exacte, ou
l'adresse de la page. Je vais vérifier.
```

## 2. Qu'il délègue sans que tu aies à le demander

Cette phrase ajoute à ton `CLAUDE.md` personnel une courte section que Claude lit au début de
chaque conversation :

```text
Ajoute à mon CLAUDE.md personnel, celui qui vaut pour tous mes projets, une
courte section sur les sous-agents. Avant de l'écrire, pose-moi trois questions
sur les tâches que je te confie le plus souvent. La section tient en dix lignes
au plus et te dit :
- de confier à un sous-agent ce qui demande de lire beaucoup pour n'en garder
  qu'une conclusion : plusieurs documents, de longs fichiers, une recherche sur
  le web, une relecture ;
- de garder dans notre conversation ce qui demande des allers-retours avec moi,
  une petite modification, une décision ;
- de demander à chaque sous-agent un rendu court, avec le fichier ou l'adresse
  d'où vient chaque fait ;
- de lancer plusieurs sous-agents en même temps quand les morceaux sont
  indépendants, mais de regrouper : trois ou quatre au plus, chacun sur un lot,
  plutôt qu'un par document.
Montre-moi la section avant de l'enregistrer.
```

Testée avant le live sur le dossier de Léa : sans cette section, Claude a lu les dix fichiers
lui-même ; avec, il a confié la lecture à trois sous-agents, sans qu'on le lui demande. C'est
une consigne : Claude la suit le plus souvent, pas à chaque fois. La ligne « regroupe » compte.
Sans elle, il a lancé un sous-agent par fichier, ce qui coûtait plus cher et allait deux fois
moins vite.

## 3. Chercher en éventail

**La recherche toute prête** : `/deep-research [ta question]`. Elle lance des recherches web
sous plusieurs angles, croise les sources, vote sur chaque affirmation et te rend un rapport
cité, sans ce qui n'a pas tenu. Elle tourne en arrière-plan ; `/workflows` montre où elle en
est. **Sur l'abonnement Pro, active-la d'abord** : `/config`, ligne « Dynamic workflows ».

**Ta propre recherche en éventail.** Un sous-agent de recherche a besoin de quatre choses : un
objectif, un format de rendu, où chercher, et où s'arrêter.

```text
Lance [nombre] sous-agents de recherche en parallèle, un par [angle : un outil,
un concurrent, une question]. Donne à chacun l'objectif, le format de rendu
(cinq lignes, avec l'adresse et la phrase exacte qui prouve chaque fait), où
chercher (les sites officiels d'abord), et où s'arrêter (dix pages au plus).
Puis fais la synthèse, et dis-moi ce qu'aucun n'a trouvé.
```

Combien en lancer : un seul pour vérifier un fait, deux à quatre pour une comparaison, dix et
plus pour une vraie enquête. Plusieurs agents consomment environ quinze fois plus de tokens
qu'une conversation : garde l'éventail pour ce qui vaut le coup.

**Un cran plus loin : l'équipe d'agents.** Des sous-agents te rendent chacun leur résumé. Dans
une équipe, les agents se parlent, se partagent les tâches et se contredisent. C'est plus solide
pour une grosse recherche ou un gros travail, et beaucoup plus gourmand en tokens : réserve-la à
l'abonnement Max. La fonction est expérimentale et coupée par défaut. Allume-la pour une seule
fenêtre, en tapant dans le terminal à la place de `claude` :

```text
Windows (PowerShell) :  $env:CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS = "1"; claude
Mac :                   CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1 claude
```

Pourquoi une seule fenêtre : tant que le réglage est allumé, Claude peut transformer en
coéquipiers les sous-agents qu'il lance d'habitude, et ta consommation suit. Puis :

```text
Crée une équipe de trois agents sur [ta question]. Le premier cherche
[un angle], le deuxième [un autre angle], le troisième joue l'avocat du diable
et conteste ce que trouvent les deux autres. Prends Sonnet pour chacun. À la
fin, fais la synthèse, dis-moi sur quoi ils n'étaient pas d'accord, puis
arrête l'équipe.
```

Les agents s'affichent sous la zone de saisie : les flèches pour en choisir un, Entrée pour voir
ce qu'il fait. S'il lance des sous-agents à la place, redemande-lui explicitement « une équipe
d'agents ».

## 4. Ton agent à toi

```text
Crée-moi un sous-agent pour [la tâche qui me fait perdre le plus de temps
chaque semaine]. Range-le dans mes sous-agents personnels, pour tous mes
projets. Sa description dit quand l'utiliser. Donne-lui seulement les outils
dont il a besoin, et le modèle le moins cher qui suffit. Montre-moi le fichier
avant de l'enregistrer.
```

- **Claude ne le trouve pas ?** Si le dossier des sous-agents n'existait pas avant, relance
  Claude Code : une session ouverte ne voit pas un dossier créé après son lancement.
- **Il ne part jamais ?** C'est sa description qu'il faut changer : c'est elle que Claude lit
  pour décider. Notre chercheur ne partait pas, Claude répondait de mémoire. Il a suffi
  d'ajouter « même si tu crois connaître la réponse ».

**Les deux agents de l'école**, commentés en français, dans [agents/](agents/) :

- [`relecteur`](agents/relecteur.md) relit un document avant qu'il parte chez un client. Il lit,
  il ne modifie rien, il tourne sur Sonnet.
- [`chercheur`](agents/chercheur.md) cherche sur le web et ne rapporte que la conclusion, avec
  ses sources. Il ne touche pas à tes fichiers, il tourne sur Haiku, le modèle le moins cher.

Pour en installer un (remplace `relecteur` par `chercheur` pour l'autre) :

```text
Installe le sous-agent « relecteur » de l'école Noésia dans mes sous-agents
personnels. Télécharge le fichier avec curl (ou Invoke-WebRequest sous
Windows), sans le réécrire :
https://raw.githubusercontent.com/Noesia-school/noesia-lives/main/2026-10-29-sous-agents/agents/relecteur.md
Puis dis-moi si je dois relancer Claude Code.
```

## 5. Rejouer la démo du dossier de Léa

Léa est consultante. Ses dix rendez-vous découverte sont dans [bac-a-sable/](bac-a-sable/),
avec un devis à relire. Tout est inventé.

```text
Crée un dossier bac-a-sable-sous-agents dans mes Documents et télécharge-y,
avec curl (ou Invoke-WebRequest sous Windows), sans rien modifier, le devis et
les dix fichiers du dossier rendez-vous listés ici :
https://api.github.com/repos/Noesia-school/noesia-lives/contents/2026-10-29-sous-agents/bac-a-sable
https://api.github.com/repos/Noesia-school/noesia-lives/contents/2026-10-29-sous-agents/bac-a-sable/rendez-vous
Puis dis-moi comment relancer Claude Code depuis ce dossier.
```

Puis, depuis ce dossier, `/context`, cette question, et `/context` encore :

```text
Fais-moi le point sur mes dix rendez-vous du dossier rendez-vous/ : pour
chacun, l'entreprise, ce dont le prospect a besoin, ce qui le freine, et la
prochaine étape convenue. Une ligne par rendez-vous.
```

`/clear`, puis la même question suivie de : « Confie la lecture à trois sous-agents, chacun sur
un lot de fichiers, qui te rendent une ligne par rendez-vous. » Compare les deux chiffres.

Ce qu'on a mesuré le 29/10, en Sonnet : Claude seul, +70 000 tokens dans la conversation ;
un sous-agent par fichier, +20 000 et presque deux fois le prix ; trois sous-agents par lots,
+8 000, pour le même prix que seul. La réponse était la même dans les trois cas.

Avec le relecteur installé : « Relis le devis devis-fournil-saint-marc.md avant que je
l'envoie. » Il y a au moins trois erreurs. Ton agent les trouve-t-il toutes ?

## 6. La fiche

**Quand déléguer, et quand surtout pas**

| Un sous-agent | Ta conversation | `/btw` |
|---|---|---|
| Beaucoup à lire pour une conclusion | Des allers-retours avec toi | Une question sur ce qui est déjà dit |
| Un travail qui se résume | Une petite modification | |
| Des outils à limiter (un relecteur qui ne modifie rien) | Quand la vitesse compte : il repart de zéro | |

**Les quatre réglages d'un agent**

- **Le nom** : pour l'appeler toi-même (« demande au relecteur… »).
- **La description** : quand l'utiliser. C'est elle qui décide si Claude délègue.
- **Les outils** : ce qu'il a le droit de faire. Le minimum.
- **Le modèle** : sans réglage, celui de ta conversation. Haiku pour le simple, Sonnet pour
  relire.

**Ce que ça coûte.** Un sous-agent dépense ses propres tokens, sur le même quota que toi. Sur
une seule lecture, ça peut coûter le même prix, parce que ta conversation ne traîne plus tout
ce qu'il a lu. En éventail, ça monte vite. Ce que tu y gagnes : du parallèle et un regard
neuf, pas une réponse plus intelligente.

**La question à te poser au retour de chaque agent** : qu'est-ce que j'ouvre pour le croire ?
Le fichier, la ligne, la page. Son compte rendu n'est pas une preuve.

## Pour aller plus loin

- La documentation officielle des sous-agents : https://code.claude.com/docs/en/sub-agents
- Ce que coûte un sous-agent, et quand il vaut le coup : https://code.claude.com/docs/en/best-practices
- `/deep-research` et les workflows : https://code.claude.com/docs/en/workflows
- Les équipes d'agents : https://code.claude.com/docs/en/agent-teams
- Comment Anthropic a construit sa recherche à plusieurs agents (en anglais) :
  https://www.anthropic.com/engineering/multi-agent-research-system
