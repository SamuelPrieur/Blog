---
title: 5 astuces CSS que j'aurais aimé connaître plus tôt
date: 2026-10-10
description: Petites astuces CSS pour gagner du temps au quotidien.
tags: [css, design, astuces]
---

## 1. Les variables custom properties

    :root {
      --accent: #da4b0b;
    }

## 2. Le sélecteur :is()

    :is(h1, h2, h3) a {
      color: inherit;
    }

## 3. inset shorthand

    position: absolute;
    inset: 0; /* top, right, bottom, left en une ligne */

## 4. Les filtres sur les backgrounds

    backdrop-filter: blur(10px);

## 5. scroll-behavior

    html {
      scroll-behavior: smooth;
    }