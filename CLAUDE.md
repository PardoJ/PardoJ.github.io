# Guide de développement : Typographie & Design

## Vue d'ensemble du projet

Ce projet est un système de pages web statiques axé sur la **typographie optimale pour la lecture**. Il applique rigoureusement les principes d'UX/UI et d'imprimerie traditionnelle pour créer une expérience de lecture confortable et accessible.

### Philosophie du projet

- **Minimalisme radical** : Aucune dépendance externe, pas de framework, pas de JavaScript
- **Standards web purs** : HTML5 sémantique et CSS3 moderne uniquement
- **Logiciel libre** : Approche open source, code simple et maintenable
- **Accessibilité** : Respect WCAG, dégradation gracieuse
- **Performance** : Poids minimal, chargement rapide

---

## Strucure des fichiers du site web

### A la racine du site
Les fichiers techniques style.css, logo.svg et autre détaillent les besoin du site
Le fichier index.html est la page d'accueil et le menu principal du site, il renvoit vers toutes les pages.

### Les sous dossiers
Ils représentent des catégories de contenu et contiennent les articles liés à ces contenus.

### Le dossier '_images/'
Contient les images utilisée sur le site, organisées en sous dossiers de catégories et en sous sous dossiers d'articles.

## Principes typographiques fondamentaux

### Polices de caractères

**Texte courant** : Georgia (serif)
- Optimisée pour l'écran
- Contre-formes généreuses
- Hauteur d'x élevée

**Titres** : Polices système sans-serif
- `-apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Helvetica Neue', Arial, sans-serif`
- Cohérence avec l'interface utilisateur
- Performance (pas de chargement de police)

**Code** : Polices monospace système
- `'SF Mono', 'Monaco', 'Inconsolata', 'Fira Code', 'Consolas', 'Courier New', monospace`
- Chasse fixe pour alignement vertical
- Ligatures désactivées pour le code

**En-tête du site** : Times New Roman
- Approche éditoriale classique
- Élégance et autorité

### Tailles et échelle

**Échelle modulaire** : Ratio 1.25
```
--text-xs   : base / 1.25 / 1.25
--text-sm   : base / 1.25
--text-base : 16px (mobile) / 18px (desktop)
--text-lg   : base × 1.25
--text-xl   : base × 1.25²
--text-2xl  : base × 1.25³
```

**Interlignage optimal** : 120-145% du corps
- Texte courant : 1.5 (150%)
- Titres : 1.2 (tight)
- Listes : 1.75 (relaxed)
- Code : 1.6

### Longueur de ligne

**Plage optimale** : 50-75 caractères (8-12 mots en français)
```
Mobile    : 65ch
Tablette  : 75ch (≥768px)
Desktop   : 85ch (≥1024px)
```

### Couleurs

**Palette principale** :
```css
--color-text           : #1a1a1a  /* Gris très foncé */
--color-text-light     : #4a4a4a  /* Gris moyen */
--color-background     : #fafafa  /* Blanc cassé */
--color-background-alt : #ffffff  /* Blanc pur */
```

**Liens** :
```css
--color-link         : #0051a8  /* Bleu foncé, contraste 7.5:1 */
--color-link-hover   : #003d7a  /* Bleu plus foncé */
--color-link-visited : #6b3fa0  /* Violet/pourpre */
```

