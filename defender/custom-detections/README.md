# Custom Detection Rules

Scheduled Custom Detection Rules for Microsoft Defender XDR. These rules run on a defined frequency and automatically generate alerts or incidents when triggered.

## Usage

Custom Detection Rules are created in the Microsoft Defender portal under **Hunting → Custom detection rules**. Each rule requires:

- A KQL query targeting one of the supported tables
- An alert title, severity, and category
- A response action (optional): isolate device, collect investigation package, restrict app execution

## Rule Header Format

All rules in this directory follow the standard header format defined in the root README, with `Platform: MDE` and `Frequency` set to the detection schedule.
