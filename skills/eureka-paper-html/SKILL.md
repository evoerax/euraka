---
name: eureka-paper-html
description: Generate beautiful HTML reports from paper data. Uses Minimalism & Swiss Style design system with responsive layout and dark mode support. Perfect for paper presentations and sharing.
---

# Skill: eureka-paper-html

> HTML Paper Report Generation

## Overview

eureka-paper-html generates beautiful HTML reports from paper data using professional design systems. Suitable for paper presentations, sharing, and display.

## Design System

Uses **Minimalism & Swiss Style** (default) or **Cyberpunk** style:
- **Fonts**: Inter / Space Grotesk (body), JetBrains Mono (code)
- **Colors**: #2563EB (primary), #3B82F6 (secondary), #F97316 (CTA)
- **Features**: Clean, clear, high-contrast, responsive

## Templates

Two templates available in `references/templates/`:

1. **minimal.html** - Clean white background, Swiss Style
2. **cyberpunk.html** - Dark mode with gradient effects and animations

## Usage

### Basic Usage

```
/eureka-paper-html --input results.json --output report.html
```

### Specify Topic and Date

```
/eureka-paper-html --topic llm_agent --date 2026-03-17
```

### Full Parameters

```
/eureka-paper-html \
  --input results.json \
  --output report.html \
  --topic llm_agent \
  --date 2026-03-17 \
  --title "LLM Agent Research Progress"
```

## Input Format

Accepts JSON format paper data:

```json
[
  {
    "id": "2603.12933",
    "title": "Paper Title",
    "authors": ["Author1", "Author2"],
    "abstract": "Paper abstract...",
    "image": "https://example.com/image.png",
    "pseudo_code": "# Algorithm Name\nInput: ...\nOutput: ...\n1. Step one\n2. Step two",
    "contributions": ["contribution 1", "contribution 2"],
    "links": {
      "pdf": "https://...",
      "source": "https://..."
    },
    "tags": ["#Tag1", "#Tag2"],
    "published": "2026-03-13",
    "source": "arXiv"
  }
]
```

**Note**: 
- `image` is optional (max 1 per paper) - leave empty or omit if not available
- `pseudo_code` is optional - leave empty or omit if not available
- Abstracts should NOT be truncated Display full abstract content.

## Output Structure (Unified with eureka-paper-search)

Both HTML and Markdown outputs use the same structure:

```html
<!-- Header -->
<h1>yyyy-mm-dd_paper_{topic}</h1>

<!-- Overview Section -->
<section class="overview">
  <h2>Overview</h2>
  <div class="overview-cards">
    <div class="card">
      <h3>Overall Trend</h3>
      <p>{trend}</p>
    </div>
    <div class="card">
      <h3>Research Hotspots</h3>
      <p>{hotspots}</p>
    </div>
    <div class="card">
      <h3>Paper Count</h3>
      <p>{count} papers</p>
    </div>
  </div>
</section>

<!-- Paper List Section -->
<section class="papers">
  <h2>Paper List</h2>
  
  <!-- Each Paper -->
  <div class="paper-card">
    <h3>Paper Title</h3>
    <p><strong>Authors</strong>: {authors}</p>
    <p><strong>Links</strong>: [PDF] | [Source]</p>
    <p><strong>Tags</strong>: #Tag1 #Tag2</p>
    <p><strong>Abstract</strong>: {abstract}</p>
    <p><strong>Core Contributions</strong>: {contributions}</p>
    <!-- Pseudo-code (optional) -->
    <pre class="pseudo-code"><code>{pseudo_code}</code></pre>
  </div>
</section>
```

Fields match eureka-paper-search output:
- **Overview**: Overall Trend, Research Hotspots, Paper Count
- **Paper List**: Authors, Links, Tags, Abstract, Pseudo-code, Core Contributions
```

Features:
- Header (date, title)
- Overview section (Overall Trend, Research Hotspots)
- Paper card list (Authors, Links, Tags, Abstract, Pseudo-code, Core Contributions)
- Full abstract display (no truncation)
- PDF/Code/DOI links
- Responsive layout

## Design Features

1. **Card-based layout**: Each paper as independent card
2. **Responsive**: Adapts to mobile, tablet, desktop
3. **Dark mode**: Auto-adapts to system theme
4. **Accessibility**: Supports reduced-motion
5. **Fast loading**: Lightweight CSS

## Dependencies

- Python 3.x
- No extra dependencies (pure CSS)

## Relationship with eureka-paper-search

eureka-paper-html is a standalone skill, can be used independently:

- **Standalone**: Have paper data → Generate HTML
- **Combined**: eureka-paper-search → eureka-paper-html

```bash
# Combined usage example
eureka-paper-search llm_agent --output results.json
eureka-paper-html --input results.json --output report.html
```