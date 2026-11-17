# Connect a project to shared info

Steps for an agent connecting the project it's working in to this knowledge base. People start it with the prompt in the [README](./README.md#connect-a-project).

1. Add the section below at the end of the project's `AGENTS.md`, at the project root, creating the file if it's missing. If it already has a `## Shared info` section, replace that section instead, so there's only ever one.
2. Don't commit or push.
3. Reply with:
   - the file you changed
   - the entries in [knowledge/README.md](./knowledge/README.md), each with its trigger and what it does
   - this line, as is: "Push this change with **Sync → Push code**, then start a new chat: the project's instructions load when a chat starts."

The section to add:

```markdown
## Shared info
Team knowledge lives in `alexcarol/shared-info-poc`, a separate repo. Never copy it into this project or commit it here.
- Before your first reply in a chat, sync it: if `/tmp/shared-info-poc` is missing, `git clone https://github.com/alexcarol/shared-info-poc.git /tmp/shared-info-poc`; otherwise `git -C /tmp/shared-info-poc pull --ff-only`.
- Then read `/tmp/shared-info-poc/AGENTS.md` and follow it.
- If the sync fails, start your reply by saying so, with the git error, and carry on without it.
```

The clone goes to `/tmp` because EMA only lets its agent write inside the project and `/tmp`. EMA's `/tmp` is lost when its pod restarts, so the agent clones again in the next chat.
