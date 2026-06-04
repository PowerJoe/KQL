# Instructions for Claude Code

Add the BlueHammer detection rules to this repository.

1. Create the following folder structure under the repo root:

   threat-intelligence/cve/bluehammer/analytics/
   threat-intelligence/cve/bluehammer/hunting/

2. Add these files (contents provided in this drop):

   analytics/bluehammer-rstrtmgr-oplock.kql
   analytics/bluehammer-vss-sam-access.kql
   analytics/bluehammer-suspicious-services-exec.kql
   analytics/bluehammer-vss-enumeration.kql
   hunting/bluehammer-all-ttps-combined.kql
   hunting/bluehammer-rstrtmgr-baseline.kql
   README.md  (in the bluehammer/ folder)

3. If the repo's root README has a rule index/table, add a BlueHammer
   (CVE-2026-33825) section linking to threat-intelligence/cve/bluehammer/.

4. Stage, commit and push:

   git add threat-intelligence/cve/bluehammer
   git commit -m "Add BlueHammer (CVE-2026-33825) detection and hunting rules"
   git push origin main

Do not modify the KQL query bodies — they are tuned. Only adjust paths if
the repo uses a different top-level layout than threat-intelligence/.
