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
