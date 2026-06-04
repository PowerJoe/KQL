# VSCode GitHub Token Theft — Hunting Queries

Proactive hunting queries for the VSCode GitHub token theft attack. Run manually or schedule in Advanced Hunting.

## Queries

| Query | Description |
|---|---|
| `vscode-token-theft-full-chain-hunting.kql` | Correlates extensions.json drop, workspace extension install, and GitHub API enumeration per device. Two or more signals is high confidence. |
| `vscode-token-theft-ipynb-followed-by-network.kql` | Finds devices where a Jupyter notebook was accessed and VSCode made an external call within 15 minutes — matches the ~10 second exploit timing. |

## Usage

`vscode-token-theft-ipynb-followed-by-network.kql` is the most targeted hunt — the 15-minute time window between notebook open and external callout is tight enough to eliminate most legitimate noise. Start here for incident response triage. Use `vscode-token-theft-full-chain-hunting.kql` for broader retrospective coverage.
