---
relations:
  role: entrypoint
  domain: documentation
  upstream:
    - REPO_INDEX.md
    - docker-compose.yml
  downstream: []
---
# Claire de Binare

Welcome to the Claire de Binare repository. This project is a complex system for algorithmic trading, featuring a microservices-based architecture, advanced data analysis, and a sophisticated governance model.

## Overview

This repository contains all the necessary components to run and develop Claire de Binare, including:

- **Microservices:** A suite of services for handling different aspects of the trading process, such as signal generation, execution, risk management, and data persistence.
- **Infrastructure:** Infrastructure-as-Code (IaC) for setting up the required environment, including database schemas, monitoring dashboards, and deployment configurations.
- **Governance:** A comprehensive set of documents defining the project's constitution, policies, and operational guidelines.
- **Tooling:** A collection of scripts and tools to aid in development, deployment, and maintenance.

## Getting Started

To get started with this project, you will need to have Docker and Python installed. The `docker-compose.yml` file in the root directory defines the services required for local development.

For a detailed index of the repository, please refer to the `REPO_INDEX.md` file.

## Automation Tools

- **Repo Relocator:** `tools/cdb_repo_relocator.py` watches the Working repo root, filters non-user artifacts, and moves them into the Docs repo (copy → verify → delete) while committing each relocation so the Working tree stays clean.
- **Tool Runner:** `tools/run_all_tools.py` executes every Python helper listed in `tools/tool_manifest.json`, groups them by category, and aggregates exit codes for deterministic quality signals.
- Combine both with `scripts/run_docs_sync.py` for pre-commit, CI, or manual runs; it runs the relocator first, then the tool runner, and can emit JSON reports for downstream automation.
