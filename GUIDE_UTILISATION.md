# Guide d'Utilisation — all-search.ulp (Recherche Globale de Schématique EAGLE)

![Couverture all-search-ulp](all_search_cover.png)

Ce script ULP (User Language Program) permet d'effectuer une recherche textuelle multicritère sur l'ensemble des feuilles d'un schéma Autodesk EAGLE (compatible avec la version 8.0.1 et supérieures).

---

## Sommaire
1. [Fonctionnalités](#fonctionnalités)
2. [Installation](#installation)
3. [Mode d'Emploi](#mode-demploi)
4. [Raccourci Clavier (Recommandé)](#raccourci-clavier-recommandé)
5. [Foire Aux Questions (Q&A / FAQ)](#foire-aux-questions-qa--faq)

---

## Fonctionnalités

Le script parcourt de manière récursive toutes les pages (sheets) de votre schéma et recherche les éléments correspondant à vos critères :
*   **Composants (Parts)** : Recherche par nom (ex: `R1`), par valeur (ex: `10k`), par type de boîtier/device (ex: `R0805`), ou au sein de n'importe quel attribut personnalisé (ex: `FABRICANT`, `BOM_PN`).
*   **Signaux / Nets** : Recherche parmi les noms de pistes ou équipotentielles du schéma.
*   **Broches (Pins)** : Recherche de broches de composants spécifiques (ex: recherche de `CLK` renverra `U1.CLK`, `U2.CLK`, etc.).
*   **Textes** : Recherche au sein des blocs de texte indépendants posés manuellement sur les feuilles du schéma.

---

## Installation

1.  Téléchargez ou copiez le fichier `all-search.ulp`.
2.  Placez le fichier dans l'un des répertoires suivants :
    *   Le sous-dossier `ulp/` de votre installation d'EAGLE (ex: `C:\EAGLE-8.0.1\ulp\`).
    *   Ou le dossier de votre projet actif (ex: `c:\Users\ytxs\Documents\Antigrav\ulp_search\`).

---

## Mode d'Emploi

### 1. Lancement
*   Dans l'éditeur de schéma EAGLE, saisissez la commande suivante dans la console (ou utilisez le menu ULP de l'interface) :
    ```text
    RUN all-search.ulp
    ```
    *(Si le script est dans un dossier personnalisé, spécifiez le chemin complet, ex: `RUN "c:\chemin\vers\all-search.ulp"`).*

### 2. Configuration de la recherche
*   **Saisie de la requête** : Tapez votre terme de recherche dans le champ **Search Query**.
*   **Filtres de catégories** : Cochez/décochez les cases (Parts, Nets, Texts, Pins) pour limiter les résultats.
*   **Options de correspondance** :
    *   *Case Sensitive* : Différencie les majuscules des minuscules.
    *   *Exact Match* : Cherche une correspondance exacte au lieu d'une portion de texte (sous-chaîne).
*   Cliquez sur le bouton **Search** (ou appuyez sur la touche `Entrée`) pour actualiser les résultats.

### 3. Navigation vers un résultat
*   La liste affiche le numéro de la feuille, le type d'élément, le nom et un aperçu de la valeur ou du texte.
*   Pour afficher un élément dans le schéma :
    *   **Double-cliquez** sur la ligne correspondante dans la liste.
    *   Ou sélectionnez la ligne et cliquez sur **Go to / Show**.
*   Le script fermera automatiquement la fenêtre de recherche, se positionnera sur la feuille concernée, effectuera un zoom automatique sur l'élément et le mettra en surbrillance (commande `SHOW`).

---

## Raccourci Clavier (Recommandé)

Pour ouvrir instantanément la boîte de recherche à l'aide de la combinaison de touches `Ctrl` + `F`, tapez la commande suivante dans la console de commande d'EAGLE :

```text
ASSIGN C+F 'RUN "c:\Users\ytxs\Documents\Antigrav\ulp_search\all-search.ulp"';
```

*(Pensez à adapter le chemin absolu du fichier `.ulp` selon votre dossier d'installation).*

---

## Foire Aux Questions (Q&A / FAQ)

#### Q : Pourquoi la fenêtre de recherche se ferme-t-elle lorsque je double-clique sur un résultat ?
**R** : Les boîtes de dialogue des scripts ULP dans EAGLE sont modales et bloquent l'interface utilisateur générale du logiciel. Pour qu'EAGLE puisse exécuter la commande de changement de page (`EDIT`), de zoom (`WINDOW`) et de surbrillance (`SHOW`), le script ULP doit impérativement se terminer. Vous pouvez rouvrir la recherche instantanément en utilisant le raccourci `Ctrl` + `F` configuré ci-dessus.

#### Q : Le zoom automatique est-il trop serré ou mal cadré ?
**R** : Le script calcule automatiquement une boîte de délimitation (bounding box) de sécurité autour des objets. Pour les composants et les broches, il utilise la géométrie du symbole. Pour les signaux (nets) ou les textes courts, il applique une marge minimale de 10 mm pour éviter un zoom excessif.

#### Q : La commande `SHOW` affiche une erreur lors de la sélection d'un texte brut. Est-ce normal ?
**R** : Oui. Dans EAGLE, la commande `SHOW` fonctionne uniquement sur les objets physiques du schéma (composants, signaux, bus, broches). Le texte brut indépendant n'étant pas un composant nommé, EAGLE ne peut pas le cibler avec `SHOW`. Pour le texte brut, le script effectue uniquement le changement de feuille et le zoom/recentrage précis sur ses coordonnées de placement.

#### Q : Est-il possible de chercher dans les attributs personnalisés comme les références distributeurs (Digi-Key, Mouser, etc.) ?
**R** : Oui, tout à fait. Si la catégorie **Parts** est activée, le script parcourt l'intégralité des paires Nom/Valeur de tous les attributs définis sur les composants du schéma.

#### Q : Le script fonctionne-t-il sur les schémas de très grande taille avec des dizaines de pages ?
**R** : Oui. Le parcours de l'arbre d'objets en mémoire est extrêmement rapide et optimisé. Les performances restent fluides même sur des projets industriels de grande envergure.
