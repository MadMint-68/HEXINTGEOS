# Mémo Formules & Codes Réutilisables

Bienvenue dans ce fichier **Mémo.md**, qui sert de mémo personnel pour garder en un seul endroit toutes mes formules, scripts et extraits de code utiles. L’objectif est de pouvoir les retrouver rapidement et les réutiliser facilement dans mes projets.

---

## Table des matières

1. [Formules Excel / LibreOffice](#formules-excel--libreoffice)  
2. [Scripts et Macros](#scripts-et-macros)  
3. [SQL & Bases de données](#sql--bases-de-données)  
4. [Commandes et astuces système](#commandes-et-astuces-système)  
5. [Notes et idées diverses](#notes-et-idées-diverses)  

---

## Formules Excel / LibreOffice

### Conversion coordonnées décimales → degrés, minutes, secondes (DMS)

```excel
=INT(ABS(VALUE(TRIM(LEFT(A2,FIND(",",A2)-1)))) ) & "° " &
INT(MOD(ABS(VALUE(TRIM(LEFT(A2,FIND(",",A2)-1))))*60,60)) & "’ " &
SUBSTITUTE(TEXT(MOD(ABS(VALUE(TRIM(LEFT(A2,FIND(",",A2)-1))))*3600,60),"0.000"),",",".") & "” " &
IF(VALUE(TRIM(LEFT(A2,FIND(",",A2)-1)))>=0,"N","S") & "  " &
INT(ABS(VALUE(TRIM(MID(A2,FIND(",",A2)+1,100)))) ) & "° " &
INT(MOD(ABS(VALUE(TRIM(MID(A2,FIND(",",A2)+1,100))))*60,60)) & "’ " &
SUBSTITUTE(TEXT(MOD(ABS(VALUE(TRIM(MID(A2,FIND(",",A2)+1,100))))*3600,60),"0.000"),",",".") & "” " &
IF(VALUE(TRIM(MID(A2,FIND(",",A2)+1,100)))>=0,"E","W")
```
### Paramètres requis pour la formule de conversion coordonnées décimales-DMS

- **Cellule d’entrée** : La formule attend que la cellule référencée (`A2` dans l’exemple) contienne une chaîne de texte représentant des coordonnées géographiques au format suivant : `latitude,longitude`

  Exemple : `48.8566,2.3522`

- La latitude et la longitude doivent être séparées par une **virgule `,`** (et non un point-virgule ou autre caractère).

- Les valeurs peuvent être positives ou négatives (ex : `-23.5, 45.7`).

- La formule prend en compte les espaces autour des nombres et les supprime automatiquement (fonction `TRIM`).

- **Format attendu** :

  - Latitude en décimal : nombre réel positif ou négatif.

  - Virgule comme séparateur.

  - Longitude en décimal : nombre réel positif ou négatif.

- **Contraintes** :

  - Pas de texte additionnel dans la cellule (pas de mots, uniquement les coordonnées).

  - Les décimales doivent utiliser un **point ou une virgule** selon la configuration locale, mais la formule fonctionne bien si la cellule est en texte.

- **Exemple de cellule valide** :

  - `48.8566,2.3522`

  - `-23.456, 45.678`

  - `0,0`

- **Résultat attendu** :

  La formule convertira la coordonnée décimale en :  
  `48° 51’ 23.760” N  2° 21’ 7.920” E`

- **Remarques** :

  - Si la cellule ne contient pas de virgule, la formule renverra une erreur (#VALUE!) car elle utilise la fonction `FIND` pour localiser la virgule.

  - Si le format est différent (par exemple point-virgule `;` ou espace comme séparateur), la formule doit être adaptée.
