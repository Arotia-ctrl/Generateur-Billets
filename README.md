# 🎟️ CHORALE LIVE – Générateur de billets de vote sur plaque

Application web autonome et hors-ligne (**100 % côté client, fichier HTML unique sans dépendance externe**) conçue pour concevoir, calibrer et générer en lot des planches A4 de billets de vote personnalisés avec codes-barres **Code 128**.

Elle permet notamment d'imprimer directement les données variables (numéro de candidat, nom, numéro de billet, code-barres) sur des plaques papier déjà pré-imprimées, ou de générer la planche complète prête à imprimer.

---

## ✨ Fonctionnalités principales

* **Gestion des candidats (`Candidats` & `Identifiants`)**
  * Attribution automatique d'identifiants uniques (`NUM`, ex. `C-01`) avec préfixe, séparateur et padding personnalisables.
  * Modification d'un candidat existant avec mise à jour automatique en cascade des billets déjà générés.
* **Éditeur visuel sur plaque (`Éditeur sur plaque`)**
  * Import d'une image de fond de plaque (JPG/PNG) avec réglage de l'opacité pour aligner précisément les champs.
  * Configuration de la grille A4 (Portrait ou Paysage, nombre de colonnes, rangées et marges en millimètres).
  * Ajout et positionnement d'éléments dynamiques dans le premier billet (répliqués automatiquement sur toute la planche) : `NUM`, `NOM` (retour à la ligne et ajustement automatique de la taille de police), `VOTE`, `NUM + VOTE`, `BARCODE` (Code 128 jeu B), `TEXTE` libre et `LIGNE` de découpe.
  * Déplacement à la souris, au clavier (flèches directionnelles), via un pavé de précision (pas de `0.2 mm` à `5 mm`), système de verrouillage (`🔒`) et historique d'annulation (`Ctrl+Z`).
* **Typographie intégrée & personnalisable**
  * Police **Montserrat Bold** embarquée en Base64 (WOFF) pour un rendu identique hors-ligne et lors de l'export PDF.
  * Possibilité d'importer n'importe quelle police personnalisée au format `.ttf`.
* **Génération PDF haute précision (`Génération`)**
  * Création de lots multi-candidats avec détection automatique des doublons et chevauchements de numéros.
  * Deux modes d'impression :
    * **Surimpression** : imprime uniquement les données variables sur vos planches pré-imprimées.
    * **Complet** : fusionne l'image de la plaque et les données sur papier blanc.
  * Outils de calibration imprimante : décalage fin en X/Y (mm) et ajustement d'échelle (%).
  * Génération native du fichier PDF en JavaScript pur (sans bibliothèque tierce).
* **Suivi, Export & Sauvegarde (`Historique` & `Sauvegarde`)**
  * Persistance automatique des données en local via **IndexedDB** (avec repli sur `localStorage`).
  * Journal complet des générations, annulation de billets individuels et export de la base au format **CSV**.
  * Export et restauration complète de l'espace de travail (image de plaque, gabarit, candidats et historique) au format **JSON**.

---

## 🚀 Installation et utilisation

Aucune installation, compilation ou serveur web n'est requis :

1. Téléchargez le fichier `index.html` (ou clonez ce dépôt).
2. Ouvrez simplement `index.html` dans n'importe quel navigateur web moderne (Chrome, Edge, Firefox, Safari).
3. Configurez vos règles d'identifiants, placez vos repères dans l'éditeur, puis lancez la génération PDF.

> 💡 **Conseil d'impression :** Lors de l'impression du PDF généré, veillez à régler l'échelle à **100 % (Taille réelle)** et à désactiver l'option *« Ajuster à la page »* afin de conserver les dimensions exactes en millimètres.

---

## 🛠️ Architecture technique

* **Langages :** HTML5, CSS3, JavaScript (ES6+ Vanilla).
* **Rendu vectoriel & PDF :** Manipulation dynamique du DOM **SVG**, conversion haute résolution via **Canvas API**, et encodage binaire d'un flux **PDF 1.4** natif intégrant les flux JPEG (`DCTDecode`).
* **Codes-barres :** Encodeur **Code 128 (Set B)** développé en JavaScript pur avec calcul de somme de contrôle modulo 103.
* **Stockage local :** Base de données **IndexedDB** (`chorale-live-v3`) couplée à un système de sauvegarde de secours dans `localStorage`.

---

## 📄 Licence

Ce projet est placé sous les termes de la **licence Apache 2.0**. Vous pouvez utiliser, modifier et distribuer ce logiciel librement, sous réserve de conserver les notices de copyright et de mentionner la licence d'origine. Consultez le fichier [LICENSE](LICENSE) pour plus de détails.
