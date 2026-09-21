---
layout: page
title: Alethic
description: Generate–Verify–Revise reasoning agent for mathematics and physics
importance: 2
category: software
github: https://github.com/hyperion-git/alethic
---

Alethic is an open-source reimplementation of the Generate–Verify–Revise architecture from Google DeepMind's Aletheia paper, built on Claude. A generator drafts a proof or physics derivation, an independent verifier that never sees the generator's reasoning grades it, and a reviser repairs it until the verdict clears a confidence threshold, or the agent admits failure.

It ships as Claude Code skills (`/alethic-solve`, `/alethic-derive`, `/alethic-scientific-figure`) and as a Python library with a CLI, a sandboxed SymPy/NumPy execution environment and four speed-versus-rigour presets.

- Source: [github.com/hyperion-git/alethic](https://github.com/hyperion-git/alethic) (Apache-2.0)
