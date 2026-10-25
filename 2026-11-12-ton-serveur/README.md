# Ferme ton ordinateur, Claude continue : installe ton premier serveur

**École Noésia · live du jeudi 12 novembre 2026 · Brice Gachadoat**

Tout ce qui sert au live est rangé dans ce dossier. Tu n'as rien à télécharger : ouvre le
fichier, lis-le, et copie ce dont tu as besoin.

## Dans ce dossier

- **L'exercice** : juste en dessous.
- **Le cadeau** : la bibliothèque de phrases à donner à Claude pour installer et sécuriser ton
  serveur (sécurisation, Docker, Caddy et le HTTPS, code-server sur ton domaine, n8n, Coolify,
  sauvegardes, entretien du mois). Il arrive ici au plus tard le jour du live.
- **Le support de la présentation** : il arrive ici après le live.

## L'exercice (facultatif)

Pour ceux qui veulent se lancer : loue ton serveur, installe Claude Code dessus, puis
demande-lui l'état des lieux et la sécurisation. Compte une heure.

Apporte trois preuves à la Permanence Technique du vendredi 13 novembre, de 12h30 à 13h30 :

1. une capture de Claude Code lancé sur ton serveur ;
2. ton fichier REGISTRE.md avec au moins trois lignes (quoi, pourquoi, comment le relancer) ;
3. la liste des ports ouverts que Claude t'aura donnée, avec seulement ceux dont tu as besoin.

En bonus, n8n ou code-server ouvert en HTTPS sur ton sous-domaine. Pense à masquer l'adresse de
ton serveur sur tes captures.

Ce qu'on regarde à la permanence : Claude Code tourne sur le serveur, pas sur ton ordinateur ;
chaque ligne du registre a ses trois colonnes ; aucun port de base de données ni le port brut
de n8n (5678) n'est ouvert sur internet, seulement la connexion SSH et le web.

## Ce qu'il te faut pour suivre

Un abonnement Claude Pro ou Max (Claude Code n'est pas inclus dans le plan gratuit), un serveur
loué sous Ubuntu avec au moins 4 Go de mémoire (8 Go si tu veux n8n à côté), et un nom de
domaine pour le bonus. Accessibilité 3/5 : tout se passe dans un terminal, mais c'est Claude
qui tape les commandes.

## Les liens utiles

- Installer Claude Code (configuration requise et commande d'installation) :
  https://code.claude.com/docs/en/setup
- Se connecter à Claude Code depuis un serveur sans navigateur :
  https://code.claude.com/docs/en/authentication
- Installer n8n avec Docker, la documentation officielle :
  https://docs.n8n.io/hosting/installation/docker/
- Installer Coolify : https://coolify.io/docs/get-started/installation

Une question ? Viens à la Permanence Technique du vendredi 13 novembre, de 12h30 à 13h30.
