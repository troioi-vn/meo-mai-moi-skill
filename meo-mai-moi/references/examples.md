# Install and Example Prompts

## Install in OpenClaw

Put the skill folder in one of these locations:

- `<workspace>/skills/meo-mai-moi/`
- `<workspace>/.agents/skills/meo-mai-moi/`
- `~/.openclaw/skills/meo-mai-moi/`

Minimal layout:

```text
meo-mai-moi/
├── SKILL.md
└── references/
    ├── api.md
    ├── domain-model.md
    ├── examples.md
    └── workflows.md
```

After installing, start a new session or restart the gateway so OpenClaw reloads skills.

Useful checks:

```bash
openclaw skills list
openclaw agent --message "List my Meo Mai Moi pets"
```

## Token setup

Store the Meo Mai Moi PAT in a local env file outside git.

Example:

```env
API_KEY=your_pat_here
```

The agent should load it from a local env file and never commit or echo the token back into chat unless the user explicitly asks to reveal it.

## Example user prompts

These are good natural-language triggers for the skill:

- "List my pets from Meo Mai Moi."
- "Show me the current profile for Miu on Meo Mai Moi."
- "Add a new weight entry for Bánh Bao: 4.3kg today." (Agent should call the live API with `weight_kg` and `record_date`.)
- "Update this pet's description but keep everything else unchanged."
- "Check whether my Meo Mai Moi API key still works."
- "Explain what helper profiles are on Meo Mai Moi."
- "Help me understand whether this placement request is active or pending transfer."
- "Use Meo Mai Moi to add a vaccination record for my cat."

## Example agent behavior

Good behavior:

- Read current state first.
- Use documented routes.
- Match payload field names to the verified live contract, especially for nested health records.
- Confirm destructive actions.
- Re-read after writes.
- Explain state transitions for placement tasks.

Bad behavior:

- Invent undocumented endpoints.
- Use `PATCH` for pet updates without proof.
- Delete or transfer ownership casually.
- Expose PAT secrets in logs, chat, or commits.

## Suggested one-line setup note for users

"Use the Meo Mai Moi skill whenever I ask you to manage my pets, health records, helper profiles, or placement workflows through the documented API. Load my local API token from env, use read-first workflows, and avoid undocumented routes."
