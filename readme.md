# Les Media Queries et Container Queries : Maîtriser le Responsive Design Moderne

## 📚 Lexique des Termes Essentiels

**Media Query**
Règle CSS permettant d'appliquer des styles en fonction des caractéristiques du *dispositif* (viewport, orientation, résolution).
**C'est une question posée au navigateur : "Quelle est la taille de l'écran ?"**

**Container Query**
Règle CSS permettant d'appliquer des styles en fonction des dimensions d'un *élément conteneur parent* spécifique, plutôt que de l'écran entier.
**On demande : "Quelle est la taille de mon conteneur ?"**

**Viewport**  
Zone visible de la page web dans le navigateur. 
Sa taille varie selon l'appareil (mobile, tablette, desktop).

**Breakpoint**  
Point de rupture : seuil de largeur où le design change
(ex : passage de mobile à tablette à 768px).

**Container**  
Élément HTML défini comme contexte de référence pour les container queries.
*Il devient le point de mesure pour ses enfants.*

**Responsive Design**  
Approche de conception où l'interface s'adapte automatiquement aux différentes tailles d'écran.
_Tel de l'eau qui s'adapterai selon différents récipients._

[**Progressive Enhancement**](#progressive-enhancement-et-responsive-design--le-lien-intrins%C3%A8que)
Philosophie de développement web consistant à construire une expérience de base fonctionnelle pour tous les utilisateurs, puis à ajouter progressivement des couches d'amélioration pour les navigateurs et appareils plus capables.
On part du *minimum viable* et *on enrichit l'expérience*

**Mobile-First**
Approche de conception commençant par l'expérience mobile (la plus contrainte), puis enrichissant pour les écrans plus grands. 
C'est une application concrète du **Progressive Enhancement** dans le responsive design.
