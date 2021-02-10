# guide-developpement-web
Ensemble de règle et de bonnes pratiques de développement Web

[Guide HTML](guide-html.md)
[Guide CSS](guide-css.md)
[Liste de contrôle -101](liste-de-controle-101.md)
[Liste de contrôle](liste-de-controle.md)

-------------------------------------------------------------------------------

# Guide HTML


## Généralités

- L’encodage des fichiers et des bases de données doit se faire en UTF-8. 
- Séparer les noms des fichiers, des images des classes et id CSS par des tirets (`.slide-info`, `styles-ie.css`, `jquery-2.0.min.css`, etc), sauf convention contraire apportée par le client.
- Les noms d'éléments et des attributs sont rédigés en minuscules,
- Les éléments sont imbriqués correctement,
- L'usage des guillemets doubles est préconisé autour des valeurs d’attributs (ex. `class="fruit"`) ainsi que les simples quotes dans les autres langages JavaScript, PHP (ex. `alert('blup');`) de manière à faciliter les imbrications (ex. `alert('<p class="fruit">plop</p>');`)

## Doctype

Le doctype HTML5 est fortement recommandé.

```html
<!DOCTYPE html>
```

## Langue

La langue de la page est systématiquement renseignée via un attribut dans l’élément `<html>` :

```html
<html lang="fr"></html>
```

## Encodage

L’encodage du document (en UTF-8) est systématiquement renseigné via un élément meta placé dans le `<head>` avant le title:

```html
<meta charset="UTF-8" />
```

## Titre de la page

Le titre de page, différent à chaque page, est systématiquement renseigné via un élément `<title>` dans le `<head>` :

```html
<title>Titre significatif du contenu de la page</title>
```

## Meta "Viewport"

Pour une adaptation du site web vers les terminaux mobiles, l’élément `<meta name="viewport">` est ajouté dans la partie `<head>`.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

**_Note : Les syntaxes empêchant l’agrandissement des contenus par le visiteur sont proscrites (maximum-scale=1, user-scalable=no, etc.)._**

## Favicon

L’icône de favori est utilisée de différentes manières par les navigateurs et systèmes. Le format ICO est ancien, le format PNG permet une meilleure définition avec un poids plus léger.  
- Tous les navigateurs récents reconnaissent le format PNG  
- IE ne reconnaît pas le format PNG et va chercher par défaut dans la racine `/favicon.ico`  

