---
name: meo-mai-moi
description: Use for tasks involving the Meo Mai Moi platform, especially when an agent needs to read or update pets, weights, vaccinations, medical records, microchips, helper profiles, or placement workflows through the documented API. Also use when the user asks how to authenticate to Meo Mai Moi, how to structure API calls, or how to safely automate pet-management actions.
---

# Meo Mai Moi

Use the Meo Mai Moi API deliberately. Prefer documented `/api/*` endpoints and avoid inventing routes or payload fields.

## Load the right reference

Read only the reference file you need:

- Read `references/api.md` for authentication, response format, documented endpoints, and API usage rules.
- Read `references/domain-model.md` for pet, helper, relationship, and placement concepts.
- Read `references/workflows.md` for task playbooks and safe execution patterns.

## Working rules

- Prefer read operations first to discover current state before proposing or making updates.
- Treat personal access tokens as bearer secrets. Load them from a local env file; never paste them into chat, commits, logs, or generated docs.
- Assume the stable external contract is the documented pet-management slice unless the user explicitly says to work with another route and you can verify it.
- Send `Accept: application/json` and `Authorization: Bearer <token>` for PAT-backed requests.
- Expect the standard API envelope. Success is usually `{ success: true, data, message? }`. Errors are usually `{ success: false, data: null, message, error?, errors? }`.
- Respect documented abilities: `read`, `create`, `update`, `delete`.
- Do not assume PATCH support for pets. Use the documented methods.
- For destructive changes like delete, ownership transfer, or status changes with real-world consequences, confirm intent unless the user clearly asked for that exact action.
- When the task needs domain nuance, read the domain reference before acting. The app has relationship-based access and placement-specific lifecycle rules that are easy to mangle if you wing it.

## Output expectations

When helping with Meo Mai Moi tasks:

- Be explicit about which endpoint and method you are using.
- Surface important constraints before risky writes.
- If the contract looks incomplete for the requested task, say so plainly and stop guessing.
- Prefer compact examples over long tutorials.
