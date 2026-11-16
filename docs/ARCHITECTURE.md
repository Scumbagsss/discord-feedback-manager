# Discord Feedback Triage — architecture notes

> This is a **suggested technical boundary for a private-source module**, not a claim that all components are implemented or active in a particular deployment.

## Objective

Community feedback easily disappears in chat or gets repeatedly submitted. Structured intake and a staff queue help distinguish new ideas from reviewed, deferred and rejected feedback while preserving enough context to act.

## Conceptual responsibilities

**1. Feedback form.** Collect a structured feedback message through a form.

**2. Input validation.** Validate text and create a persistent record.

**3. SQLite queue.** Route the record to a private staff review surface.

**4. Staff decision.** Allow authorized reviewers to record a decision.

**5. Updated triage view.** Update the displayed queue without losing historical context.

## Review risks and recommended tests

| Concern | Failure mode | Verification to add |
|---|---|---|
| Duplicate submissions | Players may submit the same idea several times | Use clear duplicate/merge policy and synthetic fixtures |
| Long input | Feedback can contain excessive text or unsafe mentions | Validate length, sanitize display and mention policy |
| Review concurrency | Two staff members may review simultaneously | Use optimistic locking or a transactional state change |
| Recovery after restart | Persistent UI may become detached from stored records | Test view reconstruction and missing messages |

## Integration and permissions

The Discord interaction layer should treat its inputs as untrusted. A server-side handler must establish the principal, check authorization for the concrete operation and return user-safe errors. The persistence or external API adapter is separately responsible for safe updates, retries and recovery. The public `src/public_interface.py` is only a surface sketch; **none of these safeguards can be confirmed by running it**.

## Production/public boundary

No real member IDs, credentials, channel IDs, private schemas, moderation rules or live logs should appear in this repository. The architectural context belongs to the wider [DeadCity platform case study](https://github.com/Scumbagsss/BOT). For a separately developed runnable example, see the [ticket workflow backend](https://github.com/Scumbagsss/advanced-discord-ticket-bot).
