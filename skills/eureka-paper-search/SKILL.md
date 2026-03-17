---
name: eureka-paper-search
description: Multi-source academic paper search tool with automatic fallback. Supports paper image extraction and pseudo-code generation from paper content. Generates structured paper recommendation notes in Obsidian or Markdown format.
---

# Skill: eureka-paper-search

> Multi-source Academic Paper Search

## Overview

eureka-paper-search is an independent skill for searching academic papers from multiple data sources with automatic fallback. It generates structured paper recommendation notes with optional image extraction and pseudo-code generation.

## Configuration

### 1. Research Interests

Create and edit `~/.eureka/preference.md` to configure your research interests:

```yaml
# Language setting
language: "zh"  # or "en"

# Research interests
research_interests:
  - topic: "llm_agent"
    keywords:
      - "LLM"
      - "agent"
      - "skill"
      - "autonomous"
    priority: high
```

### 2. Output Configuration

```yaml
output_target:
  type: "obsidian"  # or "markdown"
  obsidian:
    vault_path: "/path/to/vault"
    directory: "paper_daily"
```

### 3. Feature Configuration

```yaml
# Image extraction (optional)
image_extraction:
  enabled: true  # Enable/disable paper image extraction
  priority: "arxiv-source"  # "arxiv-source" | "pdf" | "both"
  top_n: 3  # Extract images for top N papers

# Pseudo-code generation (optional)
pseudo_code:
  enabled: true  # Enable/disable pseudo-code extraction
  top_n: 3  # Generate pseudo-code for top N papers
  include_algorithms: true  # Include algorithm descriptions
  include_math: true  # Include mathematical formulas
```

## Usage

### Basic Usage

```
/eureka-paper-search llm_agent
```

### Specify Topic

Search papers for a specific research topic:

```
/eureka-paper-search memory_skills
/eureka-paper-search reasoning
```

### Specify Date

```
/eureka-paper-search 2026-03-17 llm_agent
```

### Disable Features

```
/eureka-paper-search llm_agent --no-images --no-pseudo
```

## Features

### 1. Paper Image Extraction

When enabled, extracts images from papers:

- **arXiv source** (priority): Downloads paper source package, extracts figures/images
- **PDF fallback**: Extracts images directly from PDF
- **Output**: Saves to `{vault}/20_Research/Papers/{topic}/images/`

### 2. Pseudo-code Generation

When enabled, extracts pseudo-code from papers:

- **Algorithm descriptions**: Extracts algorithm steps from paper text
- **Mathematical formulas**: Renders equations in pseudo-code format
- **Output**: Includes pseudo-code in generated notes

#### Configuration Options

```yaml
pseudo_code:
  enabled: true              # Enable/disable pseudo-code extraction
  top_n: 3                  # Generate pseudo-code for top N papers
  include_algorithms: true  # Include algorithm descriptions
  include_math: true        # Include mathematical formulas
```

#### How It Works

1. **Paper Content Analysis**: Parse paper text to identify algorithm sections
2. **Algorithm Extraction**: Extract key algorithm steps and pseudo-code blocks
3. **Math Rendering**: Convert LaTeX formulas to readable pseudo-code
4. **Output**: Embed pseudo-code in the paper notes under "Pseudo-code" section

#### Output Format

```markdown
### Paper Title
- **Authors**: ...
- **Abstract**: ...

#### Pseudo-code
```
# Algorithm Name
Input: ...
Output: ...

1. Step one description
2. Step two description
3. Step three description
```

# Mathematical Formulas
- Formula 1: description
- Formula 2: description
```

#### Notes

- Pseudo-code generation is computationally intensive, use `top_n` to limit
- Works best with papers that have clear algorithm descriptions
- Falls back gracefully if paper doesn't contain extractable algorithms

## Output

Generates file: `{yyyy-mm-dd}_paper_{topic}.md`

```markdown
# yyyy-mm-dd_paper_{topic}

## Overview
- **Overall Trend**: {summary of overall research trend}
- **Research Hotspots**:
  - **Hotspot 1**: brief description
  - **Hotspot 2**: brief description
  - **Hotspot 3**: brief description

## Paper List
### Paper Title
- **Authors**: author list
- **Links**: [PDF](url) | [Code](url) | [DOI](url)
- **Tags**: #Tag1 #Tag2
- **Abstract**: abstract content
- **Core Contributions**:
  - contribution point 1
  - contribution point 2
- **Pseudo-code** (optional):
  ```
  # Algorithm Name
  Input: ...
  Output: ...
  1. Step one
  2. Step two
  ```

### Another Paper
...
```

---
```

## Data Sources

Search in priority order:
1. arXiv - Latest papers
2. Semantic Scholar - Popular papers (fallback)
3. DBLP - Top conference papers (fallback)
4. Agent Self-Search - Final fallback

## Dependencies

- Python 3.x
- PyYAML
- Network connection
- (Optional) PyMuPDF for image extraction