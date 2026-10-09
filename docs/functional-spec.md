# Technology-neutral functional specification — draft v0.1

A **small backend benchmark workload**, not the feature-complete sports application. All implementations must expose behaviorally equivalent REST and WebSocket interfaces. The contract is **not frozen** until an OpenAPI file, WebSocket schema, and evaluator agree.

## Entities
User, Group (private), Membership, Role, Permission, MembershipRole, Channel, Message, Event, EventRegistration, WaitlistOffer, Notification, OutboxEvent. Use stable opaque identifiers. Scope memberships and permissions by group.

## Functional stories
### Groups / authorization
- Users create a private group, join via a valid invitation, and list groups where they are members.
- A membership may have multiple roles; effective permissions are the union of role grants within that group.
- Role checks apply to protected operations and never bleed across groups.
- Unauthorized actors must not access private group messages/events or member lists.

### Events / capacity / FIFO
- Authorized organizer creates event with start time, optional capacity, signup deadline, and RSVP state.
- RSVP rules support confirmed, waitlisted, pending offer, declined/cancelled.
- With capacity N, **at most N confirmed seats** at every committed state, including concurrent requests.
- When capacity is full, new registrations enter a deterministic FIFO waitlist, with stable ordering/tie-breaking.
- A confirmed cancellation releases a seat and offers it to the first eligible waitlisted member.
- Offer must have an explicit acceptance deadline. Acceptance is idempotent and atomic; duplicate/late acceptance cannot overbook.
- Expired/declined offer makes the seat available to the next eligible member, without double promotion.
- All state transitions maintain an audit record and produce durable notification intents.

### Messaging
- Authorized group members can create/read channel messages with durable server-side identifiers, sender, channel, timestamp, and sequence/cursor.
- WebSockets deliver new messages to connected authorized members. Disconnected members retrieve persisted history after reconnect.
- Replayed client requests with the same idempotency key must not duplicate persisted messages.
- Define and document order, at-least-once vs exactly-once claims, ack/reconnect behavior and visibility of edits/deletes before freezing contract.
- Prohibit access to channels outside the authenticated member's scope.

### Notifications
- Event cancellation recipients default to confirmed **and waitlisted** participants.
- Waitlist spot offers notify the eligible person. Their status changes to confirmed only on acceptance.
- Store durable notification intent, retry safely, and avoid duplicate logical notifications on processing retries.
- For benchmark purposes, a simulated/in-process notification transport may be used **only if the same contract and test behavior apply to every language**. No dependency on real Apple/Android push services.

## Shared requirements
- PostgreSQL persistence for durable entities.
- Consistent date/time conventions (UTC on wire); clear validation and error semantics.
- Authentication mechanism and token handling defined centrally and identically.
- Migrations and repeatable seed fixture.
- Health/readiness endpoints; graceful shutdown; structured logging; no plaintext secrets.
- Security tests: cross-group authorization, broken membership, request validation, replay protection.
- Concurrency tests: same last seat, competing cancellations/offers, duplicate requests and expiry races.

## Deferred to production platform
Public discovery, organizations, sport-specific runtime plugins, payment processing, mobile UI, image storage, production APNs/FCM push and advanced moderation. These should not creep into this benchmark.

## Contract freeze checklist
- Define concrete routes, schemas, HTTP statuses, pagination, authentication, error shape, idempotency rules.
- Specify WebSocket connect/auth/subscription/ack/reconnect and message ordering.
- Define clock/time-control method for testing offer expiry.
- Define notification simulator and delivery expectations.
- Pre-register datasets, load profiles, and observability requirements.
