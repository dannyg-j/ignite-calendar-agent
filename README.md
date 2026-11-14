# Ignite Calendar Agent Starter

This repository contains:

- `ignite-agent-instructions.md` - instruction set for the M365 Copilot Agent Builder agent
- `my ignite event source.docx` - redacted template source document (no personal schedule data)
- `scout-prompts.md` - sanitized Scout collector prompt template

## 1. Refresh the source document with Scout (manual run)

1. In Scout, sign in to Microsoft 365 and open Ignite in browser automation.
2. Collect your current **My Event / My schedule** entries from Ignite.
3. Update `my ignite event source.docx` with the latest snapshot content.
4. Ensure the document includes:
   - snapshot timestamp
   - retrieval status (Complete/Partial)
   - daily schedule rows
   - direct conflicts / comparison groups
5. Save the updated `.docx` to your approved private location.

## 2. Create the M365 Copilot Agent Builder agent

1. Open **Microsoft 365 Copilot Agent Builder** and create a new custom agent.
2. Set the agent instruction text to the contents of `ignite-agent-instructions.md`.
3. Add `my ignite event source.docx` as a knowledge source.
4. Validate with test prompts:
   - compare overlapping sessions
   - list direct conflicts for a selected day
   - show availability gaps with caveats
5. Publish only after responses consistently include source-grounded answers and snapshot timestamps.

## 3. Operational notes

- Treat the `.docx` source as a snapshot, not live event access.
- Re-run Scout refresh whenever schedule changes are expected.
- Keep private schedule outputs in private storage; publish only redacted artifacts to public repositories.
