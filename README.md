# shared-info-poc

A proof of concept for a team knowledge base that AI agents read while working in other projects. Agents only read it; people add entries on GitHub.

- [AGENTS.md](./AGENTS.md): how an agent uses this repo
- [knowledge/](./knowledge/): the entries, one fact or pattern per file
- [SETUP.md](./SETUP.md): how an agent connects a project to this repo

## Set up EMA

Once per person. In EMA, open **Settings → Agent permissions**, turn on **Allow LLM to use my git credentials**, and select **Save**. Wait for the "LLM git permissions saved" message before starting a chat.

## Connect a project

Once per project. Open the project in EMA and paste this into a chat:

```
Connect this project to our shared knowledge base.
If /tmp/shared-info-poc is missing, run: git clone https://github.com/alexcarol/shared-info-poc.git /tmp/shared-info-poc
Otherwise run: git -C /tmp/shared-info-poc pull --ff-only
If that fails, stop and show me the git error. Otherwise follow /tmp/shared-info-poc/SETUP.md.
```

The agent adds a "Shared info" section to the project's `AGENTS.md`, and lists what's in the knowledge base. Push the change with **Sync → Push code**, then start a new chat. From then on, every chat in that project syncs this repo before its first reply.

If the agent shows a git error, check [Set up EMA](#set-up-ema).

## Demo it

Use an EDS project in EMA that isn't connected yet. Each step needs a **new chat**: the agent loads the project's instructions, and syncs this repo, when a chat starts.

1. **Before connecting**, send:

   > triage https://www.fairtrade.net/africa-en/why-fairtrade.html

   EMA answers in its own words, at length, or starts working on the page.
2. **Connect the project** (see [Connect a project](#connect-a-project)) and push the change. In a new chat, send the same message. The reply is only the card. This is what it gave in our test:

   ```
   🟢 Ready · ~1 h
   Reuses: hero, columns · New: none
   Watch out: nothing obvious
   Next: say "migrate it" to start
   ```
3. **Change the rule.** On GitHub, edit [knowledge/triage.md](./knowledge/triage.md): change `1 h for the page` to `3 h for the page`. Send the same message in a new chat: the hours go up (`~3 h`). Change it once, and every teammate's agent follows.

To show steps 1 and 2 side by side, connect the project on a separate branch and switch branches between chats.

## Why a shared triage card helps

- **Same shape every time:** cards from different people and pages compare at a glance in Slack or a ticket.
- **Triage a list:** `triage` ten URLs, sort by light, start with the 🟢 ones.
- **On a client call:** a straight answer in seconds instead of a paragraph.
- **Consistent estimates:** when a pilot gives real rates, one edit here moves everyone's numbers.
- **Lessons stick:** add "forms are always the watch-out" after one bites the team, and no one's agent forgets it.
