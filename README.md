# Parul Chemicals Sales Documentation

This repository contains the source code for the internal documentation website of the PC Sales Platform. It is built using [MkDocs](https://www.mkdocs.org/) and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

## 🚀 Getting Started

### Prerequisites
- Python 3.x installed.

### 1. Installation

Install the required packages:

```bash
pip install mkdocs mkdocs-material pymdown-extensions
```

### 2. Running Locally

To start the live-reloading development server:

```bash
mkdocs serve
```

The documentation will be accessible at: `http://127.0.0.1:8000`

### 3. Building for Production

To build the static HTML site (output goes to `site/` directory):

```bash
mkdocs build
```

## 📂 Project Structure

```
pc_sales_docs/
├── docs/                   # Markdown source files
│   ├── assets/             # Images, logos, favicons
│   ├── architecture/       # Architecture diagrams & modules
│   ├── guides/             # Developer how-to guides
│   ├── reference/          # API reference definitions
│   ├── concepts.md         # Business logic definitions
│   └── index.md            # Homepage
├── mkdocs.yml              # Main configuration file
└── site/                   # Generated static site (ignored in git)
```

## 📝 Editing Content

- **Navigation**: Update `nav` in `mkdocs.yml` to add new pages.
- **Diagrams**: Use mermaid syntax within ````mermaid` blocks.
- **Admonitions**: Use `!!! info` or `!!! warning` for callouts.
