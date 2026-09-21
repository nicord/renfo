# Renfo — lecteur de séance

Un chronomètre de renforcement musculaire pour le téléphone : bips à chaque changement d'étape, aperçu de l'exercice suivant, écran maintenu allumé, fonctionnement hors ligne après le premier chargement. Une seule page HTML, sans dépendance ni build.

**Page :** https://nicord.github.io/renfo/

## Utilisation

Le programme de la séance est décrit dans l'URL, après le `#` :

```
https://nicord.github.io/renfo/#@reprise
https://nicord.github.io/renfo/#@echauf-court,[bridge-band,abd,clam,r60]x2,plank:45
https://nicord.github.io/renfo/#bridge,abd:30,r45,~Marche~60
```

Ce qui suit le `#` n'est jamais envoyé au serveur : la page lit le programme localement. Sans `#`, la séance type `@reprise` s'ouvre par défaut.

Le bouton ☰ ouvre l'éditeur du programme, avec « Copier le lien », le déroulé complet, les fiches détaillées des exercices et le catalogue des identifiants.

## Syntaxe

| Élément | Sens |
|---|---|
| `id` | un exercice, avec sa durée par défaut |
| `id:45` | le même exercice avec une durée de 45 s |
| `r45` | repos de 45 s (remplace le repos automatique qui précède) |
| `[a,b,c]x2` | groupe répété 2 fois (affiché « Tour 1 », « Tour 2 ») |
| `@nom` | séance type ou échauffement prédéfini |
| `~Nom~40` | étape libre de 40 s, pour un exercice absent de la base |

Les exercices à deux côtés (abduction, coquille, planche latérale, etc.) sont dédoublés automatiquement : droite, puis gauche. Chaque exercice ajoute un repos automatique défini dans la base.

## Contenu

**Exercices** (identifiants) : `hip`, `swing-ap`, `swing-lat`, `knees`, `bridge`, `bridge-band`, `bridge-sl`, `monster`, `abd`, `abd-band`, `clam`, `bal`, `sldl`, `sldl-w`, `step-up`, `plank`, `sp-knees`, `sp-feet`, `sp-any`.

**Séances types** : `@echauf`, `@echauf-court`, `@reprise`, `@maintenance`, `@entretien`, `@sans-materiel`.

Chaque exercice a une fiche : mise en place, exécution, erreurs à éviter, ce qu'il vise.

## Ajouter un exercice ou une séance type

Toute la base est un bloc JSON dans `index.html` (`<script type="application/json" id="db">`). Il n'y a pas de code à modifier :

- un exercice : ajouter une entrée dans `ex` (champs `t` titre, `p` phase, `d` durée par défaut en secondes, `rest` repos automatique après, `sides` pour droite/gauche, `s` dose affichée, `cue` consigne du bandeau, `m` `e` `w` `g` pour la fiche) ;
- une séance type : ajouter une entrée dans `presets` (`t` titre, `p` programme, dans la même syntaxe que l'URL).

Le JSON doit rester valide : sans virgule en trop, et les guillemets doubles dans les textes remplacés par « » ou échappés.

## Confidentialité

Le dépôt est public : il ne contient que du contenu générique (fiches d'exercices et séances types). Aucune donnée personnelle, historique de santé ni séance datée ne doit y figurer. Les programmes individuels vivent uniquement dans des liens, hors de ce dépôt.