**Rationale** : Contraste réduit (#1a1a1a au lieu de #000) pour diminuer la fatigue oculaire sur écran lumineux.

---

## Structure HTML

### Anatomie d'une page type

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="...">
    <title>...</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- En-tête de site (sur toutes les pages) -->
    <header class="site-header">
        <h1 class="site-title">
            <a href="/">Nom du site</a>
        </h1>
        <img src="logo.svg" alt="Logo" class="site-logo">
    </header>

    <!-- Contenu principal -->
    <article class="container">
        <header class="article-header">
            <h1>Titre de l'article</h1>
            <div class="meta">Métadonnées</div>
            <p class="lead">Chapô introductif</p>
        </header>

        <!-- Table des matières (optionnelle) -->
        <details class="toc" open>
            <summary>Table des matières</summary>
            <ol class="toc-list">
                <li><a href="#section">Section</a></li>
            </ol>
        </details>

        <!-- Sections de contenu -->
        <section>
            <h2 id="section">
                <a href="#section" class="anchor" aria-label="Lien vers cette section">§</a>
                Titre de section
            </h2>
            <p>Contenu...</p>
        </section>
    </article>

    <!-- Pied de page -->
    <footer class="container">
        <div class="footer-content">
            <p>© 2026 · Contact · Liens</p>
        </div>
    </footer>
</body>
</html>
```

### Éléments sémantiques

**Texte** :
- `<p>` : Paragraphes standard
- `<em>` : Emphase (italique)
- `<strong>` : Importance forte (gras)
- `<blockquote>` : Citations

**Code** :
- `<code>` : Code inline
- `<pre><code>` : Blocs de code
- Pas de coloration syntaxique (philosophie minimaliste)

**Images** :
- `<img>` seule : Image simple
- `<figure>` + `<figcaption>` : Image avec légende
- Classes : `.full-width`, `.small`
- `<div class="gallery">` : Galerie d'images
- Attributs obligatoires : `alt`, `loading="lazy"`, `width`, `height`

**Listes** :
- `<ul>` : Listes non ordonnées
- `<ol>` : Listes ordonnées (table des matières)

---

## Architecture CSS

### Organisation du fichier

1. **Variables CSS** (custom properties)
2. **Reset et base**
3. **Conteneur principal**
4. **En-tête de site**
5. **Typographie** (titres, paragraphes, listes)
6. **Mise en emphase**
7. **Code**
8. **Liens**
9. **Séparateurs**
10. **Images et figures**
11. **Tableaux**
12. **Footer**
13. **Métadonnées et article header**
14. **Table des matières**
15. **Ancres dans les titres**
16. **Media queries** (mobile, impression, accessibilité)

### Variables CSS essentielles

Toujours utiliser les variables CSS pour faciliter la maintenance :
```css
var(--base-font-size)
var(--text-sm), var(--text-base), var(--text-lg), etc.
var(--space-xs), var(--space-sm), var(--space-md), var(--space-lg), var(--space-xl)
var(--color-text), var(--color-link), var(--color-background)
var(--content-width)
var(--line-height-base)
```

### Breakpoints responsive

```css
Mobile    : < 768px  (défaut)
Tablette  : ≥ 768px  (@media (min-width: 768px))
Desktop   : ≥ 1024px (@media (min-width: 1024px))
```

**Approche** : Mobile-first avec progressive enhancement

### Règles de formatage

**Espacement vertical** :
- Entre sections : `var(--space-xl)` (3rem)
- Entre paragraphes : `var(--space-md)` (1.5rem)
- Entre éléments proches : `var(--space-sm)` (1rem)
- Entre éléments très proches : `var(--space-xs)` (0.5rem)

**Marges latérales** :
- Desktop : `var(--space-xl)` (3rem)
- Tablette : `var(--space-lg)` (2rem)
- Mobile : `var(--space-sm)` (1rem)

---

## Composants spécifiques

### En-tête de site

**Caractéristiques** :
- Hauteur minimale (quasiment une ligne de texte)
- Flexbox : titre à gauche, logo à droite
- Bordure inférieure subtile
- Suit le scroll (pas de sticky)
- Logo : 1.5rem de hauteur (1.25rem sur mobile)

### Table des matières

**Utilisation** : Articles longs avec plusieurs sections H2

**Implémentation** :
```html
<details class="toc" open>
    <summary>Table des matières</summary>
    <ol class="toc-list">
        <li><a href="#id">Titre</a></li>
    </ol>
</details>
```

**Fonctionnement** :
- `<details>` natif HTML (pas de JS)
- Ouverte par défaut (`open`)
- Rétractable d'un clic
- Indicateur "▸" qui pivote

### Ancres dans les titres

**But** : Permettre de partager l'URL d'une section précise

**Implémentation** :
```html
<h2 id="section-id">
    <a href="#section-id" class="anchor" aria-label="Lien vers cette section">§</a>
    Titre de la section
</h2>
```

**Comportement** :
- Symbole "§" invisible par défaut
- Apparaît au survol du titre (desktop)
- Toujours visible mais atténué sur mobile
- Position absolute à gauche du titre

### Images

**Types supportés** :

1. **Image standard** :
```html
<img src="image.jpg" alt="Description" loading="lazy" width="800" height="600">
```

2. **Image avec légende** :
```html
<figure>
    <img src="image.jpg" alt="Description" loading="lazy" width="800" height="600">
    <figcaption>Légende de l'image</figcaption>
</figure>
```

3. **Image pleine largeur** :
```html
<img src="large.jpg" alt="Description" class="full-width" loading="lazy" width="1200" height="600">
```

4. **Petite image** :
```html
<img src="icon.jpg" alt="Description" class="small" loading="lazy" width="400" height="300">
```

5. **Galerie** :
```html
<div class="gallery">
    <figure>
        <img src="1.jpg" alt="Description" loading="lazy" width="400" height="400">
        <figcaption>Légende 1</figcaption>
    </figure>
    <figure>
        <img src="2.jpg" alt="Description" loading="lazy" width="400" height="400">
        <figcaption>Légende 2</figcaption>
    </figure>
</div>
```

**Règles obligatoires** :
- Toujours inclure `alt` descriptif
- Toujours inclure `loading="lazy"`
- Toujours inclure `width` et `height` explicites (évite layout shift)
- Formats recommandés : WebP (performance), JPEG (photos), SVG (logos/icônes)

### Code

**Code inline** :
```html
<code>variable</code>
```

**Blocs de code** :
```html
<pre><code>function example() {
  return true;
}</code></pre>
```

**Règles** :
- Pas de coloration syntaxique (minimalisme)
- Passage à la ligne automatique (`white-space: pre-wrap`)
- Évite le scroll horizontal sur mobile
- Police monospace avec ligatures désactivées
- Interlignage 1.6 pour respiration verticale

### Footer

**Contenu type** :
- Copyright et année
- Liens de contact
- Lien vers code source (GitHub)
- Mention de licence (CC BY-SA, GPL, etc.)
- Mention technique ("Construit avec HTML5 et CSS3, sans JavaScript")

**Style** :
- Taille de texte réduite
- Couleur atténuée
- Centré
- Liens discrets (soulignement au survol uniquement)

---

## Principes de conception

### 1. Lisibilité avant tout

**Toujours privilégier** :
- Longueur de ligne optimale (50-75 caractères)
- Interlignage généreux (150% minimum)
- Contraste suffisant mais pas excessif
- Espacements cohérents et respirants

**Toujours éviter** :
- Lignes trop longues (>100 caractères)
- Interlignage serré (<120%)
- Noir pur sur blanc pur (éblouissement)
- Sur-formatage (trop de gras, trop de couleurs)

### 2. Approche minimaliste

**Ce qui est inclus** :
- HTML5 sémantique
- CSS3 moderne (variables, grid, flexbox)
- Fonctionnalités natives (`<details>`, `loading="lazy"`)

**Ce qui est exclu** :
- JavaScript (sauf si absolument nécessaire)
- Frameworks CSS (Bootstrap, Tailwind, etc.)
- Bibliothèques externes
- Polyfills
- Coloration syntaxique automatique

### 3. Performance

**Objectifs** :
- Première page < 50 KB (HTML + CSS)
- Images optimisées (WebP, lazy loading)
- Pas de requêtes externes
- Rendu instantané

**Techniques** :
- CSS inline pour variables critiques
- Images avec dimensions explicites
- Lazy loading natif
- Formats modernes (WebP, SVG)

### 4. Accessibilité

**Standards respectés** :
- WCAG 2.1 niveau AA minimum
- Contrastes suffisants (4.5:1 minimum)
- Navigation au clavier
- Lecteurs d'écran compatibles

**Techniques** :
- HTML sémantique
- Attributs `alt` descriptifs
- Attributs ARIA quand nécessaires
- `prefers-reduced-motion` respecté
- `prefers-contrast` respecté
- `prefers-color-scheme` respecté (dark mode)

### 5. Responsive design

**Approche** : Mobile-first

**Breakpoints** :
```
< 768px   : Mobile (défaut)
≥ 768px   : Tablette
≥ 1024px  : Desktop
```

**Adaptations clés** :
- Taille de police : 16px → 18px
- Largeur de contenu : 65ch → 75ch → 85ch
- Marges : 1rem → 2rem → 3rem
- Galeries : 1 colonne → auto-fit (250px min)
- Logo : 1.25rem → 1.5rem

---

## Conventions de code

### HTML

**Indentation** : 4 espaces

**Attributs** :
```html
<!-- Ordre recommandé -->
<img 
    src="image.jpg" 
    alt="Description" 
    class="full-width"
    loading="lazy"
    width="800"
    height="600">
```

**Classes** :
- Noms descriptifs en kebab-case
- Pas de classes utilitaires (approche sémantique)
- Classes de composants : `.toc`, `.gallery`, `.site-header`
- Classes de variantes : `.full-width`, `.small`, `.lead`

### CSS

**Indentation** : 2 espaces

**Organisation des propriétés** :
1. Positionnement (position, top, left, etc.)
2. Box model (display, width, height, margin, padding, border)
3. Typographie (font, text, line-height)
4. Visuel (background, color, opacity)
5. Autres (transform, transition, etc.)

**Nommage** :
- Variables : `--nom-descriptif`
- Classes : `.nom-composant`
- Modificateurs : `.composant-variante`

**Commentaires** :
```css
/* === SECTION MAJEURE === */

/* Commentaire de sous-section */

/* Note spécifique sur une règle complexe */
```

---

## Workflow de développement

### Ajout d'une nouvelle page

1. **Copier** le template de base (structure HTML type)
2. **Adapter** le contenu dans `<article class="container">`
3. **Ajouter** la page à la navigation si nécessaire
4. **Tester** sur mobile, tablette, desktop
5. **Valider** l'accessibilité (contraste, navigation clavier)

### Ajout d'un nouveau composant

1. **Définir** le besoin et la structure HTML
2. **Créer** le CSS dans la section appropriée
3. **Tester** la responsivité
4. **Vérifier** l'accessibilité
5. **Documenter** dans ce fichier

### Modification du style

1. **Identifier** la variable CSS concernée
2. **Modifier** la variable plutôt que les valeurs en dur
3. **Tester** l'impact sur toutes les pages
4. **Vérifier** les breakpoints responsive
5. **Valider** que les contrastes restent suffisants

---

## Checklist de qualité

### Avant chaque commit

- [ ] Le HTML est valide (HTML5)
- [ ] Le CSS est valide (CSS3)
- [ ] Aucune erreur dans la console
- [ ] Testé sur mobile (<768px)
- [ ] Testé sur tablette (768-1023px)
- [ ] Testé sur desktop (≥1024px)
- [ ] Navigation au clavier fonctionnelle
- [ ] Contrastes suffisants (vérifier avec outil)
- [ ] Images avec alt, loading, width, height
- [ ] Pas de dépendances externes ajoutées
- [ ] Performance maintenue (<50KB première page)

### Avant mise en production

- [ ] Tous les liens fonctionnent
- [ ] Toutes les images chargent
- [ ] Footer correct sur toutes les pages
- [ ] Table des matières à jour
- [ ] Métadonnées (title, description) remplies
- [ ] Testé avec lecteur d'écran
- [ ] Testé en mode dark
- [ ] Testé avec zoom (200%)
- [ ] Fichier `claude.md` à jour

---

## Ressources et références

### Documentation technique

- [MDN Web Docs](https://developer.mozilla.org/) : Référence HTML/CSS
- [Can I Use](https://caniuse.com/) : Compatibilité navigateurs
- [WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/) : Standards d'accessibilité
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) : Vérification des contrastes

### Typographie et design

- [Practical Typography](https://practicaltypography.com/) : Guide typographique moderne
- [The Elements of Typographic Style Applied to the Web](https://webtypography.net/)
- Robert Bringhurst, *The Elements of Typographic Style* (livre de référence)

### Outils

- Éditeur de texte : VS Code, Vim, ou autre
- Navigateur : Firefox Developer Edition ou Chrome DevTools
- Validation : W3C Validator (HTML), Jigsaw (CSS)
- Images : DxO PhotoLab, GIMP, Darktable (logiciels libres)
- SVG : Inkscape ou éditeur de texte

---

## Notes de maintenance

### Variables à surveiller

Lors de modifications, ces variables impactent l'ensemble du design :
- `--base-font-size` : Taille de base (16px mobile, 18px desktop)
- `--scale-ratio` : Ratio de l'échelle typographique (1.25)
- `--content-width` : Largeur maximale du contenu (65/75/85ch)
- `--line-height-base` : Interlignage standard (1.5)

### Dépendances système

**Polices utilisées** (toutes système, pas de chargement) :
- Georgia (texte courant)
- Times New Roman (en-tête site)
- System fonts sans-serif (titres)
- System fonts monospace (code)

Si une police n'est pas disponible, le fallback fonctionne automatiquement.

### Compatibilité navigateurs

**Support minimum** :
- Chrome/Edge 88+ (janvier 2021)
- Firefox 85+ (janvier 2021)
- Safari 14+ (septembre 2020)

**Fonctionnalités modernes utilisées** :
- CSS Custom Properties (variables)
- CSS Grid
- Flexbox
- `<details>` / `<summary>`
- `loading="lazy"`
- `prefers-color-scheme`, `prefers-contrast`, `prefers-reduced-motion`

**Dégradation gracieuse** : Les navigateurs anciens affichent le contenu correctement mais sans les améliorations progressives.

---

## Évolutions futures possibles

### Fonctionnalités envisageables

- **Recherche** : Recherche côté client avec un petit script JS
- **Navigation inter-articles** : Liens précédent/suivant
- **Fil d'Ariane** : Navigation hiérarchique pour sites complexes
- **Tags/Catégories** : Organisation thématique du contenu
- **RSS Feed** : Syndication du contenu

### Améliorations techniques

- **Service Worker** : Cache pour navigation offline
- **Manifest** : PWA pour installation sur mobile
- **Compression** : Gzip/Brotli côté serveur
- **CDN** : Distribution de contenu pour performance globale

### Règles pour les ajouts

**Un ajout est acceptable si** :
1. Il améliore significativement l'expérience utilisateur
2. Il reste dans la philosophie minimaliste
3. Il ne nécessite pas de dépendances lourdes
4. Il reste accessible et performant
5. Il se dégrade gracieusement

**Un ajout est à éviter si** :
1. Il nécessite un framework externe
2. Il augmente significativement le poids de la page
3. Il complexifie la maintenance
4. Il crée une dépendance externe
5. Il n'apporte qu'un bénéfice esthétique

---

## Contact et contribution

Pour toute question ou suggestion d'amélioration, maintenir l'esprit du projet :
- Minimalisme et simplicité
- Standards web et accessibilité
- Performance et maintenabilité
- Typographie et lisibilité

**Principe directeur** : La forme sert le fond, jamais l'inverse.

---

*Dernière mise à jour : 11 janvier 2026*