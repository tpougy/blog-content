---
title: "Theme-aware images test"
description: "Verification post for FEAT-01 — theme-aware image rehype plugin."
date: "May 18 2026"
lang: "en"
tags: ["test", "theme"]
draft: false
---

This post verifies that the rehype plugin for FEAT-01 correctly renders theme-aware image pairs.

## Themed image (FEAT-01 test)

The image below should render differently in light and dark mode:

![Diagram](/test-theme-images/diagram.light.svg)

## Regular image (passthrough test)

This image has no `.light` or `.dark` suffix and should render as a single `<img>` tag unchanged in both themes:

![Normal image](./assets/normal.svg)

