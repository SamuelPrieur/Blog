---
title: Showcase Markdown du blog
date: 2026-10-14
description: Guide des styles Markdown compatibles avec Obsidian et ReactMarkdown.
tags:
  - design
  - astuces
---

# Showcase Markdown du blog

> **But de cette page** — servir de billet de démonstration pour le blog React : typographie, contenu technique, médias et extensions Markdown.

Ce document est volontairement plus riche qu’un Markdown « de base ». Le rendu dépend du moteur utilisé par le blog. Dans la configuration actuelle, `ReactMarkdown` est associé à `remark-gfm` pour le [GitHub Flavored Markdown (GFM)](https://github.github.com/gfm/), ce qui couvre notamment les tableaux, les cases à cocher et le ~~texte barré~~.

> **À retenir :** tout ce qui suit ne fonctionne pas automatiquement dans un renderer Markdown ordinaire. Les équations, les callouts et certaines syntaxes Obsidian nécessitent des plugins, des extensions ou un renderer React personnalisé.

## Sommaire rapide

- [Mise en forme](#mise-en-forme)
- [Liens et images](#liens-et-images)
- [Listes et tâches](#listes-et-tâches)
- [Code](#code)
- [Tableaux](#tableaux)
- [Citations et callouts](#citations-et-callouts)
- [Mathématiques](#mathématiques)
- [Fonctionnalités propres à Obsidian](#fonctionnalités-propres-à-obsidian)
- [Compatibilité React](#compatibilité-react)

---

## Mise en forme

Un paragraphe peut contenir du **gras**, de l’*italique*, du ***gras italique***, du ~~barré~~ et du `code en ligne`. On peut aussi utiliser des caractères échappés comme `\*` pour afficher un astérisque littéral.

### Une hiérarchie lisible

Les titres `h1` à `h6` structurent l’article. Évitez de sauter plusieurs niveaux sans raison : les titres aident autant les lecteurs que la navigation au clavier et les technologies d’assistance.

#### Petit exemple éditorial

La simplicité est une fonctionnalité : un article doit rester agréable à lire, même lorsqu’il explique une API, un hook React ou une configuration de build.

---

## Liens et images

- Lien externe : [documentation de React Markdown](https://github.com/remarkjs/react-markdown).
- Lien interne : [retour au sommaire](#sommaire-rapide).
- Lien avec titre : [GitHub](https://github.com "Visiter GitHub").
- Adresse automatique (GFM) : <https://react.dev>.
- Courriel : <bonjour@example.com>.

### Image distante

![Montagnes au lever du jour](https://images.unsplash.com/photo-1464822759023-fed622ff2c3b?auto=format&fit=crop&w=1200&q=80 "Illustration de couverture")

*Le texte alternatif reste indispensable : il décrit l’image quand celle-ci ne peut pas être affichée et améliore l’accessibilité.*

### Image locale du projet

![Illustration du blog](/img/Mountain.png)

Le chemin de l’image doit correspondre à la façon dont les assets sont servis par l’application React. Une image distante peut aussi être filtrée par une politique CSP ou échouer hors connexion.

---

## Listes et tâches

### Liste non ordonnée

- **Frontend**
  - React
  - Vite
  - CSS
- **Animation**
  - GSAP
  - SplitType
- **Contenu**
  - Markdown
  - Métadonnées YAML

### Liste ordonnée

1. Écrire le brouillon.
2. Vérifier les liens et les images.
3. Publier le fichier dans `posts/`.
4. Contrôler le rendu sur mobile.

### Checklist GFM

- [x] Charger l’article depuis GitHub
- [x] Afficher le titre et la date
- [x] Activer `remark-gfm`
- [ ] Ajouter le support des équations
- [ ] Ajouter un renderer pour les callouts

> Les cases à cocher ci-dessus sont une extension GFM : elles nécessitent `remark-gfm` avec React Markdown, ou un équivalent dans votre pipeline.

---

## Code

Le code court s’écrit avec des accents graves : `const slug = "mon-article"`.

### JavaScript / React

```jsx
import ReactMarkdown from "react-markdown";
import remarkGfm from "remark-gfm";

export function Article({ content }) {
  return (
    <div className="post-content">
      <ReactMarkdown remarkPlugins={[remarkGfm]}>
        {content}
      </ReactMarkdown>
    </div>
  );
}
```

### Appel réseau en JavaScript

```js
const response = await fetch("https://api.example.com/posts");
if (!response.ok) throw new Error(`HTTP ${response.status}`);
const posts = await response.json();
```

### CSS

```css
.post-content {
  max-width: 70ch;
  margin-inline: auto;
  line-height: 1.7;
}

.post-content img {
  max-width: 100%;
  height: auto;
}
```

Le langage indiqué après les trois accents (par exemple `jsx`, `js` ou `css`) permet à un plugin de coloration syntaxique de choisir le bon lexer. Sans plugin de highlight, le bloc reste tout de même du code préformaté.

---

## Tableaux

| Élément | Extension / outil | Statut |
| --- | --- | --- |
| Titres, listes, liens | Markdown standard | ✅ Natif |
| Tableaux, tâches, barré | `remark-gfm` | ✅ Activé dans le blog |
| Équations | `remark-math` + `rehype-katex` | 🔧 À configurer |
| Callouts | Renderer React personnalisé | 🔧 À configurer |
| Wikilinks | Plugin Obsidian ou transformation dédiée | 🟡 Obsidian seulement |

Les tableaux conviennent aux comparaisons courtes. Pour des données longues ou complexes, préférez une vraie interface tabulaire avec une navigation accessible.

---

## Citations et callouts

### Citation standard

> « La lisibilité est une forme de respect pour le lecteur. »
>
> — Principe éditorial du blog

### Callout Obsidian simple

> [!NOTE]
> Cette boîte est une **syntaxe de callout Obsidian**. Un renderer Markdown standard l’affichera généralement comme une citation contenant le texte `[!NOTE]`.

### Callout Obsidian avec titre

> [!TIP] Astuce React
> Gardez les transformations de contenu dans un composant dédié : le renderer d’article reste ainsi facile à tester.

### Callout repliable (Obsidian)

> [!INFO]- Détails techniques
> Le signe `-` demande à Obsidian de replier le contenu par défaut.
>
> Cette capacité n’est pas une règle Markdown standard. En React, il faut interpréter la syntaxe et produire par exemple un élément HTML `<details>`.

### Callout imbriqué (Obsidian)

> [!WARNING] Attention aux différences de renderer
> Le même fichier peut avoir des rendus différents selon l’application.
>
> > [!TIP] Conseil
> > Documentez les extensions activées dans le projet et testez les articles avec le renderer réellement utilisé en production.

> **Compatibilité :** les exemples `[!NOTE]`, `[!TIP]`, `[!INFO]-` et les callouts imbriqués sont Obsidian-style. Pour les afficher comme des cartes colorées dans React, ajoutez une transformation (par exemple un plugin `remark` ou un composant `blockquote` personnalisé) et les styles CSS correspondants.

---

## Mathématiques

### Équation en ligne

La relation entre la vitesse, la distance et le temps s’écrit $v = \frac{d}{t}$.

### Équation sur plusieurs lignes

$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$

Cette syntaxe nécessite généralement `remark-math` côté `remark`, puis `rehype-katex` (et la feuille de style KaTeX) côté `rehype` :

```js
<ReactMarkdown
  remarkPlugins={[remarkGfm, remarkMath]}
  rehypePlugins={[rehypeKatex]}
>
  {content}
</ReactMarkdown>
```

Sans cette chaîne de plugins, les délimiteurs `$...$` et `$$...$$` risquent d’être rendus comme du texte brut ou de ne pas être interprétés.

---

## Notes de bas de page

Le Markdown GFM permet d’associer une référence[^accessibilite] à une note située plus bas. Cette technique est pratique pour garder le fil de la lecture tout en ajoutant une précision.

[^accessibilite]: Vérifiez toutefois que le plugin utilisé génère des liens de retour accessibles et des identifiants uniques lorsque plusieurs articles sont rendus sur la même page.

---

## Fonctionnalités propres à Obsidian

Les exemples suivants sont **étiquetés Obsidian-only** : ils ne sont pas garantis par Markdown standard ni par `react-markdown` avec `remark-gfm` seul.

### Wikilink — Obsidian-only

Obsidian peut transformer `[[Guide React]]` en lien interne vers une note : [[Guide React]].

Avec une section ciblée : [[Guide React#Compatibilité React]].

### Transclusion — Obsidian-only

Pour intégrer le contenu d’une autre note, Obsidian utilise une transclusion : `![[Guide React]]`.

Exemple visuel (Obsidian-only, à ne pas confondre avec une image Markdown) :

![[Guide React]]

> Dans un blog React, ces syntaxes peuvent rester textuelles, être converties en liens par un plugin, ou être résolues par une logique applicative. Il faut choisir explicitement le comportement attendu et gérer les notes introuvables pour éviter des références cassées.

---

## Compatibilité React

### Ce que le blog sait déjà rendre

Dans le composant d’article actuel, `ReactMarkdown` reçoit `remarkGfm`. Le contenu Markdown peut donc exploiter les fonctionnalités GFM prises en charge par cette extension, notamment les tableaux, les tâches et le barré.

### Ce qui demande une extension

Pour obtenir un rendu complet de ce showcase, prévoyez au minimum :

1. `remark-gfm` pour le GFM (déjà utilisé par le blog).
2. `remark-math` pour analyser les délimiteurs mathématiques.
3. `rehype-katex` et les styles KaTeX pour afficher les formules.
4. Un plugin `remark`/`rehype` ou un composant personnalisé pour les callouts.
5. Une stratégie dédiée pour les wikilinks et transclusions Obsidian.
6. Une solution de coloration syntaxique si les blocs de code doivent être colorés.

> **Sécurité :** n’activez pas du HTML brut ou des composants arbitraires sans traiter la question de la confiance dans le contenu. Les articles récupérés depuis une source externe doivent être nettoyés selon la politique de sécurité du site.

### Exemple de configuration étendue

```jsx
import ReactMarkdown from "react-markdown";
import remarkGfm from "remark-gfm";
import remarkMath from "remark-math";
import rehypeKatex from "rehype-katex";
import "katex/dist/katex.min.css";

export function MarkdownArticle({ content }) {
  return (
    <ReactMarkdown
      remarkPlugins={[remarkGfm, remarkMath]}
      rehypePlugins={[rehypeKatex]}
    >
      {content}
    </ReactMarkdown>
  );
}
```

Cette configuration rend les mathématiques possibles, mais ne transforme pas automatiquement les callouts ou les wikilinks : chaque syntaxe supplémentaire doit être implémentée et testée séparément.

---

## Conclusion

Ce fichier rassemble une palette de styles pour composer des articles cohérents : une hiérarchie claire, des liens accessibles, des images documentées, des listes actionnables, du code, des tableaux, des citations, des notes et des extensions avancées.

**Règle pratique :** écrivez d’abord en Markdown portable, puis ajoutez les fonctionnalités Obsidian ou les plugins React dont le projet a réellement besoin.
