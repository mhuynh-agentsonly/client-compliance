# Contract renewal & contract end date — client portal

Decisions. Client-side scope only.

**Why.** Some countries cap how long a contractor engagement can run on a single
signature. Past that, the agent has to sign the same agreement again. Separately, legal
may need a contract to stop being valid on a fixed date. Today a project contract is
signed once and runs forever — the only way to change either is to upload a new document,
which creates a new contract when nothing has changed.

**What.** Project Managers can set a renewal schedule and an end date on a project
contract. When an agent's renewal comes round they're asked to sign the stored document
again. No re-upload, no new record.

**Where.** Client portal → project → Legal → the Upload legal contract wizard. Project
contracts only. No Admin changes.

**Three new controls**, per document, in step 2 of the wizard:

- **Signing Requirement** — new applicants / existing agents / both
- **Set an end date** — off by default; on, one date. The contract takes effect on
  publish, so there is no start date to choose.
- **Require contract renewal** — off by default; on, a number of months between 1 and 60

## Decisions

1. **The clock runs from each agent's own signature date**, not the upload date.
   50 agents means 50 different renewal dates. This is the most likely thing to be built wrong.
2. **Audience and renewal don't conflict.** Signing Requirement sets who signs initially;
   renewal follows any signature that exists.
3. **Offlining a contract closes that record for good.** It cannot be republished — to put
   the contract back you create a new record and publish it. For offlined contracts, any
   pending renewals will be invalidated. Any renewal an agent is currently being asked for
   is cancelled at the same time.
4. **No grace period.** A renewal coming round raises the same state as a newly added
   contract — only the wording changes, to say this is the document they already signed.
5. **The interval is a plain number box, not a preset list.** Range from 1 to 60 months.
6. **The interval has no default.** The field starts **empty** and the wizard won't continue
   until a number is entered.
7. **Review step shows each optional setting only when it's ticked in the previous step.**
8. **Settings can't be changed after publish.** To change a renewal interval or an end date,
   offline the contract and publish the document again as **a new record**.

## What the end date adds

1. **One new status: Expired.** The table goes from Active / Offline to Active / Expired /
   Offline. Status becomes derived rather than stored, because an end date flips the chip
   overnight with nobody touching the row.
2. **Expired behaves like Offline, without being it.** The contract stops being enforced
   and the row menu drops to View only. The difference is that it ran out on its own rather
   than being stopped.
3. **The renewal interval must fit inside the contract.** A 12-month renewal on a contract
   ending in 6 months would never fire — the setting would look live and do nothing. The
   wizard refuses it and names the longest interval that fits.
4. **An end date can't be extended.** Same reason as decision 8 — publish a new record instead.

> [!WARNING]
> **Clients can't see whose renewal is coming.** Renewal dates live per agent. Nothing in
> Legal or the Agents list surfaces "8 of 40 agents have a renewal outstanding." Expiry
> sharpens this: unlike a newly added contract, an end date is predictable, so a client
> should be warned before agents are affected rather than after. Probably out of scope for
> a minor feature — but it will be the first thing a PM asks for once this ships.

## Open: what happens agent-side when a contract expires

An expired contract is the opposite of an outstanding one — it asks for nothing. So it must
not raise a signing prompt: there is no action the agent could take, and blocking them
behind a signature they cannot give is the one thing to avoid. Access to that project
probably does have to stop, since the agent would otherwise be working with no current
agreement, but the screen has to say it is the client's move, not theirs. Needs a decision
before build.

## Prototype

[Prototype 🔗](https://mhuynh-agentsonly.github.io/client-compliance/client-legal-contracts-prototype-with-dates.html)
