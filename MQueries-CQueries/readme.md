# Les Media Queries et Container Queries : Maîtriser le Responsive Design Moderne

## 📚 Lexique des Termes Essentiels

**Media Query**
Règle CSS permettant d'appliquer des styles en fonction des caractéristiques du *dispositif* (viewport, orientation, résolution).
**C'est une question posée au navigateur : "Quelle est la taille de l'écran ?"**

**Container Query**
Règle CSS permettant d'appliquer des styles en fonction des dimensions d'un *élément conteneur parent* spécifique, plutôt que de l'écran entier.
**On demande : "Quelle est la taille de mon conteneur ?"**

**Viewport**  
Zone visible de la page web dans le navigateur. Sa taille varie selon l'appareil (mobile, tablette, desktop).

**Breakpoint**  
Point de rupture : seuil de largeur où le design change
(ex : passage de mobile à tablette à 768px).

**Container**  
Élément HTML défini comme contexte de référence pour les container queries.
*Il devient le point de mesure pour ses enfants.*

**Responsive Design**  
Approche de conception où l'interface s'adapte automatiquement aux différentes tailles d'écran.
Tel de l'eau qui s'adapterai selon différents récipients.

[**Progressive Enhancement**](#progressive-enhancement-et-responsive-design--le-lien-intrins%C3%A8que)
Philosophie de développement web consistant à construire une expérience de base fonctionnelle pour tous les utilisateurs, puis à ajouter progressivement des couches d'amélioration pour les navigateurs et appareils plus capables. 
On part du *minimum viable* et *on enrichit l'expérience*

**Mobile-First**
Approche de conception commençant par l'expérience mobile (la plus contrainte), puis enrichissant pour les écrans plus grands. C'est une application concrète du **Progressive Enhancement** dans le responsive design.

---

## Comprendre la Différence Fondamentale

Imaginez que vous construisez des meubles modulables :

**Media Queries** = Adapter les meubles selon la *taille de la pièce*
Vous réorganisez tout votre salon différemment selon que vous êtes dans un studio ou une grande maison.

**Container Queries** = Adapter les meubles selon *l'espace disponible dans le meuble lui-même*
Votre étagère modulable réorganise ses compartiments selon sa propre largeur, peu importe la taille de la pièce.

---

## Documentation Officielle

🔗 **Media Queries** : [MDN Web Docs - Media Queries](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_media_queries/Using_media_queries)

🔗 **Container Queries** : [MDN Web Docs - Container Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_containment/Container_queries)

🔗 **Guide Complet Responsive** : [web.dev - Responsive Design](https://web.dev/responsive-web-design-basics/)

🔗 **Media Queries sur Alsacreation** : [Les Media Queries CSS3](https://www.alsacreations.com/article/lire/930-css3-media-queries.html)

🔗 **Les Container Queries en CSS sur Alsacreation** : [Les Container Queries en CSS](https://www.alsacreations.com/article/lire/1915-Les-Container-Queries-en-CSS.html)

---

## Partie 1 : Les Media Queries - L'Approche Classique

### Le Principe de Base

Les media queries interrogent les caractéristiques du **dispositif d'affichage global**, l'écran du navigateur.
Elles permettent de créer des points de rupture où votre design entier se réorganise.

### Exemple Commenté - Carte de Produit Responsive

```css
/* 
ÉTAPE 1 : Styles de base (Mobile First)
On commence par définir les styles pour les petits écrans
Cette approche est appelée "Mobile First" car on part du plus petit écran
*/
.product-card {
  /* La carte occupe toute la largeur disponible sur mobile */
  width: 100%;
  
  /* Espacement interne confortable pour le tactile */
  padding: 16px;
  
  /* Bordure légère pour délimiter la carte */
  border: 1px solid #e0e0e0;
  
  /* Coins arrondis pour un aspect moderne */
  border-radius: 8px;
  
  /* Ombre subtile pour donner de la profondeur */
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.product-card__image {
  /* L'image prend toute la largeur sur mobile */
  width: 100%;
  
  /* Hauteur fixe pour maintenir la cohérence visuelle */
  height: 200px;
  
  /* L'image couvre tout l'espace sans déformation */
  object-fit: cover;
  
  /* Arrondi uniquement en haut pour suivre la carte */
  border-radius: 8px 8px 0 0;
}

.product-card__content {
  /* Espacement entre l'image et le contenu */
  margin-top: 12px;
}

.product-card__title {
  /* Taille de police lisible sur mobile */
  font-size: 18px;
  
  /* Espacement en bas du titre */
  margin-bottom: 8px;
  
  /* Poids de police pour hiérarchie visuelle */
  font-weight: 600;
}

/* 
ÉTAPE 2 : Adaptation pour Tablettes (≥ 768px)
@media = "si la condition suivante est vraie"
min-width: 768px = "largeur minimale de 768 pixels"
Donc : "Si l'écran fait AU MOINS 768px de large"
*/
@media (min-width: 768px) {
  /* 
  Sur tablette, on peut afficher 2 cartes côte à côte
  calc() permet de calculer dynamiquement la largeur
  50% de la largeur - 16px d'espacement entre les cartes
  */
  .product-card {
    width: calc(50% - 16px);
  }
  
  /* Image légèrement plus haute sur tablette */
  .product-card__image {
    height: 250px;
  }
  
  /* Titre plus grand car plus d'espace disponible */
  .product-card__title {
    font-size: 20px;
  }
}

/* 
ÉTAPE 3 : Adaptation pour Desktop (≥ 1024px)
Même logique mais pour les grands écrans
*/
@media (min-width: 1024px) {
  /* 
  Sur desktop, 3 cartes côte à côte
  33.333% = un tiers de la largeur
  Moins 24px pour les espacements entre 3 éléments
  */
  .product-card {
    width: calc(33.333% - 24px);
  }
  
  /* Image encore plus haute sur grand écran */
  .product-card__image {
    height: 300px;
  }
  
  /* Titre au maximum de lisibilité */
  .product-card__title {
    font-size: 22px;
  }
  
  /* 
  Effet au survol uniquement sur desktop
  Car le survol n'existe pas sur tactile
  */
  .product-card:hover {
    /* Ombre plus prononcée au survol */
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    
    /* Légère élévation avec transformation */
    transform: translateY(-4px);
    
    /* Animation fluide de la transformation */
    transition: all 0.3s ease;
  }
}

/* 
ÉTAPE 4 : Media Query pour l'orientation
Utile pour les tablettes qui peuvent pivoter
*/
@media (orientation: landscape) and (max-width: 1023px) {
  /* 
  En mode paysage sur tablette, on peut afficher 3 cartes
  même si l'écran n'atteint pas 1024px de large
  */
  .product-card {
    width: calc(33.333% - 20px);
  }
}
```

### Pourquoi cette approche ?

Les media queries fonctionnent parfaitement quand vous voulez adapter **l'ensemble de votre layout** aux dimensions de l'écran. C'est l'outil *historique* du responsive design, fiable et universellement supporté.

**Limites identifiées**
Si votre carte est placée dans une sidebar étroite sur desktop, elle gardera le style "desktop" (33.333% de largeur) même si son conteneur est petit. 
La carte ne "voit" que la taille de l'écran, pas son contexte réel.

---

## Partie 2 : Les Container Queries - L'Approche Moderne

### Le Principe Révolutionnaire

Les container queries permettent aux composants de s'adapter à **leur propre espace disponible**, indépendamment de la taille de l'écran.
> C'est le chaînon manquant du CSS moderne !

### Exemple Commenté - Composant Vraiment Réutilisable

```css
/* 
ÉTAPE 1 : Définir le conteneur
C'est LA nouveauté : on déclare quel élément servira de référence
*/
.card-container {
  /* 
  container-type définit le type de surveillance
  inline-size = surveiller la largeur du conteneur
  (inline-size car on surveille l'axe horizontal)
  */
  container-type: inline-size;
  
  /* 
  container-name donne un nom au conteneur
  Permet de cibler spécifiquement ce conteneur dans les queries
  Optionnel mais recommandé pour la clarté
  */
  container-name: card-wrapper;
}

/* 
ÉTAPE 2 : Styles de base du composant
Ces styles s'appliquent TOUJOURS, quelle que soit la taille
*/
.adaptive-card {
  /* Padding confortable */
  padding: 16px;
  
  /* Bordure et coins arrondis */
  border: 1px solid #ddd;
  border-radius: 12px;
  
  /* Couleur de fond */
  background: white;
  
  /* 
  Par défaut, disposition verticale (colonne)
  Image au-dessus, texte en dessous
  */
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.adaptive-card__image {
  /* Image responsive par défaut */
  width: 100%;
  height: 180px;
  object-fit: cover;
  border-radius: 8px;
}

.adaptive-card__title {
  font-size: 16px;
  font-weight: 600;
  line-height: 1.4;
}

.adaptive-card__description {
  font-size: 14px;
  color: #666;
  line-height: 1.6;
}

/* 
ÉTAPE 3 : Container Query pour taille moyenne
@container = "si le conteneur parent répond à cette condition"
(min-width: 400px) = "si le conteneur fait au moins 400px"
*/
@container card-wrapper (min-width: 400px) {
  /* 
  Quand le conteneur dépasse 400px, on passe en disposition horizontale
  L'image à gauche, le contenu à droite
  */
  .adaptive-card {
    flex-direction: row;
    align-items: center;
  }
  
  /* 
  L'image occupe maintenant 40% de la largeur
  Et non plus 100% comme en version verticale
  */
  .adaptive-card__image {
    width: 40%;
    height: 200px;
    /* 
    flex-shrink: 0 empêche l'image de rétrécir
    si le texte est long
    */
    flex-shrink: 0;
  }
  
  /* Le contenu occupe l'espace restant */
  .adaptive-card__content {
    flex: 1;
  }
  
  /* Texte plus grand avec plus d'espace */
  .adaptive-card__title {
    font-size: 18px;
  }
  
  .adaptive-card__description {
    font-size: 15px;
  }
}

/* 
ÉTAPE 4 : Container Query pour grande taille
Quand le conteneur dépasse 600px
*/
@container card-wrapper (min-width: 600px) {
  .adaptive-card {
    /* Padding plus généreux */
    padding: 24px;
  }
  
  /* Image encore plus grande */
  .adaptive-card__image {
    width: 45%;
    height: 250px;
  }
  
  /* Typographie optimisée pour grand espace */
  .adaptive-card__title {
    font-size: 22px;
    margin-bottom: 8px;
  }
  
  .adaptive-card__description {
    font-size: 16px;
  }
  
  /* 
  On peut ajouter des éléments qui n'apparaissent
  que quand il y a assez d'espace
  */
  .adaptive-card__metadata {
    display: flex;
    gap: 16px;
    margin-top: 12px;
    font-size: 14px;
    color: #888;
  }
}

/* 
ÉTAPE 5 : Combiner container queries et unités de conteneur
cqw = Container Query Width (largeur du conteneur en %)
1cqw = 1% de la largeur du conteneur
*/
@container card-wrapper (min-width: 500px) {
  .adaptive-card__title {
    /* 
    La taille de police s'adapte fluidement
    entre 18px et 24px selon la largeur du conteneur
    clamp(min, préféré, max)
    */
    font-size: clamp(18px, 4cqw, 24px);
  }
}
```

### HTML correspondant pour comprendre

```html
<!-- 
Exemple 1 : Dans une colonne principale large
Le conteneur fait environ 800px sur desktop
La carte utilisera le style @container (min-width: 600px)
-->
<div class="main-content">
  <div class="card-container">
    <article class="adaptive-card">
      <img src="product.jpg" class="adaptive-card__image" alt="Produit">
      <div class="adaptive-card__content">
        <h3 class="adaptive-card__title">Titre du produit</h3>
        <p class="adaptive-card__description">Description détaillée...</p>
        <div class="adaptive-card__metadata">
          <span>Prix : 29€</span>
          <span>En stock</span>
        </div>
      </div>
    </article>
  </div>
</div>

<!-- 
Exemple 2 : Dans une sidebar étroite
Le conteneur fait environ 300px
La carte utilisera le style de base (vertical)
MÊME SI nous sommes sur un écran desktop de 1920px !
-->
<aside class="sidebar">
  <div class="card-container">
    <article class="adaptive-card">
      <img src="product.jpg" class="adaptive-card__image" alt="Produit">
      <div class="adaptive-card__content">
        <h3 class="adaptive-card__title">Titre du produit</h3>
        <p class="adaptive-card__description">Description...</p>
      </div>
    </article>
  </div>
</aside>
```

---

## Tableau Comparatif : Quand Utiliser Quoi ?

| Critère | Media Queries | Container Queries |
|---------|-----------------|---------------------|
| **Question posée** | "Quelle taille fait l'écran ?" | "Quelle taille fait mon conteneur ?" |
| **Utilisation idéale** | Layout global, grilles principales, navigation | Composants réutilisables, widgets, cartes |
| **Réutilisabilité** | Faible (dépend du contexte écran) | Élevée (s'adapte automatiquement) |
| **Support navigateurs** | Excellent (100%) ✅ | Bon (95%+ depuis 2023) ✅ |
| **Performance** | Excellent | Excellent |
| **Complexité** | Simple à comprendre | Nécessite de définir des conteneurs |

---

## Cas Pratique : Combinons les Deux

La vraie puissance vient de la **combinaison** des deux approches :

```css
/* 
STRATÉGIE HYBRIDE COMPLÈTE
Utiliser les deux pour un résultat optimal
*/

/* 1️⃣ Media Query pour le layout global */
@media (min-width: 1024px) {
  .page-layout {
    /* Grille à 2 colonnes sur desktop */
    display: grid;
    grid-template-columns: 300px 1fr;
    gap: 32px;
  }
  
  .sidebar {
    /* Sidebar fixe de 300px */
    width: 300px;
  }
  
  .main-content {
    /* Contenu principal prend l'espace restant */
    flex: 1;
  }
}

/* 2️⃣ Container Query pour les composants */
.card-container {
  container-type: inline-size;
}

@container (min-width: 400px) {
  /* 
  Peu importe si cette carte est dans :
  - La sidebar (300px) → reste vertical ❌
  - Le contenu principal (700px) → passe horizontal ✅
  Le composant décide selon SON espace !
  */
  .adaptive-card {
    flex-direction: row;
  }
}
```

---

## Exercice Progressif pour Maîtriser

### Niveau 1️⃣ : Media Query Simple

Créez une grille de cartes qui passe de 1 colonne (mobile) à 2 (tablette) à 3 (desktop).

### Niveau 2️⃣ : Container Query Basique  

Créez une carte qui passe de vertical à horizontal quand son conteneur dépasse 400px.

### Niveau 3️⃣ : Combinaison

Créez un dashboard avec une sidebar contenant des mini-cartes et un contenu principal avec des grandes cartes, où chaque type de carte s'adapte à son propre contexte.

---

aller plus loin dans la compréhension du concept de *Progressive Enhancement* appliqué au responsive design.

### Progressive Enhancement et Responsive Design : Le Lien Intrinsèque

Dans le contexte du responsive design avec media queries et container queries, Progressive Enhancement se traduit par une approche Mobile-First structurée en couches.

```text
┌─────────────────────────────────────────┐
│  COUCHE 3: Desktop Enhancement          │  ← Expérience optimale
│  • Container queries                    │
│  • Animations complexes                 │
│  • Interactions avancées (hover)        │
├─────────────────────────────────────────┤
│  COUCHE 2: Tablette & Medium Screens    │  ← Amélioration intermédiaire
│  • Layout multi-colonnes                │
│  • Media queries standard               │
│  • Images optimisées                    │
├─────────────────────────────────────────┤
│  COUCHE 1: Mobile Base (FONDATION)      │  ← Expérience universelle
│  • HTML sémantique                      │
│  • CSS de base                          │
│  • Contenu accessible                   │
│  • Fonctionnement sans JavaScript       │
└─────────────────────────────────────────┘
```

---

## 🌟 Points Clés à Retenir

✅ **Media Queries** = Pour les décisions de layout global basées sur l'écran, Viewport.
✅ **Container Queries** = Pour les composants autonomes qui s'adaptent à leur contexte (*@container*).
✅ **Mobile First** = Commencer par les petits écrans puis cibler les plus grandes dimmension d'écran.  
✅ **Combinaison** = La vraie puissance vient d'utiliser les deux ensemble.
✅ **Container-type** = Toujours déclarer le conteneur parent avant d'utiliser *@container*.  

> Avec ces deux outils complémentaires, vous pouvez créer des interfaces véritablement adaptatives et des composants réellement réutilisables !

*Happy Coding !*
