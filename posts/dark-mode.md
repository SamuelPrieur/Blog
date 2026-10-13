---
title: Implémenter un dark mode avec GSAP
date: 2026-10-12
description: Transition fluide entre light et dark mode avec des CSS variables et GSAP.
tags: [css, gsap, react]
---

## L'idée

Stocker la palette en `sessionStorage`, puis animer les variables CSS
directement avec GSAP.

    gsap.to(document.documentElement, {
      duration: 0.5,
      "--base-background": "#1e1e1e",
      ease: "power2.inOut",
    });

## Attention

Le fallback `sessionStorage` doit prévoir une valeur par défaut
au premier chargement.