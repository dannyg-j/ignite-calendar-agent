# Scout Prompt (Sanitized)

This file contains the Scout prompt used to set up the Ignite collector workflow.

> Replace placeholders like `<DESTINATION_FOLDER_URL>` before running in your private environment.  
> This public version intentionally excludes personal identities and private Teams/SharePoint links.

---

## Prompt 1: Create / refresh `my ignite event source.docx`

```text
Scout prompt: Create my Ignite event source

Create a real Word document named my ignite event source.docx, with the document title My Ignite Event Source, for use as a knowledge source in a Microsoft 365 Copilot Agent Builder agent.

Destination folder: <DESTINATION_FOLDER_URL>

Purpose and boundaries
- Retrieve the complete saved Microsoft Ignite 2026 My Event schedule from https://ignite.microsoft.com/en-US/home.
- Read-only behavior: do not add/remove sessions, register, update profile, create Outlook appointments, download media, or send channel messages.
- If authentication/MFA is required, pause for interactive sign-in. Never request credentials/tokens in chat.

Retrieve and reconcile
1. Confirm event year and visible schedule owner display name from the website.
2. Retrieve all saved sessions across all event days (including lazy-loaded/paginated content).
3. Distinguish saved selections from public catalog/agenda content.
4. Preserve repeated session occurrences individually (use occurrence IDs or local refs like S001).
5. Verify portal timezone; default output timezone is America/Los_Angeles with explicit PST/PDT + UTC offset.
6. Preserve original displayed timestamps/timezone and include UTC when reliable.
7. Refresh fully (additions/removals/reschedules/location changes), not incremental append-only.

Word document structure
1. Snapshot and provenance
2. Daily schedule
3. Full session details
4. Direct conflicts (`startA < endB AND startB < endA`)
5. Comparison groups
6. Availability and caveats
7. Changes since previous successful snapshot

Saving and failure handling
- Update the same destination file when possible (preserve link/history).
- Partial/failed retrieval must not overwrite a previously complete snapshot.
- Empty schedule is valid only when My Event explicitly confirms no saved sessions with filters cleared.
- Reopen/read-back the saved Word file and report link, retrieval time, count, and limitations.
- Do not create recurring automation in this run.

Optional follow-up
- After a successful manual run, optionally propose hourly refresh (08:00-18:00 America/Los_Angeles) during verified Ignite event dates, with timezone/date range/approval behavior shown before activation.
```

## Suggested run order

1. Run Prompt 1 to create or refresh `my ignite event source.docx`.
2. In Agent Builder, attach the refreshed `.docx` as knowledge source.
