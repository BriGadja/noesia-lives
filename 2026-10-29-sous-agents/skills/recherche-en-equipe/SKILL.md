---
name: recherche-en-equipe
# Ce que fait le skill. Il ne part que si tu tapes /recherche-en-equipe (ligne plus bas) :
# une équipe d'agents consomme beaucoup, réserve-la à l'abonnement Max.
description: Lance une équipe d'agents qui enquête sur une question sous plusieurs angles, se contredit, puis rend une synthèse sourcée dans un fichier. À lancer soi-même avec /recherche-en-equipe suivi de la question.
# Ce que Claude Code t'affiche quand tu tapes la commande.
argument-hint: "[ta question]"
# Claude ne le lance jamais de lui-même : c'est toi qui décides de dépenser.
disable-model-invocation: true
---

La question : $ARGUMENTS

## 1. Avant de lancer

- Si la question est vide, demande-la et arrête-toi là.
- Cette recherche demande la fonction « équipes d'agents ». Vérifie dans le terminal que la
  variable d'environnement `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` vaut `1`. Si elle est absente
  ou vaut autre chose, ne remplace pas l'équipe par des sous-agents. Arrête-toi et dis à
  l'utilisateur de quitter Claude Code, puis de le relancer avec la fonction allumée pour cette
  fenêtre :
  - Windows (PowerShell) : `$env:CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS = "1"; claude`
  - Mac ou Linux : `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1 claude`

## 2. L'équipe

Il n'existe pas d'outil séparé pour créer une équipe. Quand la fonction est allumée, chaque
appel à l'outil Agent qui donne un nom à l'agent (le paramètre `name`) lance un coéquipier, sauf
s'il s'agit d'un fork ou s'il passe `isolation`. Lance donc trois coéquipiers, chacun avec
l'outil Agent, un nom, et le modèle Sonnet. Choisis deux angles de recherche qui ne se
recouvrent pas et qui conviennent à la question (par exemple : les offres et les prix sur les
sites officiels ; ce qu'en disent les utilisateurs). Nomme chaque chercheur d'un mot qui dit son
angle, et le troisième « contradicteur ».

Donne à chaque chercheur, dans sa consigne de départ :

- son objectif : son angle, et ce qu'il laisse à l'autre chercheur ;
- son format de rendu : dix lignes au plus, chaque fait suivi de l'adresse complète de la page
  et de la phrase exacte qui le prouve, entre guillemets ;
- où chercher : les sites officiels d'abord, puis les comparatifs et les avis ;
- où s'arrêter : dix pages lues au plus ;
- d'envoyer chaque trouvaille importante au contradicteur, et de répondre à ses objections par
  une source, ou de retirer le fait.

Donne au contradicteur : lire les trouvailles des chercheurs dès qu'elles arrivent, chercher ce
qui les contredit (une page plus récente, un autre chiffre, une source peu fiable), écrire
directement au chercheur concerné pour contester, et noter ce qui a tenu et ce qui est tombé.

## 3. Pendant qu'ils travaillent

Ne fais pas la recherche toi-même. Réponds aux messages de l'équipe, laisse les chercheurs et le
contradicteur se répondre, et attends que les trois aient fini.

## 4. Le rendu

Écris dans le dossier courant un fichier `recherche-en-equipe-` suivi du sujet en deux ou trois
mots, `.md`, qui contient :

- la réponse à la question en quinze lignes au plus, chaque fait avec l'adresse de sa page ;
- « Ce qui a été contesté » : chaque fait attaqué par le contradicteur, et qui a eu raison ;
- « Ce que personne n'a trouvé ».

N'invente aucune adresse : un fait sans source n'entre pas dans le fichier. Ne modifie aucun
autre fichier.

Puis demande à chaque coéquipier de s'arrêter, et donne à l'utilisateur le chemin du fichier et
les trois lignes qui comptent le plus.
