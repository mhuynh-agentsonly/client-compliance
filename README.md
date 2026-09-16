# Contract renewal — client portal

Decisions. Client-side scope only.

**Why.** Some countries cap how long a contractor engagement can run on a single
signature. Past that, the agent has to sign the same agreement again. Today a project
contract is signed once and that's it — the only way to make someone re-sign is to upload
a new document, which creates a new contract when nothing has changed.

**What.** Project Managers set a re-signing schedule on a project contract. When an
agent's clock runs out, they're asked to sign the stored document again. No re-upload,
no new row.

**Where.** Client portal → project → Legal → the Upload legal contract wizard. Project
contracts only. No Admin changes.

**Two new controls**, per document, in step 2 of the wizard and editable afterwards from
the row menu:

- **Signing Requirement** — new applicants / existing agents / both
- **Require periodic re-signing** — off by default; on, it gives 3 / 6 / 12 / 24 months
  or a custom 1–36

## Decisions

1. **The clock runs from each agent's own signature date**, not the upload date.
   50 agents means 50 different due dates. This is the most likely thing to be built wrong.
2. **Audience and renewal don't conflict.** Signing Requirement sets who signs initially;
   renewal follows any signature that exists.
3. **Offline contracts don't renew.**
4. **No grace period.** A due renewal raises the same state as a newly added contract —
   only the wording changes, to say this is the document they already signed.
5. **Default interval is 3 months, not 6.** With no country cap to validate against, the
   default should fail harmlessly: too short is friction, too long is the breach this
   feature exists to prevent. (The "Australia = 6 months" figure in the brief is
   unverified — worth confirming with legal.)
6. **Review shows re-signing only when it's on.** A "Not required" row on almost every
   publish was noise.
7. **Signing rules stay editable after publish.** The document can't change; the schedule
   can. Shortening an interval recomputes each agent's due date as their last signature +
   the new interval, so the confirm warns how many that makes immediately due.

> [!WARNING]
> **Clients can't see who is due.** Renewal dates live per agent. Nothing in Legal or the
> Agents list surfaces "8 of 40 agents are overdue." Probably out of scope for a minor
> feature — but it will be the first thing a PM asks for once this ships.

## Designs

[Feature — Legal (Figma)](https://www.figma.com/design/31OYHKGXthe9oLLssyOs77/Feature---Legal?node-id=1368-38558&t=vGT0kGaGWNLcZawo-11)
