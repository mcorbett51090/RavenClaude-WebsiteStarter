# Rules for agent sessions in this repo

## Ask the owner in modals, never in a prose list

Every decision, choice or go-ahead you need from the owner goes through the `AskUserQuestion`
tool, which shows a modal they cannot scroll past. Batch up to 4 questions per call, and use as
many calls as it takes.

- **Never end a reply with a list of open questions** ("Decisions for you", "Needs you", "Open
  questions"). Ask them as modals instead.
- **Recommended option first,** labelled "(Recommended)", and every option carries a one-line
  consequence, so the owner can answer without scrolling back.
- **Status that needs no answer stays in prose,** short. A modal is for a decision, not an update.
- **Record each answer** where the next session will find it, so nothing is asked twice.

Owner rule, added 2026-10-26: questions at the end of a long reply were being missed on a phone.
On a tool without `AskUserQuestion`, use its own blocking prompt; where none exists, put the
questions in one headed block at the top of the reply, not the end.
