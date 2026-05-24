# GLSimpleSQL — Interpréteur de Requêtes SQL Simplifiées

![C](https://img.shields.io/badge/C-A8B9CC?style=flat-square&logo=c&logoColor=white)
![Flex](https://img.shields.io/badge/Flex-Lexical_Analyzer-blue?style=flat-square)
![Bison](https://img.shields.io/badge/Bison-Parser_Generator-orange?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)

Interpréteur de requêtes SQL simplifiées développé en langage C, utilisant Flex pour l'analyse lexicale et Bison pour l'analyse syntaxique, dans le cadre du module Théorie des Langages et Compilation.

---

## Description

GLSimpleSQL est un interpréteur qui analyse, valide et affiche des informations détaillées sur des requêtes SQL simplifiées. Il ne s'agit pas d'un vrai SGBD — l'interpréteur effectue uniquement l'analyse lexicale, syntaxique et sémantique des requêtes.

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
MiniProjet/
├── src/
│   ├── lexer.l         # Analyseur lexical (Flex)
│   ├── parser.y        # Analyseur syntaxique (Bison)
│   ├── main.c          # Point d'entrée du programme
│   ├── symbols.c/h     # Gestion de la table des symboles
│   └── semantic.c/h    # Actions sémantiques
├── tests/
│   ├── test1.sql
│   ├── test2.sql
│   └── erreurs.sql
├── build/
│   └── fichiers générés (parser.tab.c, lex.yy.c)
├── Grammaire.pdf
└── README.md
```

---

## Compilation et Exécution

### Prérequis

- GCC
- Flex
- Bison

### Compilation

```bash
bison -d parser.y
flex lexer.l
gcc parser.tab.c lex.yy.c main.c -o glsql -lfl
```

### Exécution avec un fichier

```bash
./glsql test.txt
```

### Exécution interactive

```bash
./glsql
```

---

## Exemple d'utilisation

Entrée :
```sql
CREATE TABLE Etudiant (id INT, nom VARCHAR(50), age INT);
INSERT INTO Etudiant VALUES (1, 'Ali', 22);
SELECT nom FROM Etudiant WHERE age > 20;
UPDATE Etudiant SET age = 23 WHERE id = 1;
DELETE FROM Etudiant WHERE age < 18;
DROP TABLE Etudiant;
```

Sortie :
```
=== Interpreteur GLSimpleSQL ===
CREATE TABLE detecte : Etudiant
INSERT INTO Etudiant : 3 valeurs (nombre correct)
SELECT avec WHERE, table=Etudiant, nb_champs=1 (colonnes OK)
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
ERREUR SEMANTIQUE ligne 3 :
La table 'Produit' n'existe pas.
```

---

## Actions Sémantiques

Pour chaque requête analysée, le programme affiche des statistiques détaillées.

Exemple pour SELECT :
```
Requete SELECT analysee :
- Table : Etudiant
- Nombre de champs : 2 (nom, age)
- Clause WHERE : OUI
- Nombre de conditions : 1
- Operateurs logiques : 0
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
