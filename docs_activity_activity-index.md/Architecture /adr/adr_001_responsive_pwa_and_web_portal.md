# ADR-001: Responsive mobile web app (PWA) and unified web portal

| Field | Value |
|---|---|
| Status | Accepted |
| Date | Lesson 4 |

**Context.** Park visitors interact with MySen primarily on smartphones while walking outdoors (scanning checkpoint QR codes, viewing the 2.5D map, showing e-tickets and F&B vouchers). Meanwhile, park administrators and commercial partners manage campaigns, analytics, and space rental workflows on desktop browsers. Maintaining separate native iOS and Android codebases would exceed DBIZ3 team capacity.

**Decision.** Build a single responsive web application with Progressive Web App (PWA) capabilities optimized for mobile viewports (`375px` baseline) for visitors, alongside a unified desktop-responsive web portal view for administrators and commercial partners.

**Consequences.** Visitors can access MySen immediately via browser or QR code without app-store installation friction while still using device camera and GPS APIs. Native mobile apps are excluded from scope, keeping the frontend on a single shared codebase within DBIZ3 capacity.