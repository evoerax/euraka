# Eureka Paper Search Configuration

## Language Setting
language: "zh"

## Output Target Configuration
output_target:
  # Options: "obsidian", "markdown"
  type: "obsidian"
  
  # Obsidian configuration
  obsidian:
    vault_path: "/Users/leon/files/Agent-Vault"
    directory: "paper_daily"
  
  # Markdown configuration (alternative)
  markdown:
    output_dir: "/your/custom/path"

## Data Source Configuration
data_sources:
  - name: "arXiv"
    enabled: true
    priority: 1
    categories: ["cs.AI", "cs.LG", "cs.CL", "cs.CV"]
  
  - name: "Semantic Scholar"
    enabled: true
    priority: 2
    fallback: true
  
  - name: "DBLP"
    enabled: true
    priority: 3
    conferences: ["ICLR", "NeurIPS", "ICML", "CVPR"]
  
  - name: "Agent Self Search"
    enabled: true
    priority: 0
    description: "Fallback when other sources fail"

## Research Interests
research_interests:
  - topic: "llm_agent"
    keywords:
      - "LLM"
      - "large language model"
      - "agent"
      - "autonomous"
      - "tool use"
      - "function calling"
      - "MCP"
      - "A2A"
      - "multi-agent"
      - "skill"
    priority: high

  - topic: "memory_skills"
    keywords:
      - "memory"
      - "skill"
      - "agent"
      - "reflection"
    priority: medium

  - topic: "reasoning"
    keywords:
      - "reasoning"
      - "chain of thought"
      - "self-consistency"
    priority: medium

## Search Configuration
search:
  max_results: 50
  top_n: 10
  recency_days: 30
  hot_days: 365

## Feature Configuration

### Image Extraction (Optional)
image_extraction:
  enabled: true
  # Priority: "arxiv-source" (download source package) | "pdf" (extract from PDF) | "both"
  priority: "arxiv-source"
  # Number of top papers to extract images from
  top_n: 3
  # Output directory for images
  images_dir: "20_Research/Papers/{topic}/images"

### Pseudo-code Generation (Optional)
pseudo_code:
  enabled: true
  # Number of top papers to generate pseudo-code for
  top_n: 3
  # Include algorithm descriptions
  include_algorithms: true
  # Include mathematical formulas in pseudo-code
  include_math: true

## Scoring Weights
scoring:
  relevance: 0.40
  recency: 0.20
  popularity: 0.30
  quality: 0.10

## Output Configuration
output:
  directory: "paper_daily"
  filename_format: "yyyy-mm-dd_paper_{topic}"
  include_abstract: true
  include_pseudo_code: true
  generate_detailed_report: true
  top_n_for_detailed: 3