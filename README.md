# GLSimpleSQL — Interpréteur de Requêtes SQL Simplifiées

![C](https://img.shields.io/badge/C-A8B9CC?style=flat-square&logo=c&logoColor=white)
![Flex](https://img.shields.io/badge/Flex-Lexical_Analyzer-blue?style=flat-square)
![Bison](https://img.shields.io/badge/Bison-Parser_Generator-orange?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)

Interpréteur de requêtes SQL simplifiées développé en langage C, utilisant Flex pour l'analyse lexicale et Bison pour l'analyse syntaxique, dans le cadre du module Théorie des Langages et Compilation.

---

## Description

GLSimpleSQL analyse, valide et affiche des informations détaillées sur des requêtes SQL simplifiées. Il ne s'agit pas d'un vrai SGBD — l'interpréteur effectue uniquement l'analyse lexicale, syntaxique et sémantique des requêtes.

> Faculté des Sciences et Techniques — Errachidia | Module I513 — LST GL S5 | 2025–2026

---

## Fonctionnalités

- Analyse lexicale avec Flex
- Analyse syntaxique avec Bison (grammaire LALR)
- Gestion d'une table des symboles (tables, champs, types)
- Vérifications sémantiques complètes
- Détection et affichage d'erreurs lexicales, syntaxiques et sémantiques
- Exécution depuis un fichier ou en mode interactif

---

## Commandes SQL Supportées

| Commande | Description |
|----------|-------------|
| CREATE TABLE | Créer une table avec colonnes et types |
| INSERT INTO | Insérer des valeurs dans une table |
| SELECT | Interroger une table avec ou sans WHERE |
| UPDATE | Modifier des lignes existantes |
| DELETE | Supprimer des lignes selon une condition |
| DROP TABLE | Supprimer une table entière |

---

## Types et Opérateurs

**Types supportés :** INT, FLOAT, VARCHAR(n), BOOL

**Opérateurs de comparaison :** =, !=, <, >, <=, >=

**Opérateurs logiques :** AND, OR, NOT

---

## Structure du Projet

```
miniprojet/
├── main.c              # Point d'entrée du programme
├── flex.l              # Analyseur lexical (Flex)
├── bison.y             # Analyseur syntaxique (Bison)
├── bison.tab.c         # Fichier généré par Bison
├── bison.tab.h         # En-tête généré par Bison
├── lex.yy.c            # Fichier généré par Flex
├── test.txt            # Requêtes SQL valides
└── testE.txt           # Cas d'erreurs
```

---

## Compilation et Exécution

### Prérequis

- GCC
- Flex
- Bison

### Compilation

```bash
bison -d bison.y
flex flex.l
gcc bison.tab.c lex.yy.c main.c -o miniprojet -lfl
```

### Exécution avec un fichier

```bash
./miniprojet test.txt
```

### Exécution interactive

```bash
./miniprojet
```

---

## Exemple d'utilisation

Entrée (`test.txt`) :
```sql
CREATE TABLE Etudiant (id INT, nom VARCHAR(50), age INT);
INSERT INTO Etudiant VALUES (1, 'Diallo', 20);
SELECT * FROM Etudiant;
SELECT nom, age FROM Etudiant WHERE age > 18;
UPDATE Etudiant SET age = 21 WHERE id = 1;
DELETE FROM Etudiant WHERE age < 18;
DROP TABLE Etudiant;
```

Sortie :
```
=== Interpreteur GLSimpleSQL ===
CREATE TABLE detecte : Etudiant
INSERT INTO Etudiant : 3 valeurs (nombre correct)
SELECT simple, table=Etudiant, nb_champs=1 (colonnes OK)
SELECT avec WHERE, table=Etudiant, nb_champs=2 (colonnes OK)
UPDATE table=Etudiant : 1 modifications (colonnes SET/WHERE verifiees)
DELETE conditionnel table=Etudiant (colonnes WHERE verifiees)
DROP TABLE Etudiant
=== Fin de l'analyse SQL ===
```

---

## Gestion des Erreurs

| Type d'erreur | Exemple |
|---------------|---------|
| Table inexistante | SELECT * FROM Produit; |
| Colonne inexistante | SELECT prix FROM Etudiant; |
| Nombre de valeurs incorrect | INSERT INTO Etudiant VALUES (1, 'Ali'); |
| Table déjà existante | CREATE TABLE Etudiant (id INT); |
| Erreur syntaxique | SELECT FROM Etudiant; |

Exemple de message d'erreur :
```
ERREUR : table 'Produit' inexistante pour SELECT.
ERREUR : colonne 'prix' inexistante dans la table 'Etudiant' pour SELECT.
ERREUR : 2 valeurs fournies, mais la table 'Etudiant' a 3 colonnes.
Erreur syntaxique ligne 23 : syntax error
```

---

## Ressources

- [Manuel Flex](https://westes.github.io/flex/manual/)
- [Manuel Bison](https://www.gnu.org/software/bison/manual/)

---

## Auteurs

| Nom | Filière |
|-----|---------|
| KASRI Chouayb | LST Génie Logiciel |
| HAJIR Salah Eddine | LST Génie Logiciel |
| MERIZAK Ferdaousse | LST Génie Logiciel |
| KHYAR Ibtissam | LST Génie Logiciel |

Encadrant : Mme MOUHNI Naoual — FST Errachidia
