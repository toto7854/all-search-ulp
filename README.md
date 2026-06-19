# EAGLE Schematic Search ULP (v1.0.0)

![Couverture all-search-ulp](all_search_cover.png)

Un script ULP (User Language Program) performant pour Autodesk EAGLE, conçu pour rechercher des composants, des équipotentielles (nets), des broches (pins) et des étiquettes de texte manuel à travers toutes les pages d'un schéma.

***Pour un guide d'utilisation plus détaillé et une foire aux questions (FAQ), consultez le [GUIDE_UTILISATION.md](GUIDE_UTILISATION.md).***

---

## Fonctionnalités

*   **Parcours multi-feuilles** : Analyse automatique de toutes les pages/feuilles du schéma actif.
*   **Recherche multi-catégories** :
    *   **Composants (Parts)** : Correspondance avec les désignations (ex: `R1`), les valeurs (ex: `10k`), le type de boîtier/device, et les attributs personnalisés.
    *   **Nets** : Correspondance avec les noms de signaux et équipotentielles (ex: `VCC`, `GND`).
    *   **Broches (Pins)** : Correspondance avec les connexions spécifiques des composants (ex: `U1.CLK`).
    *   **Textes** : Correspondance avec les blocs de texte saisis manuellement sur le schéma.
*   **Filtres de correspondance** : Supporte les modes **Sensibilité à la casse** (Case Sensitive) et **Correspondance exacte** (Exact Match).
*   **Interface dynamique** : Met à jour la liste des résultats lors de la frappe sans recharger la boîte de dialogue.
*   **Zoom & Surlignage automatiques** : Double-cliquer sur un résultat bascule l'éditeur sur la bonne feuille, centre et zoome sur l'élément, et le met en surbrillance avec la commande `SHOW` (gère des marges de sécurité sur les petits éléments pour un affichage propre).

---

## Installation

1.  Téléchargez ce dépôt.
2.  Copiez le fichier [all-search.ulp](all-search.ulp) dans :
    *   Le dossier `ulp/` de votre installation d'Autodesk EAGLE.
    *   **OU** directement dans le dossier de votre projet actif.

---

## Utilisation

1.  Dans la console de l'éditeur de schéma d'EAGLE, lancez :
    ```text
    RUN all-search.ulp
    ```
    *(Si le fichier est dans un dossier spécifique, utilisez le chemin complet, ex : `RUN "C:\chemin\vers\all-search.ulp"`).*
2.  Saisissez votre recherche dans la barre de saisie et appuyez sur **Entrée** ou cliquez sur le bouton **Search**.
3.  Double-cliquez sur un élément de la liste pour naviguer vers sa position sur le schéma.

---

## Recommandé : Associer à `Ctrl` + `F`

Vous pouvez associer ce script de recherche au raccourci standard `Ctrl` + `F`. Pour cela, lancez la commande suivante dans la console d'EAGLE :

```text
ASSIGN C+F 'RUN "C:\chemin\vers\all-search.ulp"';
```

---

## Licence

Ce projet est sous licence MIT - voir le fichier [LICENSE](LICENSE) pour plus de détails.
