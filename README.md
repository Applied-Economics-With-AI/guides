# Guides for Applied Economics Research with AI & Big Data

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)](https://github.com/Applied-Economics-With-AI/guides/issues)

Welcome to the Applied Economics with AI Guides repository! This collection of guides is designed to help researchers and students in applied economics leverage cloud computing and AI tools to enhance their productivity and research capabilities.

These guides have been developed by [Peter John Lambert](mailto:p.j.lambert@lse.ac.uk) at the [London School of Economics](https://www.lse.ac.uk/), with contributions from researchers across the applied economics community.

## Table of Contents

1. [Introduction](#introduction)
2. [Guides](#guides)
   - [Setting Up a Google Cloud VM for R and Python with VSCode](#setting-up-a-google-cloud-vm-for-r-and-python-with-vscode)
   - [Mount Filestore on the GCP Instance](#mount-filestore-on-the-gcp-instance)
   - [Research Project Folder Structure (Recommended)](#research-project-folder-structure-recommended)
3. [Further Resources](#further-resources)
4. [Contributing](#contributing)
5. [Support](#support)

## Introduction

The field of applied economics is increasingly relying on large-scale data analysis and complex computational methods. This repository aims to provide step-by-step guides to help researchers set up powerful, cloud-based environments for their work, integrating tools like R, Python, and AI assistants.

Whether you're working with large datasets, running computationally intensive simulations, or simply looking for a more flexible development environment, these guides will help you get started with cloud computing in a research context.

## Guides

### Setting Up a Google Cloud VM for R and Python with VSCode

This comprehensive guide walks you through the process of setting up a virtual machine (VM) on Google Cloud Platform (GCP) for R and Python development using Visual Studio Code (VSCode). It covers:

- Creating a Google Cloud account and setting up a VM
- Configuring SSH for secure access
- Installing necessary tools and packages for R and Python
- Setting up VSCode for remote development
- Installing and using GitHub Copilot for AI-assisted coding

[📖 Read the full guide](./google-cloud-vm-setup/Setting%20Up%20a%20Google%20Cloud%20VM%20with%20VSCode.md)

### Mount Filestore on the GCP Instance

This guide explains how to automatically mount a Google Cloud Filestore on your GCP instance using a startup script. It includes:

- Preparing your environment
- Installing necessary utilities
- Creating a mount directory
- Adding a startup script for automatic mounting
- Verifying the mount
- Troubleshooting tips

[📖 Read the full guide](./cp-filestore-setup/Mount%20Filestore%20on%20the%20GCP%20Instance.md)

### Research Project Folder Structure (Recommended)

This guide proposes a simple, battle-tested directory structure for empirical research projects. It helps keep raw data immutable, derived data reproducible, scripts organised, and makes it easier to collaborate (including with AI assistants like Cline / Claude Code).

[📖 Read the full guide](./project-structure/Research%20Project%20Folder%20Structure.md)

## Further Resources

### Google Cloud Platform
- [Google Cloud Console](https://console.cloud.google.com/) - Main dashboard for managing your GCP resources
- [Google Cloud Pricing Calculator](https://cloud.google.com/products/calculator) - Estimate costs for your cloud setup
- [Google Cloud Free Tier](https://cloud.google.com/free) - Details on free credits and always-free resources
- [GCP Documentation](https://cloud.google.com/docs) - Official documentation for all GCP services
- [Compute Engine Documentation](https://cloud.google.com/compute/docs) - VM-specific documentation

### Development Tools
- [Visual Studio Code](https://code.visualstudio.com/) - Download and documentation
- [VSCode Remote Development](https://code.visualstudio.com/docs/remote/remote-overview) - Guide to remote development with VSCode
- [GitHub Copilot](https://docs.github.com/en/copilot) - AI-powered code completion

### Programming Languages
- [The R Project](https://www.r-project.org/) - Official R website
- [CRAN](https://cran.r-project.org/) - Comprehensive R Archive Network
- [Python.org](https://www.python.org/) - Official Python website
- [Anaconda](https://www.anaconda.com/) - Python distribution for data science

### Research Computing
- [The Turing Way](https://the-turing-way.netlify.app/) - Guide to reproducible research
- [Software Carpentry](https://software-carpentry.org/) - Computing skills for researchers
- [Research Computing at LSE](https://info.lse.ac.uk/staff/divisions/dts/help/guides-faqs/fasd-guides/Research-Computing) - LSE-specific resources

### Social Science Research Workflows (Code, Data, and Reproducibility)
- [Code and Data for the Social Sciences: A Practitioner's Guide (Gentzkow & Shapiro)](https://web.stanford.edu/~gentzkow/research/CodeAndData.xhtml) - Classic guide to automation, version control, directory structure, and project management
- [Social Science PhD Tech Stack (Kevin Bryan)](https://kevinbryanecon.com/techstack.html) - Practical guide to a modern research tech stack (version control, editors, AI tools, and reproducible workflows)
- [Project TIER Protocol](https://www.projecttier.org/tier-protocol/) - Widely used protocol for transparent and reproducible research in the social sciences
- [BITSS (Berkeley Initiative for Transparency in the Social Sciences)](https://www.bitss.org/) - Training and resources for open, rigorous, and reproducible social science
- [Code, Data, and Version Control: Best Practices for Economic Research (Brendan M. Price, 2023)](https://www.brendanmichaelprice.com/workflow/2023lectures/Price_BestPractices_Apr2023.pdf) - Slide deck with concrete best practices and common pitfalls

### AI for Research (Economists and Practitioners)

Below are a few resources that focus on **practical workflows, methodological tools, and hands-on guidance** for using modern AI (especially LLMs) in applied research. I’m intentionally avoiding “impact of AI on X” links here.

**Economics-focused resources**

- [Generative AI for Economic Research: Use Cases and Implications for Economists (AEA JEL)](https://www.aeaweb.org/articles?id=10.1257/jel.20231736) - Practitioner-oriented discussion of how generative AI can enter the research workflow
- [Social Science PhD Tech Stack (Kevin Bryan) — “Be Efficient with AI Tools” section](https://kevinbryanecon.com/techstack.html#ai-tools) - Practical tips on integrating AI tools into a reproducible workflow
- [Alexander W. Bartik, Arpit Gupta, and Daniel Milo: *The Costs of Housing Regulation: Evidence From Generative Regulatory Measurement* (PDF)](https://www.alexbartik.com/papers/GenRegMeasure_Sep142024.pdf) - Worked example: using generative methods for measurement in applied work
- [Stephen Hansen and coauthors: *Large Language Models in Economics* (CEPR DP19479)](https://cepr.org/publications/dp19479) - Methods and applications of LLMs in economics (measurement, classification, text)
- [Elliott Ash & Stephen Hansen: *Large Language Models in Economics* (PDF)](https://elliottash.com/wp-content/uploads/2024/10/Ash-Hansen-Large-Language-Models-Economics.pdf) - Short, readable PDF overview oriented toward economists
- [Inference for Regression with Variables Generated by AI or Machine Learning (arXiv:2402.15585)](https://arxiv.org/abs/2402.15585) - Guidance on inference when ML/AI generates regressors

**Hands-on / prompt engineering resources**

- [OpenAI Cookbook](https://cookbook.openai.com/) - Practical examples and patterns for working with LLMs
- [Anthropic: Prompt Engineering Overview](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) - Prompt engineering guidance for Claude
- [DeepLearning.AI: ChatGPT Prompt Engineering for Developers (course)](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) - Short, hands-on prompt engineering course
- [NVIDIA: Prompt Engineering Guide](https://www.nvidia.com/en-us/ai-data-science/generative-ai/prompt-engineering/) - Useful overview and practical patterns

**Practical cautions (highly recommended reading)**

- [The Turing Way: Reproducible Research](https://the-turing-way.netlify.app/reproducible-research/reproducible-research.html) - Reproducibility basics that become even more important when AI enters the workflow

## Contributing

We welcome contributions to improve these guides or add new ones! If you have suggestions, corrections, or want to contribute a new guide, please:

1. Fork this repository
2. Create a new branch for your changes
3. Submit a pull request with a clear description of your modifications or additions

For major changes, please [open an issue](https://github.com/Applied-Economics-With-AI/guides/issues) first to discuss what you would like to change.

## Support

If you have any questions or need assistance with these guides, please:

- [Open an issue](https://github.com/Applied-Economics-With-AI/guides/issues) in this repository
- Contact: [Peter John Lambert](mailto:p.j.lambert@lse.ac.uk) at LSE

---

We hope these guides help you enhance your research capabilities in applied economics. Happy coding!

*Last updated: January 2026*
