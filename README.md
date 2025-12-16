

#  — Mini Projet GLSimpleSQL

**Théorie des Langages et Compilation – Année 2025/2026**
**Interpréteur de requêtes SQL simplifiées (Flex & Bison)**


##  1. Description du Projet

Ce projet consiste à développer un **interpréteur de requêtes SQL simplifiées** appelé *GLSimpleSQL*.
Il a été réalisé en langage **C**, avec :

* **Flex** pour l’analyse lexicale
* **Bison** pour l’analyse syntaxique
* Une **gestion sémantique** permettant d’effectuer vérifications et statistiques

 **Important :**
Cet interpréteur **n’exécute pas les requêtes sur une vraie base de données**. Il se limite à analyser, valider et afficher des informations détaillées sur les requêtes SQL.


##  2. Objectifs Pédagogiques

Ce projet permet de :

* Maîtriser **Flex** (analyse lexicale)
* Comprendre et implémenter **Bison** (analyse syntaxique)
* Manipuler une **grammaire formelle**
* Construire des **actions sémantiques**
* Gérer une **table des symboles** (tables, champs, types)
* Détecter et afficher des **erreurs lexicales, syntaxiques et sémantiques**



##  3. Fonctionnalités Supportées

L’interpréteur reconnaît les commandes suivantes du langage **GLSimpleSQL** :

###  CREATE TABLE

Créer une table avec champs et types.

###  INSERT INTO

Insérer des valeurs dans une table.

###  SELECT

Interroger une table, avec ou sans clause WHERE.

###  UPDATE

Modifier des lignes existantes.

###  DELETE

Supprimer des lignes ou vider une table.

###  DROP TABLE

Supprimer une table entière.



##  4. Types et Opérateurs Supportés

### Types :

* `INT`
* `FLOAT`
* `VARCHAR(n)`
* `BOOL`

### Opérateurs :

* Comparaison : `=`, `!=`, `<`, `>`, `<=`, `>=`
* Logiques : `AND`, `OR`, `NOT`



##  5. Structure du Projet

```
MiniProjet/
│── src/
│   ├── lexer.l           -> Analyseur lexical (Flex)
│   ├── parser.y          -> Analyseur syntaxique (Bison)
│   ├── main.c            -> Point d’entrée du programme
│   ├── symbols.c/h       -> Gestion de la table des symboles
│   ├── semantic.c/h      -> Actions sémantiques
│
│── tests/
│   ├── test1.sql
│   ├── test2.sql
│   ├── erreurs.sql
│
│── build/
│   └── fichiers générés (p.tab.c, lex.yy.c…)
│
│── Grammaire.pdf        -> Grammaire complète GLSimpleSQL
│── Rapport.pdf          -> Rapport détaillé
│── README.md            ->Ce fichier
```



##  6. Compilation et Exécution

### 1️ Génération des fichiers Flex/Bison

```bash
bison -d parser.y  
flex lexer.l
gcc parser.tab.c lex.yy.c main.c -o glsql
```

### 2️ Lancer l'interpréteur

```bash
./glsql
```

### 3️ Saisir une requête SQL simplifiée 
*« Chaque fichier test doit contenir une seule requête SQL simplifiée !!! »*

Exemple :

```
CREATE TABLE Etudiant(id INT, nom VARCHAR(50), age INT);
INSERT INTO Etudiant VALUES (1, 'Ali', 22);
SELECT nom FROM Etudiant WHERE age > 20;
```


##  7. Actions Sémantiques Implémentées

Pour chaque requête, le programme affiche des statistiques :

### Exemple SELECT :

```
Requête SELECT analysée :
- Table : Client
- Nombre de champs : 2 (nom, prenom)
- Clause WHERE : OUI
- Nombre de conditions : 1
- Opérateurs logiques : 0
```

### Vérifications accomplies :

* Table existante / inexistante
* Champs valides
* Nombre de valeurs correct (INSERT)
* Duplications de tables (CREATE)
* Utilisation incorrecte de `*`
* Suppression d’une table inexistante

### Erreurs claires (exemples) :

```
ERREUR SÉMANTIQUE ligne 3 :
La table 'Produit' n'existe pas.
```

###  Tests d'erreurs :

* Table inexistante
* Champ inexistant
* Nombre de valeurs incorrect
* Syntaxes invalides
* Table déjà existante


##  9. Livrables Fournis

*  Code source complet
*  Grammaire complète — *Grammaire.pdf*
*  Rapport détaillé — *Rapport.pdf*
*  Vidéo de démonstration
*  README.md (ce fichier)


##  10. Auteurs

Mini projet réalisé par HAJIR SALAH EDDINE, KASRI CHOUAYB, MERIZAK FERDAOUSSE,KHYAR IBTISSAM, dans le cadre du module **Théorie des Langages et Compilation (I513)**, filière **LST GL S5**.

Professeur encadrant :
**<3 MOUHNI NAOUAL <3**


##  11. Ressources Utilisées

* Manuel Flex:  https://westes.github.io/flex/manual/
* Manuel Bison:  https://www.gnu.org/software/bison/manual/
* GCC: https://www.youtube.com/watch?v=oC69vlWofJQ&t=41s
* Visual Studio Code
* LMMS(large langage models): ChatGPT, DeepSeek




