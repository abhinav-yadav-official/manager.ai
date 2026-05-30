<div align="center">

# DevFeedbackAI

**Generate quarterly developer feedback from Phabricator or git activity.**

[![Release](https://img.shields.io/github/v/release/abhinav-yadav-official/DevFeedbackAI?style=for-the-badge)](https://github.com/abhinav-yadav-official/DevFeedbackAI/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)]()

</div>

## Overview

DevFeedbackAI collects engineering activity for selected developers, then asks a language model to turn that raw work history into concise quarterly feedback. It currently supports:

- **Phabricator**: closed Maniphest tasks, task comments, and Differential revisions.
- **Git**: local repository commit history, commit messages, and changed file stats.

The output is markdown with `Delivery`, `Quality`, and `Behavior` sections.

## Features

- **Provider-based activity fetch**: use `--provider phabricator` or `--provider git`.
- **Flexible selection**: pick developers with `--users`; Phabricator also supports `--teams`.
- **Repo-local git support**: point at any local git checkout with `--repo`.
- **Configurable model command**: defaults to `claude -p`, configurable through `.env`.
- **Tracked example config**: copy `.env.example` to `.env` for local settings.

## Installation

```sh
git clone https://github.com/abhinav-yadav-official/DevFeedbackAI.git
cd DevFeedbackAI
cp .env.example .env
```

Prereqs:

- Python 3.
- A model CLI configured locally. By default this is `claude -p`.
- For Phabricator: `arc` on `PATH`, authenticated for Conduit.
- For git: a local git repository with commit history.

## Usage

Phabricator:

```sh
./dev-feedback-ai 2026-01-01 --provider phabricator --teams Engineering
./dev-feedback-ai 2026-01-01 --provider phabricator --users alice,bob
```

Git:

```sh
./dev-feedback-ai 2026-01-01 --provider git --repo /path/to/repo
./dev-feedback-ai 2026-01-01 --provider git --repo /path/to/repo --users "Alice <alice@example.com>,bob@example.com"
```

The old executable name still works:

```sh
./manager-ai 2026-01-01 --provider git --repo /path/to/repo
```

## Configuration

`.env` is loaded automatically when present.

```sh
DEVFEEDBACKAI_PROVIDER=git
DEVFEEDBACKAI_GIT_REPO=/path/to/repo
DEVFEEDBACKAI_MODEL_COMMAND=claude -p
```

## License

[MIT](LICENSE) © 2026 Abhinav Yadav
