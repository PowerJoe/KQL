# Sentinel Analytics Rules

Scheduled Analytics Rules for Microsoft Sentinel. These run on a defined frequency and generate alerts or incidents when triggered.

## Usage

Analytics Rules are created in the Microsoft Sentinel portal under **Configuration → Analytics**. Each rule requires:

- A KQL query against the Log Analytics workspace
- An alert name, severity, tactics, and techniques
- A query schedule (frequency and lookback period)
- An alert grouping / incident creation policy

## Rule Header Format

All rules in this directory follow the standard header format defined in the root README, with `Platform: Sentinel` and `Frequency` set to the detection schedule.
