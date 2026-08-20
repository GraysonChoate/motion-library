# THE TOOLROOM

## Upload one file. This one.

**`TOOLROOM-UPLOAD-THIS.html`**

Upload it to a fresh chat — Claude, ChatGPT, Gemini — and send exactly:

```
IMPLEMENT PHASE ONE — theirsite.com
```

Nothing else. Do not add instructions, preferences, context or encouragement.
Every one of those is already in the file, and adding your own weakens it.

## What comes back

**A link.** Click it and the page is live in your browser. Ask for changes and
the same link updates — you refresh. **You never download anything to look at
it.** The file comes at the end, once you have approved the page and want to
send it to somebody. Ask for it then.

If the first thing it gives you is a file, it skipped BLD 04. Say:
*"preview it and give me a link."*

## Nothing else in this repo goes into a build chat

| File | What it is |
|---|---|
| `TOOLROOM-UPLOAD-THIS.html` | **The tool.** The only file you upload. |
| `HANDOFF.md` | Context for a session that is going to EDIT the Toolroom. Never for a build. |
| `builds/` | Finished concepts. Output, not input. |
| `NOTES-effects-tab.md` | Notes about the Effects tab. Reference only. |

Anything named `*-FIX-PROMPT.md` or `RETROSPECTIVE-*.md` is a document about
the tool, aimed at the session that edits it. **Feeding one to a build chat
makes the AI start editing the Toolroom instead of building a website.** Keep
them in an `old/` folder, out of reach.

## Updating it

This file is the canonical copy. Edit it here, commit, push, and republish to
the same artifact URL so the link never goes stale:

https://claude.ai/code/artifact/b5dc9473-a0f7-4658-82f5-1495fa86af65

One file, one folder, one link. That is the whole system.
