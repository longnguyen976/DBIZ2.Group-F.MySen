# ADR-002: Token-based authentication (JWT) with Role-Based Access Control

| Field | Value |
|---|---|
| Status | Accepted |
| Date | Lesson 4 |

**Context.** MySen serves three distinct user groups—Visitors, Commercial Partners, and Park Administrators—each requiring different permissions across ticketing, loyalty wallets, partner booth operations, and system analytics. Visitors also expect fast onboarding via social accounts or phone OTP without complex password management.

**Decision.** Implement stateless JWT (JSON Web Token) authentication supporting OAuth2 social login (Google) and phone/email OTP verification, paired with server-side Role-Based Access Control (RBAC) enforcing `VISITOR`, `PARTNER`, and `ADMIN` roles on every API route.

**Consequences.** API requests remain stateless and easy to scale across services. Unauthorized cross-role access (such as a visitor accessing admin campaign endpoints) is blocked at the business layer, while sensitive user credentials are protected via standard OAuth2 delegation and hashed tokens.