# Neurodex

**L’encyclopédie à collectionner de l’esprit humain.** Un jeu de cartes à collectionner éducatif : chaque série présente un concept de psychologie ou de neurosciences, appuyé sur des sources académiques.

Ce dépôt contient le prototype web mobile (React), version 0.6

## Tester sur téléphone en 5 minutes (GitHub Pages)

1. Crée un dépôt sur GitHub et pousse ce dossier sur la branche `main`.
2. Dans **Settings › Pages**, choisis **GitHub Actions** comme source.
3. Attends la fin du déploiement dans l’onglet **Actions** (environ 1 minute).
4. Ouvre l’adresse indiquée (du type `https://ton-compte.github.io/neurodex/`) sur ton téléphone.
5. Pour l’utiliser comme une vraie appli : **Partager › Sur l’écran d’accueil** sur iPhone (Safari), ou **⋮ › Ajouter à l’écran d’accueil** sur Android (Chrome). L’appli s’ouvre alors en plein écran avec son icône.

Pour ouvrir autant de boosters que voulu pendant les tests, ajoute `#test` à la fin de l’adresse. Un bouton « Test : booster Shiny + Mythe + Ultra » apparaît alors sur l’accueil.

## Tester en local

Prérequis : Node.js 18 ou plus récent.

```bash
npm install
npm run dev
```

Le terminal affiche une adresse « Network » (par exemple `http://192.168.1.20:5173`) : ouvre-la sur un téléphone connecté au même Wi-Fi.

```bash
npm run build     # site statique dans dist/
npm run preview   # sert le build localement
```

Remarque : le gyroscope (« Pencher avec le téléphone ») n’est autorisé par les navigateurs que sur une adresse **https**. En local sur le Wi-Fi, utilise plutôt le glisser au doigt ; sur GitHub Pages, tout fonctionne.

## Ce que change la version 0.6 (Mirages et Ultra Shiny)

Les 10 cartes spéciales passent elles aussi à la nouvelle lisibilité, en gardant leur identité propre :

- **Mirages (5)** : dessin « fantôme » en traits lilas sur fond nuit, cadre en pointillés, panneau crème au bord ondulé ; l’idée reçue, puis « En réalité », puis la source toujours en bas. L’héroïne est le seul élément en couleur.
- **Ultra Shiny (5)** : scène dans l’horizon de la zone, entièrement recouverte d’un fractured foil irisé, cadre crème nacré ; l’héroïne rend hommage au chercheur sans portrait, avec les symboles de ses travaux.
- **Lucioles** : les Mirages et les Ultra Shiny ont maintenant aussi leur luciole cachée.

## Ce que change la version 0.5 (refonte complète des 10 séries)

Les 60 cartes de série (10 séries de 5 cartes + leurs 10 Shiny) sont refaites. Les Mirages et les Ultra Shiny ne changent pas.

- **Lisibilité sur téléphone** : texte principal 50 % plus grand, aucun texte sous 20 px, intitulés en langage simple (« L’idée », « On l’a testé », « Comment ça marche », « Une histoire vraie »), une définition en une phrase sur chaque carte 1.
- **Structure stable** : titre et texte centrés ; le bloc « Source », « À nuancer », « Bon à savoir » ou « Le lien » toujours au même endroit, en bas de la carte.
- **Un horizon par zone**, en rendu aérographe aux formes arrondies :
  - Forêt des biais : château dans la brume, la nuit ;
  - Jardin des émotions : champ de blé sous un ciel d’orage ;
  - Montagne de la motivation : vallée au soleil couchant ;
  - Village des relations : campagne au crépuscule ;
  - Observatoire de la personnalité : ciel étoilé.
- **Cartes maîtresses** en pleine illustration, cadre foil, avec seulement le nom de la série.
- **L’héroïne** est le personnage principal de chaque carte ; c’est elle qui rejoue les expériences et les histoires vraies.
- **Lucioles** repositionnées sur toutes les nouvelles illustrations.

Questions à poser aux testeurs : le texte se lit-il sans zoomer ? Comprend-on l’idée de chaque carte en une lecture ? Les cinq univers se reconnaissent-ils au premier coup d’œil ?

## Ce que contient la version 0.4

- **70 cartes V3** dans l’univers pictural du Parc des Idées : 10 séries de 5 cartes (dont 10 cartes maîtresses en foil), 10 Shiny prismatiques, 5 Mirages (les idées reçues) et 5 Ultra Shiny en fractured foil.
- **Nouveau booster** : sachet aux soudures dorées, à déchirer par le haut.
- **Lucioles cachées** : une par carte de série et par Shiny ; en inspection, toucher la luciole rapporte +5 éclats de savoir.
- **Vidéo d’explication de 30 secondes** au tout premier booster (rejouable avec « Comment ça marche ? »).
- **Booster du jour** à déchirer au doigt, révélation en crescendo (de la plus commune à la plus rare), effets spéciaux pour les Shiny, Mythes et Ultra Shiny.
- **Inspection 3D** : chaque carte se penche au doigt ou avec le gyroscope, reflets et holographie suivent l’angle, verso consultable.
- **Éclats de savoir** (booster du jour et doublons) et **atelier** pour fabriquer les cartes manquantes.
- **Collection** : fresques des séries, onglet des cartes bonus.
- Sauvegarde locale et demande d’e-mail (prototype : rien n’est envoyé à un serveur).

## Équilibrage

| Type | Cartes | Fréquence |
| --- | --- | --- |
| Commune | 20 (illustration, histoire vraie) | 3 par booster |
| Peu commune | 10 (mécanisme) | emplacement 4 (75 %), emplacement 5 (15 %) |
| Rare | 10 (expérience) | emplacement 4 (25 %), emplacement 5 (85 %) |
| Shiny | 10 | environ 1 booster sur 8, garantie au 10e booster sans Shiny |
| Mirage | 5 | environ 1 booster sur 25 |
| Ultra Shiny | 5 | environ 1 booster sur 40 ; un Mythe ou une Ultra garanti au 30e booster |
| Carte maîtresse | 10 | série complète |

Éclats : +10 par booster du jour ; doublons +5 / +10 / +20 / +50 / +100 selon la rareté. Atelier : 40 / 80 / 150 / 400 / 800.

Les taux se règlent dans `src/App.jsx` (fonctions `rollSlot` et `draw`, constantes `DUP`, `COST`, `PITY_SHINY`, `PITY_BIG`).

## Structure

```
src/
  App.jsx            l’appli : accueil, intro, booster, révélation, collection, atelier, inspection 3D
  main.jsx           démarrage, ciel étoilé
  styles.css
  data/
    cards.json       les 70 cartes (HTML/SVG, format 630 × 880)
    catalog.js       séries et catalogue (rareté, libellés)
    art.js           dos de carte, illustration du booster
    hills.js         collines de fond
public/              icônes, manifeste pour l’écran d’accueil
prototype/index.html version autonome en un seul fichier
```

## Avant toute diffusion publique

- Vérifier les références, dates et chiffres marqués « à vérifier » dans les publications d’origine.
- Prévoir un vrai serveur pour la sauvegarde par e-mail (connexion par lien envoyé par e-mail).
- Définir la licence du dépôt (par défaut : tous droits réservés).
