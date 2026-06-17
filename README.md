# Poster-Stage

Poster HTML/CSS interactif présentant le bilan de stage d'Arthur Duret chez **Airbus Helicopters** (équipe ETRV, mission via SOREAM) : préparation de données LiDAR et vidéo pour l'entraînement de modèles IA de détection d'obstacles (câbles, pylônes) en vol à basse altitude.

## Aperçu

Le poster est une page web statique, en une seule pièce (`index.html` + `styles.css`, aucune dépendance JS externe hormis les polices/icônes via CDN), organisée en 12 cartes :

1. Présentation Airbus Helicopters & périmètre ETRV
2. Contexte, enjeux et politiques entreprise
3. Définition de la mission
4. Pipeline d'entraînement IA (schéma SVG)
5. Planning réel (Gantt 12 semaines)
6. Détail des phases
7. Méthodes & choix techniques
8. Visuels (placeholders à remplacer par des captures réelles)
9. Bilan objectifs vs résultats
10. Difficultés rencontrées & solutions
11. Impact & projection professionnelle
12. Démonstration clé (démo armée) et conclusion

Chaque carte est cliquable et s'ouvre en plein écran (overlay zoom), navigable au clavier (flèches / espace / Échap).

## Structure du projet

```
.
├── index.html   # contenu et structure du poster
├── styles.css   # thème visuel (dark, accents bleu/cyan), grille des cartes, overlay
└── README.md
```

## Utilisation

Ouvrir simplement `index.html` dans un navigateur (pas de serveur ni de build nécessaire) :

```bash
open index.html        # macOS
xdg-open index.html    # Linux
```

Ou servir le dossier avec un serveur statique si besoin (ex. `python3 -m http.server`).

### Personnalisation

- **Logos** : remplacer `airbus-logo-blanc.png`, `soream-logo-blanc.png`, `cesi-logo-blanc.png` à la racine du projet. Si une image est absente, un fallback texte stylé s'affiche automatiquement (`onerror`).
- **Visuels (carte 7)** : les `<img class="visual-img" src="">` sont des emplacements vides volontaires — renseigner `src` avec vos captures (nuage de points, annotation, interface de l'outil). Le placeholder visuel disparaît automatiquement dès qu'une image se charge correctement.
- **Couleurs / thème** : toutes les couleurs sont centralisées dans les variables CSS `:root` en haut de `styles.css`.

## Revue de code

Le code a été relu et un correctif appliqué :

- **Corrigé** — une `</div>` surnuméraire dans une cellule du tableau Gantt (ligne « Perfectionnement outil + annotation ») cassait localement l'imbrication des balises ; la structure est maintenant équilibrée (vérifié : nombre de `<div>` ouverts = fermés).

Points relevés mais laissés en l'état (choix volontaires, pas des bugs) :

- Les `<img>` de la section "Visuels" ont un `src=""` vide par construction : c'est un emplacement à remplacer, le `onerror` gère proprement le fallback visuel tant qu'aucune image n'est fournie.
- Le fallback des logos (`onerror="this.parentNode.innerHTML=...">`) injecte du HTML inline en JS — fonctionnel et sans risque ici (contenu statique, pas de donnée utilisateur), mais à éviter si la source des logos devenait un jour dynamique/externe.
- La classe CSS `.img-airbus` (dans `styles.css`) n'est référencée par aucun élément du HTML actuel — elle peut être supprimée si elle ne sert pas ailleurs, ou appliquée au `<img>` du logo Airbus si un alignement de taille spécifique est souhaité.

Aucun autre problème structurel ou de syntaxe détecté (HTML valide, CSS sans règle dupliquée problématique, JS minimal et sans fuite mémoire — un seul `setTimeout` correctement réinitialisé via `clearTimeout`).

## Auteur

Arthur Duret — Stage A2 Informatique, Cycle Ingénieur, CESI École d'Ingénieurs (2026), mission SOREAM chez Airbus Helicopters.
