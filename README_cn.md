# Eureka

[English](./README.md) | [中文](./README_cn.md)

![Eureka](./assets/logo.jpg)

> 学术论文研究工作流工具

独立的论文搜索和 HTML 汇报生成工具集合。

## Skills

### eureka-paper-search

多数据源论文搜索工具，支持自动回退。

- **功能**:
  - 从 arXiv、Semantic Scholar、DBLP 搜索
  - 自动回退机制
  - 可配置研究兴趣
  - 生成结构化笔记（Obsidian/Markdown）

- **用法**:
  ```
  /eureka-paper-search llm_agent
  /eureka-paper-search memory_skills
  /eureka-paper-search 2026-03-17 reasoning
  ```

### eureka-paper-html

从论文数据生成美观的 HTML 汇报。

- **功能**:
  - 两种设计模板：简约（白色）& 赛博（暗黑）
  - 响应式布局
  - 动画效果（赛博风格）
  - 无障碍优化

- **模板**:
  - `minimal.html` - 简约瑞士风格
  - `cyberpunk.html` - 暗黑模式带渐变和动画

- **用法**:
  ```
  /eureka-paper-html --input results.json --output report.html
  /eureka-paper-html --topic llm_agent --date 2026-03-17
  ```

## 安装

将 skills 复制到你的 Claude Code skills 目录：

```bash
cp -r skills/eureka-paper-search ~/.claude/skills/
cp -r skills/eureka-paper-html ~/.claude/skills/
```

## 配置

编辑每个 skill 中的 `references/preference.md`：

- 研究兴趣（关键词、主题）
- 输出目标（Obsidian/Markdown/HTML）
- 数据源偏好

## 设计系统

eureka-paper-html 在 `references/templates/` 提供两个模板：

| 模板 | 描述 | 文件 |
|------|------|------|
| **minimal** | 简洁白色背景，瑞士风格 | `minimal.html` |
| **cyberpunk** | 暗黑模式，带渐变效果和动画 | `cyberpunk.html` |

两个模板都生成包含以下内容的报告：
- 概览：总体趋势、研究热点
- 论文列表：作者、链接、标签、摘要、核心贡献

**默认**：简约风格

## 许可证

MIT