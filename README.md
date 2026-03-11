# TĀFELE

> A sketchpad for diagrams, UI wireframes, and relational ideas — built for humans and LLMs alike.
![TĀFELE screenshot](https://github.com/SashaYerashoff/Tafele/blob/main/Screenshot%20From%202026-03-11%2018-33-04.png)

## What is it?

TĀFELE is a single-file, zero-dependency canvas diagramming tool. Open `tafele.html` in any browser and start drawing — no install, no account, no build step.

It has two modes:

- **FLOW** — classic flowchart shapes: process, decision, terminal, I/O, database, document, and more
- **UI WIREFRAME** — interface components: cards, modals, panels, buttons, inputs, headings, badges, comments

The key idea: draw your flow or UI sketch, then export it as a **`.tafele` file** or a **Wireframe Spec** and paste it directly into an LLM. Instead of spending paragraphs trying to describe a complex relationship or layout in prose, you hand the model a structured, readable description of exactly what you drew.

## Features

- 🖊️ **Two shape palettes** — 9 flow shapes + 14 UI wireframe components
- 🔗 **Connections** — bezier curves with labels, drawn by dragging from anchor dots
- 🔍 **Zoom & pan** — Ctrl+scroll, Space/Alt+drag, FIT button
- ↩️ **80-step undo/redo** — Ctrl+Z / Ctrl+Y
- 📋 **Copy/paste** — Ctrl+C/V with offset stacking
- 💾 **Save/Open** — native `.tafele` JSON format, drag-drop or browse
- 🧜 **Mermaid export/import** — export flowchart TD, import any flowchart/graph syntax
- 📐 **Wireframe Spec export** — hierarchical text (TWS) format: containment, reading order, element types — ready to paste into any LLM
- 🖼️ **PNG export** — 2× resolution download

## The `.tafele` Format

`.tafele` files are plain JSON. Each shape has an `id`, `type`, `x`, `y`, `w`, `h`, and `label`. Connections reference shape IDs and named anchors (`top`, `right`, `bottom`, `left`).

```json
{
  "version": 1,
  "app": "tafele",
  "shapes": [
    { "id": 1, "type": "terminal", "x": 100, "y": 100, "w": 140, "h": 50, "label": "Start" },
    { "id": 2, "type": "process",  "x": 100, "y": 200, "w": 140, "h": 60, "label": "Do the thing" }
  ],
  "conns": [
    { "id": 3, "from": 1, "fromAnchor": "bottom", "to": 2, "toAnchor": "top", "label": "" }
  ]
}
```

LLMs can read, generate, and modify `.tafele` files directly — useful for iterating on diagrams or UI layouts in chat.

## Wireframe Spec (TWS)

The TWS export describes UI layouts as indented, human-readable text. Shapes whose center falls inside a container (Card, Modal, Panel) are nested as children:

```
CARD  "Login"  [340×200]
  HEADING  "Welcome back"
  LABEL  "Email"
  INPUT  "you@example.com"
  LABEL  "Password"
  INPUT  "••••••••"
  BUTTON  "Sign In"  [primary]
  BUTTON  "Cancel"  [ghost]
```

Paste this into any LLM conversation to describe your UI without ambiguity.

## Usage

```
open tafele.html
```

That's it.

| Key | Action |
|-----|--------|
| `V` | Select mode |
| `D` | Draw mode |
| `C` | Connect mode |
| `Del` | Delete selected |
| `Ctrl+C/V` | Copy / paste |
| `Ctrl+Z/Y` | Undo / redo |
| `Ctrl+Scroll` | Zoom |
| `Space+drag` | Pan |
| `Dbl-click` | Edit label |

## File

Everything lives in a single file: **`tafele.html`**

No framework. No bundler. No server. Canvas-rendered, dark theme, JetBrains Mono.
