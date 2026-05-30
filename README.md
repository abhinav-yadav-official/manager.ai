<div align="center">

# ManagerAI

**Generate quarterly developer evaluations from Phabricator activity.**

[![Release](https://img.shields.io/github/v/release/abhinav-yadav-official/ManagerAI?style=for-the-badge)](https://github.com/abhinav-yadav-official/ManagerAI/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)]()

</div>

## Overview

ManagerAI pulls a quarter's worth of Phabricator activity — closed tasks, task comments, and Differential revisions — for selected engineers, then uses a language model to write concise, manager-style quarterly feedback. The model summarisation is the core of the tool: it turns raw activity into structured `Delivery` and `Quality` write-ups.

## Features

- **Flexible selection** — pick engineers by `--users` and/or `--teams` (Phabricator projects).
- **Team filters** — skip inactive/disabled accounts, Dev Leads, Product Managers; include only Engineering members.
- **Activity fetch** — closed Maniphest tasks, their comments, and Differential revisions (with truncated diffs) since the quarter start.
- **Model-generated evaluations** — markdown per engineer with `## Delivery` and `## Quality` sections, produced under a strict writing prompt.

## Installation

Prereqs: Python 3.x, Phabricator Conduit access, a model API key.

```sh
git clone https://github.com/abhinav-yadav-official/ManagerAI.git
cd ManagerAI
# configure Conduit token + model API key
```

## Usage

```sh
./manager-ai --quarter-start 2026-01-01 --teams Engineering
./manager-ai --quarter-start 2026-01-01 --users alice bob
```

## License

[MIT](LICENSE) © 2026 Abhinav Yadav
