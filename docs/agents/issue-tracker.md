# Issue tracker: GitHub

Issues and specs for this repo live in GitHub Issues at
`Cit1zeN4/agent-workflow`. Use `gh` from this checkout.

## Operations
- Create: `gh issue create --title "..." --body-file <file>`
- Read: `gh issue view <number> --comments`
- List: `gh issue list --state open --json number,title,body,labels`
- Comment: `gh issue comment <number> --body-file <file>`
- Label: `gh issue edit <number> --add-label "..."` or `--remove-label "..."`
- Close: `gh issue close <number> --comment "..."`

Use `docs/agents/triage-labels.md` for label names.
Publishing a spec or ticket means creating a GitHub issue;
fetching one means reading it with `gh issue view`.
PRs as a request surface: no.

## Wayfinding
A map is one issue labelled `wayfinder:map`; child tickets are
linked as sub-issues where available, otherwise from a task list in
the map. Record blockers with native issue dependencies where
available, otherwise a `Blocked by: #...` line. Claim a ticket by
assigning it before work; close it after recording the result.