Source : [http://realfavicongenerator.net/](http://realfavicongenerator.net/)

## Sémantique structurelle 

Les éléments HTML5 `<header>`, `<article>`, `<main>`, `<footer>`, `<aside>`, `<section>` et `<nav>` sont privilégiés aux éléments neutres `<div>` si leur fonction s’y prête.

La structure globale préconisée est celle-ci :

- `<body>` : corps de page et du site web
- `<div id="layout-page">` : sous-conteneur optionnel. Par exemple pour centrer.
- `<header id="header" role="banner">` : entête global, comportant souvent la navigation et des éléments qui se retrouvent en commun sur (quasiment) toutes les pages
- `<main id="main" role="main">` : conteneur général du contenu principal, typiquement ce qui n'est pas dans header et footer
- `<footer id="footer" role="contentinfo">` : pied de page global comportant des éléments qui se retrouvent en commun sur (quasiment) toutes les pages  
- `<aside class="aside" role="complementary">` : barre latérale globale. Note : `<aside>` doit pouvoir être extrait de la page sans poser de problème, en clair ne pas y placer la navigation par exemple.
- `<nav id="navigation" role="navigation">` : navigation principale
- `<form id="search" role="search">` : recherche principale

__En savoir plus sur la sémantique structurelle__
https://www.w3.org/WAI/tutorials/page-structure/


#### Menu de navigation

Utiliser des combinaisons `<ul><li>` (liste non ordonnée) pour structurer les menus de navigation dans un élément `<nav role="navigation”>`.

### Hiérarchie des titres h1-h6
L'objectif est de former une table des matières des contenus du document Web.
Vérifier cette table des matières à l'aide d'un outil qui prélève les h1-h6 de la page comme par exemple avec la barre d'outils de développement de Chris Pederick.
Installer cette extension pour Chrome et faites afficher la table des matières d'un document Web en utilisant le menu *View Document Outline* de l'onglet *Informations*.
- Respecter la hiérarchie des titres `<hX>`.
- `h1` est unique et décrit le thème de la page
- Les titres (`h1`, `h2`, `h3`, etc.) sont utilisés dans l'ordre et de manière pertinente

### Sémantique des éléments
- Utiliser les éléments HTML pour leur fonction/sémantique et non pas pour leur forme.
- Les textes doit être lus et analysés afin d'identifier les contenus dont on peut préciser la nature à l'aide d'un élément et de ses attributs.

__Exemples:__  
- une citation (de Amanda Gorman)
```html
<q> Car il y a toujours de la lumière, si seulement nous sommes assez courageux pour la voir, si seulement nous sommes assez courageux pour l’incarner. </q>
```
- une date
```html
<time datetime="2021-01-20"> Jour de l'investiture du président Joe Biden. </time>
```
- une abbréviation  
Remarquez que dans le cas d'une abbréviation, on suggère de mettre aussi entre parenthèses la signification complète de l'acronyme ou de l'abbréviation au premier emploi de celui-ci dans un texte.
```html
<abbr title="HyperText Mark-Up Language"> HTML (HyperText Mark-Up Language)</abbr>
```

__En savoir plus sur la sémantique des éléments et attributs HTML__    
https://developer.mozilla.org/fr/docs/Web/HTML/Element 

-------------------------------------------------------------------------------

# Guide CSS

Ce document évolutif recense les bonnes pratiques CSS à appliquer en production.

## Base

### L’encodage des fichiers doit se faire en UTF-8.   
Notez qu'il est essentiel que l'instruction d'encodage se trouve sur la première ligne du fichier.  
Aucun commentaire, ni même un saut de ligne, ne doit être présent avant cette instruction.

```css
@charset "UTF-8";
```

### "Reset" de la feuille de styles des navigateurs

Un "reset" CSS permettant d'harmoniser les styles par défaut des navigateurs est systématiquement appliqué 
en début de projet.

### Un seul fichier CSS est relié aux documents HTML (ou 2!)  
Une division modulaire des styles en plusieurs fichiers est souhaitée.  
Cependant, pour assembler (et minifier) ces différents fichiers en un seul, l'usage d'un pré-processeur tel que __sass__ est requis.  
L'instruction `@import` en CSS n'est pas une bonne alternative à sass, car elle a un impact négatif sur la performance.   

Aussi, en attendant de faire l'apprentissage de sass, 2 fichiers .css seront prescrits:   
(1) la feuille de styles de réinitialisation "normalize-v8.css"  
(2) la feuille de styles principale nommée "styles.css"  
Chacun de ces fichiers seront reliés au document HTML par une balise `link`.  
L'ordre est important, le *reset* doit être relié avant "styles.css".

### Des commentaires structurants subdivisent le fichier "styles.css"    
(1) `/* POLICES LIÉES */`  
(2) `/* UTILITAIRES */`  
Nous placerons ici le modèle de boîte à utiliser (border-box) et quelques classes d'usage courant comme *clearfix*   
et les classes d'accessibilité comme *screen-reader-only*.  
(3) `/* CHARTE TYPOGRAPHIQUE */`  
La charte graphique de base comporte   
•	la police de caractère principale, soit celle qui sert pour le texte courant,     
en plus des polices alternatives et de la collection (sans-serif ou serif, selon votre choix)   
•	la taille de caractère de base en "rem" (précédemment en "em")  
•	la couleur de caractère   
•	la hauteur de ligne (sans unité)  
(4) `/* NAVIGATION */`  
(5) `/* HYPERLIENS */`  
(6) `/* GRILLE DE MISE EN PAGE */`  
(7) `/* ... */`  

### Table des matières
Pour faciliter la navigation dans le fichier  "styles.css" on ajoutera, tout de suite après l'instruction 
du jeu de caractères utf-8, une table des matières consistant à reprendre de manière intégrale les commentaires
structurants.   
On prendra soin de maintenir à jour cette table des matières de sorte qu'on puisse utiliser   
les titres pour naviguer vers cette section du fichier grâce à la commande *Find*.      

Exemple:  
`/*** TABLE DES MATIÈRES ***/`      
`/* POLICES LIÉES */`     
`/* UTILITAIRES */`   
`/* CHARTE TYPOGRAPHIQUE */`     
`/* NAVIGATION */`   
`/* HYPERLIENS */`    
`/* GRILLE DE MISE EN PAGE */` 

La forme des commentaires structurants et de la table des matières peut être adaptée.     
Par exemple, si on préfère les commentaires structurants en bas de casse avec une ligne de soulignement
comme ceci:
```css
/* Utilitaires
   ========================================================================== */
```
La table des matières ressemblera plutôt à cela:
```css
/**
 * @author Prenom Nom <courriel>
 *
 * TABLE DES MATIERES
 *
 * Normalize (au lieu du reset)
 * Utilitaires
 * Charte typographique
 * Grilles de mise en page
 * Hyperliens et interactivite
 *
 */
```
L'important est de reprendre avec le même orthographe et choix de casse les commentaires structurants 
dans la table des matières de sorte que la fonction *Find* puisse être utilisée.

## Sélection des éléments

La maintenabilité des feuilles de styles est une priorité. 
Il est nécessaire de prioriser les sélecteurs ayant le moins de spécificité (poids) possible afin de faciliter 
les modifications ultérieures ou dans des contextes différents (Responsive).

Privilégier au maximum l'usage de [**classes**](http://www.drinchev.com/blog/css-with-only-class-names/) plutôt 
que d'écrire des sélecteurs basés sur le type des éléments ou leur `id`.


### Noms de classes (BEM)
À compléter plus tard.


## Mobile d'abord (Mobile First)
Les règles sont d'abord écrites pour un affichage sur des appareils mobiles à écran étroit, puis, 
immédiatement après, on placera les alternatives (*media queries*) pour des écrans plus larges. 
Ainsi, les différentes alternatives pour un même élément sont toujours déclarées dans leur contexte. 

Exemple:
```css
.nav__liste {
        display: flex;
        flex-direction: row;
}
@media (min-width: 601px) {
    .nav__liste {
        flex-direction: column;
     }
}
```

-------------------------------------------------------------------------------

# Liste de contrôle 101 (pour TP long de Intégration I)

## Structure de répertoires et nomenclatures
- [ ] Les noms de dossier sont signifiants et n'ont pas de majuscules, d'espaces ou de caractères spéciaux
- [ ] Les noms de fichier sont signifiants et n'ont pas de majuscules, d'espaces ou de caractères spéciaux
- [ ] La page se nomme _index.html_ et se situe à la racine du site
- [ ] La nomenclature des fichiers est systématique
- [ ] La nomenclature des images est systématique (section associée, fonction, etc.)
- [ ] Tous les noms de classe sont signifiants et utilisent une nomenclature constante


## Favicon
- [ ] Le favicon est fonctionnel et intégré dans toutes les pages 
- [ ] Le favicon est signifiant et en lien avec le thème du site

---

## HTML 

### Contenu minimal de l'élément head 
- [ ] Doctype: La déclaration du type de document est présent 
- [ ] L'élément `html` inclut l'attribut `lang="fr"` (ou "en" si le texte est en anglais). 
- [ ] L'élément `charset` définit l'encodage du texte en UTF-8
- [ ] Les éléments `meta` (`description`, `keywords`, `author`) sont présents
- [ ] L'élément `meta` viewport est présent et complet 
- [ ] L'élément `title` est présent et placé après l'élément `charset` 
- [ ] Le contenu des éléments `title` est écrit sans faute
- [ ] L'élément `link` est bien utilisé pour relier la feuille de styles du document.

### Structure et sémantique
- [ ] Les éléments HTML sont utilisés en fonction de leur signification
- [ ] Le contenu HTML est écrit dans un ordre logique
- [ ] Les éléments de structure sont utilisés selon les règles
- [ ] `h1` est unique et décrit le thème de la page
- [ ] Les titres (`h1`, `h2`, `h3`, etc.) sont utilisés dans l'ordre et de manière pertinente

### Validité et lisibilité
- [ ] Les balises sont correctement imbriquées
- [ ] Le code HTML est valide selon le [Validateur HTML du w3c](https://validator.w3.org/)
- [ ] Le balisage est indenté correctement et régulièrement

### Hyperliens
- [ ] Les liens de la navigation principale sont tous fonctionnels  
- [ ] Les liens du contenu sont tous fonctionnels

### Images réactives
- [ ] Les images sont imbriquées dans picture (deux sources)

---
## Accessibilité

- [ ] Les éléments `a` contiennent du texte (libellé du lien) 
- [ ] Toutes les balises `img` ont un attribut `alt` avec un contenu pertinent

---

## CSS
- [ ] Les règles de styles sont consignées dans une seule feuille de style externe
- [ ] L'instruction __@charset "UTF-8";__ est placée sur la première ligne du fichier
- [ ] La feuille de style de réinitialisation précède l'ensemble des règles 
- [ ] La charte typo de base est présentée sous le sélecteur :root
- [ ] Les tailles de typo sont en em, rem ou vw
- [ ] La feuille de styles est valide selon https://jigsaw.w3.org/css-validator/

### Lisibilité
- [ ] La feuille de style est ordonnée en fonction des affinités et de la hiérarchie du contenu 
- [ ] La feuille de style est écrite lisiblement  
- [ ] La feuille de style est commentée
- [ ] Les polices importées de Google Fonts sont fonctionnelles

### Réactivité (_Responsive Web Design & Mobile First_)
- [ ] L'approche Mobile d'abord est utilisée
- [ ] La réactivité de la navigation principale est harmonieuse (horizontale à verticale)
- [ ] La réactivité de la zone de contenu des sections est harmonieuse (largeur du texte contrôlée) 
- [ ] La réactivité des images (images adaptées écran étroit vs large)
- [ ] Le ou les points de rupture sont judicieusement choisis en fonction de l'interface

### Contrôle de la mise en forme 
- [ ] L'ensemble du site comporte une identité visuelle personnalisée: couleurs, polices, etc.
- [ ] La hiérarchie visuelle des titres est cohérente
- [ ] Les images sont mis en forme de manière contrôlée 
- [ ] Les hyperliens de contenu sont mis en forme
- [ ] Les alignements sont consistants d'une section à l'autre

---

## Performance
- [ ] Taille et poids des images contrôlés

## Droits d'auteur
- [ ] Les sources des contenus sont indiquées

-------------------------------------------------------------------------------

# Liste de contrôle (version production)

Liste de bonnes pratiques et points à prendre en compte avant/durant/après l'élaboration d'un projet web.
___

## Intégration

|Critère|Priorité|
| ------------- | ------------- |
| Chaque page comporte un titre unique et pertinent (favorise le référencement et l’utilisabilité/accessibilité) | *** |
| Il y a un lien vers un flux RSS valide si un CMS est utilisé | * |
| Les préfixes navigateurs CSS sont gérés automatiquement (autoprefixer) | * |
| Un reset CSS est appliqué | * |
| Internet Explorer est géré en mode de compatibilité standard | * |
| Les balises HTML sont utilisées de manière sémantique | ** |
| Le média print est pris en compte pour les contenus imprimables | * |

## Webdesign

|Critère|Priorité|
| ------------- | ------------- |
| Le design est basé sur une grille de mise en page éprouvée pour le Web y compris pour le Responsive en mobile | ** |
| Les polices de fontes/tailles différentes sont limitées et lisibles | ** |

## Performance

|Critère|Priorité|
| ------------- | ------------- |
| Les scripts JavaScript sont chargés de manière non bloquante (les balises sont placées juste avant la fermeture du body) | * |
| Les fichiers CSS et JavaScript sont concaténés et minifiés (favorise la vitesse d'affichage) | ** |
| Les images sont optimisées et compressées (favorise la vitesse d'affichage) | * |
| Une page d'erreur 404 est présente | ** |
| Les performances front-end du site ont été vérifiées | * |
| Le nombre de web fonts est limité | * |

## Référencement

|Critère|Priorité|
| ------------- | ------------- |
| Chaque page comporte une section head avec des balises meta description et keywords et autres indications pertinentes | * |

## Accessibilité

|Critère|Priorité|
| ------------- | ------------- |
| Des liens d'évitement sont opérationnels | ** |
| Le contraste contenu / fond est suffisant | ** |
| Les contenus visuels ont des alternatives texte | ** |
| La langue des contenus est précisée (attribut lang) | * |
| Des tailles de polices fluides sont employées, le contenu est lisible avec un zoom texte à 200% | * |
| La hiérarchie des titres est correcte | ** |
| La navigation au clavier est possible | *** |
| Les formulaires sont accessibles | *** |
| Le site est utilisable sans CSS et/ou JavaScript et/ou sans images et/ou sans images de fond | ** |

## Projet

|Critère|Priorité|
| ------------- | ------------- |
| Le nom de domaine est fonctionnel | *** |
| Le projet est versionné (idéalement Git) | *** |
| La documentation est à jour | *** |
| Les permissions des fichiers en production sont correctes | ** |

## Qualité

|Critère|Priorité|
| ------------- | ------------- |
| Les liens internes sont valides | ** |
| Le site fait appel à des technologies open-source et interopérables | ** |
| Une icône favicon est présente à la racine du site | ** |
| La qualité du code HTML, CSS et JavaScript est vérifiée à l’aide d’outils automatiques (Exemple: ESLint) | ** |
| Les pages sont testées sur les navigateurs bureau et mobiles principaux | ** |
| L'orthographe et la grammaire sont vérifiées | * |

## Développement

|Critère|Priorité|
| ------------- | ------------- |
| Une nomenclature constante et internationale est adoptée | ** |
| L'indentation des fichiers est conventionnée (.editorconfig) | *** |

## Sécurité

|Critère|Priorité|
| ------------- | ------------- |
| Toutes les entrées utilisateur (formulaires, paramètres GET, etc) sont filtrées et validées côté serveur | *** |
| Le protocole HTTPS est utilisé avec un certificat valide | *** |
