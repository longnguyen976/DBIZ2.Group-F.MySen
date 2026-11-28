# ADR-004: Dedicated background scheduler and FCM for streak jobs and alerts

| Field | Value |
|---|---|
| Status | Accepted (after Lesson 7) |
| Date | Lesson 7 |

**Context.** Activity modeling for daily loyalty streaks (`AD-UC-05`) and marketing campaigns (`UC-09`) showed that the system must autonomously detect users whose daily login streak is at risk before midnight, reset expired streaks at 00:00, and dispatch scheduled promotional notifications without manual admin intervention.

**Decision.** Add a background Scheduler component inside the business layer to trigger timed cron jobs, connected to a Notification Adapter backed by Firebase Cloud Messaging (FCM) for push notifications.

**Consequences.** Timed streak resets and evening reminder alerts run reliably on schedule. External push delivery logic is decoupled behind the Notification Adapter, allowing notification templates and channels to evolve without modifying core gamification or campaign services.