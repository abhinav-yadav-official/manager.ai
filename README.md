# manager.ai

Generate quarterly developer evaluations from Phabricator data.

`manager.ai` fetches closed tasks, task comments, and Differential revisions for selected users, then sends that data to Claude with a strict writing prompt to produce concise manager-style quarterly feedback.

## What it does

- Accepts a quarter start date
- Selects users via:
  - `--users` (explicit usernames), and/or
  - `--teams` (Phabricator project/team names)
- Applies filters for team-based selection:
  - skips inactive/disabled users
  - skips members of `Dev Leads` and `Product Managers`
  - skips exact username `aditya` and usernames containing `prathis`
  - only includes members of `Engineering`
- Fetches:
  - closed Maniphest tasks since quarter start
  - task comments for those tasks
  - Differential revisions since quarter start
  - latest diff content per revision (truncated for context size)
- Generates markdown evaluations with sections:
  - `## Delivery`
  - `## Quality`
  - `## Behavior`

## Requirements

You need these tools available in your shell:

- `python3`
- `arc` (Arcanist), authenticated for Conduit calls
- `claude` CLI, authenticated

You also need to run this script from inside a Mercurial repo under a `devel` directory. The script validates:

- current path includes `devel`
- `devel/.hg` exists
- `devel/auction` exists

## Usage

```/dev/null/usage.txt#L1-4
manager.ai <quarter_start_date> [--users user1,user2] [--teams team1,team2]

manager.ai "1 Jan 2026" --users "naman.gupta,aman.azeem"
manager.ai "1 Jan 2026" --teams "team-morpheus"
manager.ai "2025-10-01" --teams "team-delta" --users "naman.gupta"

