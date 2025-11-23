
# Cahier de Suivi Personnel - MELONG LETHYCIA

# TP N°2 : OPTIMISATION NUMERIQUE SANS CONTRAINTES : Descente de Gradient (Fonction Quadratique $f(x, y) = x^2 - y^2$)

##  Informations


- **Nom** : MELONG LETHYCIA
- **Projet** : TP N°2 : OPTIMISATION NUMERIQUE SANS CONTRAINTES
- **Encadrant** : Pr. MELATAGIA Paulin 
- **Période** : 21/11/2025 - 23/11/2025


---



##  Objectifs du Projet

L'objectif principal de ce travail pratique était d'implémenter et de comparer deux variantes fondamentales de l'algorithme de descente de gradient sur une fonction quadratique spécifique, $f(x, y) = x^2 - y^2$.

* **Implémentation** : Développer un code Python fonctionnel utilisant la bibliothèque `SymPy` pour :
    * Calculer le gradient symboliquement.
    * Implémenter la descente de gradient à **pas fixe** ($\alpha$ constant).
    * Implémenter la descente de gradient à **pas optimal** (calculé analytiquement pour les fonctions quadratiques).
* **Analyse de Convergence** : Étudier et documenter le comportement de chaque algorithme, notamment autour du **point selle** $(0, 0)$.
* **Visualisation** : Représenter les lignes de niveau de la fonction et tracer les trajectoires des algorithmes pour divers pas fixes et pour le pas optimal.
* **Analyse du Pas Fixe** : Déterminer l'impact du choix du pas ($\alpha$) sur le nombre d'itérations et la convergence/divergence (en lien avec les valeurs propres de la Hessienne).

---

## ✅ Travail Réalisé

| Section | Description | Statut |
| :--- | :--- | :--- |
| **Fonction & Gradient** | Définition de $f(x, y) = x^2 - y^2$ et calcul du gradient $\nabla f(x, y) = (2x, -2y)$ avec `SymPy`. | Fait |
| **Algorithme Pas Fixe** | Implémentation de la descente de gradient avec différents pas ($\alpha = 0.005, 0.2, 0.49, 0.51$). | Fait |
| **Algorithme Pas Optimal** | Implémentation du calcul analytique du pas optimal $s_k = \frac{||\mathbf{g}_k||^2}{\mathbf{g}_k^T \nabla^2 f(\mathbf{x}_k) \mathbf{g}_k}$. | Fait |
| **Suivi des Itérations** | Génération du tableau détaillé pour l'algorithme à pas optimal (valeur de $f$, norme du gradient, pas $s_k$, coordonnées $x_k, y_k$). | Fait |
| **Visualisation** | Tracé des lignes de niveau (hyperboles) et des trajectoires pour $\mathbf{x}_0=(7, 1.5)$, comparant le pas fixe et le pas optimal. | Fait |
| **Tableau Récapitulatif** | Création du tableau comparatif du nombre d'itérations en fonction du pas fixe. | Fait |

---

##  Difficultés Rencontrées et Solutions

| Difficulté | Description détaillée | Solution Appliquée |
| :--- | :--- | :--- |
| **Instabilité du Pas Optimal** | La fonction $f(x, y)$ étant non-convexe (point selle), le dénominateur du pas optimal ($\mathbf{g}_k^T \nabla^2 f \mathbf{g}_k$) pouvait devenir **nul ou négatif**, provoquant une division par zéro ou une divergence extrême. | Ajout d'une **clause de garde** (`if abs(g_T_A_g) < 1e-12 or g_T_A_g < 0`) dans l'implémentation pour basculer sur un petit pas fixe ($s_k=0.01$) afin de continuer l'itération ou de stopper. |
| **Visualisation et Échelle** | Lors du tracé, les trajectoires divergentes (ou les premières itérations rapides) étiraient l'axe du graphique, ce qui **effaçait** les détails des lignes de niveau autour de l'origine. | Utilisation explicite des fonctions `plt.xlim()` et `plt.ylim()` pour **limiter la fenêtre de visualisation** à une zone pertinente (e.g., $[-2, 2]$ ou $[-3, 8]$) et s'assurer que les lignes de niveau restent visibles. |
| **Compréhension du Point Selle** | Interprétation des résultats : pourquoi l'algorithme converge-t-il vers l'origine alors que ce n'est pas un minimum ? | Reconnaissance que la convergence vers $(0, 0)$ est un **piège** mathématique et que la descente de gradient est fondamentalement **inefficace** ou **instable** sur les points selles. La convergence observée est souvent le résultat d'un pas optimal qui "saute" vers l'origine accidentellement. |

---

##  Compétences Développées

* **Calcul Symbolique et Numérique** : Maîtrise de l'utilisation de `SymPy` pour la dérivation symbolique et de `sp.lambdify` pour la conversion en fonctions numériques optimisées (`numpy`).
* **Algorithmes d'Optimisation** : Compréhension approfondie et implémentation pratique des deux types de descente de gradient (pas fixe et pas optimal).
* **Analyse de la Non-Convexité** : Capacité à identifier les problèmes posés par un point selle sur les algorithmes d'optimisation (instabilité du pas optimal).
* **Visualisation Scientifique** : Utilisation de `Matplotlib` pour représenter graphiquement la topographie d'une fonction multivariable (lignes de niveau) et le chemin d'un algorithme (trajectoires).
* **Diagnostic d'Erreur** : Capacité à identifier les causes d'une divergence ou d'un comportement inattendu lié au choix du pas ou à la structure de la fonction.

---

##  Réflexion Personnelle (Ce que j'ai appris)

Ce TP a mis en évidence le rôle crucial de la **convexité** en optimisation. J'ai compris que la descente de gradient est un outil puissant pour les fonctions convexes, mais qu'elle est extrêmement fragile face aux **points selles** ou aux régions non-convexes.

### J'ai appris que :

1.  **Le Pas Optimal n'est pas Toujours la Meilleure Solution** : Bien qu'analytiquement optimal pour la direction actuelle, le pas optimal peut être catastrophique si le Hessien n'est pas défini positif (cas du point selle $f(x, y) = x^2 - y^2$), menant à une division par zéro ou un pas négatif qui rend l'algorithme inutilement complexe ou divergent.
2.  **L'Importance de $\alpha$** : Le choix d'un pas fixe est un compromis délicat. Si $\alpha$ est trop petit (e.g., 0.005), la convergence est excessivement lente. S'il est trop grand (e.g., 0.51), l'algorithme diverge. La limite théorique $\alpha < 2/\lambda_{max}$ (où $\lambda_{max}=2$) est bien vérifiée par l'observation de la divergence pour $\alpha=0.51$.
3.  **Visualisation = Compréhension** : Tracer les trajectoires sur les lignes de niveau est essentiel. C'est la seule façon de voir concrètement l'**oscillation** de l'algorithme de descente de gradient lorsque le pas est trop grand (pas fixe) ou les **sauts** dramatiques du pas optimal.
