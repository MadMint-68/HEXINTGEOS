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
