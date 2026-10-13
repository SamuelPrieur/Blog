---
title: Animer du texte avec GSAP et SplitType
date: 2026-10-05
description: Guide pratique pour créer des animations de reveal sur du texte.
tags: [gsap, animation, react]
---

## Le principe

On découpe le texte en mots avec SplitType, puis on anime chaque mot avec GSAP.

### Exemple

    gsap.to(words, {
      y: 0,
      stagger: 0.02,
      duration: 1,
      ease: "power3.out",
    });

### Astuce anti-flash

Il faut initialiser les positions **avant** le premier rendu pour éviter
le flash de contenu non animé.