# Technical Architecture and Decision Records

**Status:** Initial architecture proposal and decision register. No implementation stack in this document is approved merely by being listed.
**Product:** Axiely

## 1. Purpose

This document captures technical direction, architectural constraints, candidate technologies, and decisions that require validation. It is not a final implementation specification. Product requirements remain authoritative in the product vision, principles, feature catalogue, and decision register.

The architecture must support one coherent platform with distinct product destinations, shared identity and policy foundations, and independently evolvable domains. It must not turn every destination into a disconnected application or force materially different workloads into one generic execution model.

## 2. Architecture drivers

The following requirements materially influence the architecture:

- One primary individual account and independent organisation accounts, with explicit acting context and scoped permissions.
- HDIP-backed identity and credential verification, with platform-owned authorisation and policy enforcement.
- Distinct social, video, audio, commerce, service, booking, collaboration, and event experiences.
- Persistent navigation and preservation of context when moving between destinations.
- Background audio that remains controllable while users navigate elsewhere.
- Offline video viewing in a dedicated mode that can disable other platform activity.
- Live media and synchronised watch experiences, including timing, playback coordination, and rights enforcement.
- Progressive feature enablement without fragmenting identity, permissions, or platform governance.
- Global operation with market-specific legal, payment, privacy, media-rights, and service constraints.
- Security, privacy, auditability, resilience, and operational support as baseline requirements.

## 3. Architectural shape

The proposed logical structure is:

1. **Client experiences:** mobile, web, and later desktop surfaces.
2. **Platform shell:** session, navigation, destination discovery, notifications, shared interaction conventions, and module lifecycle.
3. **Platform core:** identity integration, organisation context, authorisation, policy, consent, audit, and user preferences.
4. **Product domains:** social, communication, media, commerce, services, bookings, collaboration, monetisation, discovery, and AI.
5. **Shared infrastructure:** transactional data, events, search, analytics, object storage, media processing, and observability.
6. **Infrastructure and operations:** deployment, networking, security controls, regional operations, backup, and disaster recovery.

Logical domain boundaries do not require every domain to become an independent microservice at the outset. Begin with explicit ownership and contracts; extract independently deployed services when workload, fault isolation, security, scaling, or team ownership justifies the operational cost.

## 4. Mobile client strategy: decision open

### 4.1 Why this is a first-order decision

The earlier recommendation of Flutter as the primary mobile framework is **not approved**. Axiely is materially more media-intensive than a conventional content or social application. Background audio, offline video, live streaming, and synchronised watch experiences depend on operating-system media frameworks, background execution rules, storage behaviour, DRM and content-rights constraints, audio focus, interruptions, notifications, and lifecycle management.

A design that places the main application in a cross-platform runtime and repeatedly crosses into native code for its most demanding experiences may create a fragmented ownership model. It can increase debugging complexity at precisely the boundaries where playback reliability and platform integration matter most. This risk must be tested, not assumed away.

### 4.2 Candidate approaches

These are architecture candidates for evaluation, not founder-approved decisions.

#### Option A: Native-first clients

- Swift and the relevant Apple platform frameworks for iOS.
- Kotlin and Android media/platform APIs for Android.
- Native ownership of media playback, downloads, background execution, live media integration, synchronised viewing, and media lifecycle.
- Shared API contracts, domain specifications, design tokens, backend services, and test scenarios.
- Evaluate Kotlin Multiplatform or generated/shared libraries only for well-bounded non-UI logic where they provide a clear net benefit.

**Advantages:** strongest direct access to platform capabilities, lifecycle behaviour, media frameworks, and debugging tools; fewer cross-runtime boundaries in critical paths.

**Costs and risks:** two client implementations, greater per-platform engineering and maintenance effort, duplicated UI work, and a need for disciplined parity testing.

#### Option B: Native application shells with selectively shared non-media layers

- Swift and Kotlin own the application shell, navigation integration, lifecycle, permissions, and media-critical destinations.
- Shared contracts, validation, selected domain logic, networking utilities, or other carefully chosen non-UI components may be implemented through a shared-code approach.
- Media experiences remain native unless a specific component proves otherwise through testing.

**Advantages:** preserves native control while reducing duplication in selected areas.

**Costs and risks:** shared-code boundaries can become complicated; platform-specific behaviour still needs separate implementation and testing. Sharing must not become an abstraction that blocks native capability.

#### Option C: Cross-platform shell with isolated native media experiences

- A cross-platform framework such as Flutter owns suitable general-purpose destinations and shared shell UI.
- Video, audio, offline downloads, live media, and watch-party playback are implemented as native experiences or native-owned modules.
- Integration contracts define navigation, state restoration, playback hand-off, authentication, permissions, and error handling.

**Advantages:** potentially faster delivery and greater UI reuse for non-media destinations.

**Costs and risks:** bridge and lifecycle complexity; duplicated expertise across Dart and native code; integration failures during navigation and app lifecycle transitions; risk that the supposedly isolated native media areas expand until the cross-platform layer provides limited benefit.

### 4.3 Evaluation criteria

No option should be selected by framework popularity or a small demo. Build representative technical spikes on current supported iOS and Android versions and compare:

- Background audio continuity during navigation, screen lock, interruptions, calls, and process lifecycle changes.
- Playback controls and media-session/lock-screen integration.
- Offline download integrity, resumability, storage management, expiry, and rights enforcement.
- Video playback performance, adaptive streaming, memory pressure, and battery use.
- Live-stream startup, latency, reconnection, and network transitions.
- Watch-party synchronisation, drift correction, host hand-off, and recovery after interruption.
- Navigation hand-off between social previews and the dedicated video experience, including exact return context.
- Accessibility, picture-in-picture where supported, audio focus, subtitles, and device compatibility.
- Crash isolation, observability, testability, release coordination, and upgrade risk.
- Engineering cost, team availability, delivery time, and long-term maintenance across both platforms.

The selected approach must include documented acceptance thresholds and a failure-mode analysis. A prototype that merely plays a video is insufficient evidence.

### 4.4 Provisional architectural constraint

Until a decision is made, the architecture must preserve the option for native ownership of every media-critical capability. Avoid designing product contracts that assume Flutter, Dart, or any other cross-platform runtime is the permanent owner of media playback and lifecycle.

## 5. Backend and service technology candidates

The following are candidates from the initial architecture proposal. They are not final selections:

| Area | Candidate | Qualification |
|---|---|---|
| Backend services | Go | Candidate primary language; validate against team capability and service requirements |
| Web client | Next.js, React, TypeScript | Candidate web stack |
| AI and data science | Python | Candidate for model orchestration, evaluation, and data workflows |
| Performance/security-critical components | Rust | Use selectively where justified |
| Primary transactional data | PostgreSQL | Candidate system of record; define domain ownership and isolation |
| Cache and ephemeral state | Redis | Introduce for measured caching and coordination needs |
| Event streaming | Kafka or managed event infrastructure | Select based on throughput, replay, ordering, and operational requirements |
| Search | OpenSearch or managed search | Select based on relevance, scale, and operational burden |
| Analytics | ClickHouse or managed analytical store | Introduce for analytical workloads, not as a second transactional source of truth |
| Object storage | S3-compatible storage | Media and file storage; assess residency, lifecycle, and egress economics |
| Media processing | FFmpeg and managed media services | Evaluate build-versus-buy for transcoding and live workflows |
| Real-time media | WebRTC and a managed or operated media platform | Validate latency, reliability, scale, recording, and regional coverage |
| Identity protocols | OIDC, OAuth 2.1, WebAuthn/passkeys | Integrate with HDIP and platform account lifecycle; protocol choice does not replace authorisation |
| Authorisation | Relationship-based and policy-based authorisation | Evaluate OpenFGA/Zanzibar-style models and Cedar-like policy evaluation against real permission cases |
| Observability | OpenTelemetry with compatible metrics, logs, and tracing backends | Standardise telemetry contracts and privacy controls |
| Infrastructure | Managed containers initially; Kubernetes when justified | Do not adopt orchestration complexity before operational need |
| Infrastructure as code | OpenTofu or an equivalent | Pin versions, review plans, and protect state |
| Edge and delivery | CDN and edge security provider(s) | Keep core product logic portable and assess regional performance |

## 6. Platform core and trust boundaries

HDIP is the identity and credential verification foundation. It can establish claims about individuals, organisations, age grades, guardianship, affiliations, qualifications, licences, and other supported credentials.

Axiely remains responsible for:
- Resolving the Axiely account and active acting context.
- Mapping verified claims to platform roles and relationships.
- Evaluating resource- and action-specific permissions.
- Enforcing age, guardian, organisational, and jurisdictional policies.
- Managing sessions, consent, revocation response, and account recovery.
- Recording security-relevant decisions and administrative actions.

A verified claim must not automatically grant broad platform permissions. For example, verified employment or organisational affiliation is not equivalent to finance, staff-management, or administrator authority. Apply least privilege and purpose limitation.

## 7. Data and service boundaries

- Establish domain ownership before choosing database-per-service.
- Keep transactional records authoritative in their owning domain.
- Use explicit APIs and versioned events for cross-domain interaction.
- Design idempotency, retries, ordering, deduplication, and reconciliation for asynchronous workflows.
- Do not use analytics stores as transactional authorities.
- Define retention, deletion, export, residency, encryption, backup, and recovery per data class.
- Separate private communications, identity evidence, financial records, media rights metadata, and business records through access controls and operational boundaries.

## 8. Media architecture requirements

Media must be designed as a platform capability with separate ingestion, processing, storage, delivery, playback, rights, and analytics concerns.

Specific workflows require independent design:
- Audio playback that survives permitted navigation and background states.
- Offline video with download integrity, device storage policy, expiry, and rights enforcement.
- Adaptive on-demand video delivery.
- Live streaming with latency, moderation, recording, and reconnection policy.
- Watch parties with session coordination, synchronisation, access control, and licensed-content restrictions.
- Social-feed video previews that hand off to the dedicated video experience and restore the originating post context.

Do not assume one media provider or protocol will satisfy every workflow. Validate provider portability, regional coverage, cost, DRM/rights support, and operational responsibility.

## 9. Delivery and operational principles

- Start with a small number of deployable units and strict domain boundaries.
- Prefer managed infrastructure where it reduces undifferentiated operational work without creating unacceptable lock-in.
- Use infrastructure as code, reviewed changes, automated tests, staged deployment, rollback, and auditable production access.
- Define service-level indicators and objectives for critical user journeys, especially authentication, message delivery, media startup, playback continuity, order placement, and booking confirmation.
- Design graceful degradation for partial outages and low-connectivity conditions.
- Test backup restoration and disaster recovery, not merely backup creation.
- Keep security threat modelling, privacy review, abuse controls, and incident response within each domain's delivery process.

## 10. Decisions required before implementation baseline approval

1. Select the mobile client strategy after comparative spikes against the criteria in section 4.
2. Confirm the initial web and desktop strategy and the degree of shared UI.
3. Define backend service boundaries and the first deployable topology.
4. Establish data classification, domain ownership, and regional data requirements.
5. Select media delivery, live media, and offline rights-management providers or operating models.
6. Specify HDIP integration contracts, credential lifecycle handling, and authorisation architecture.
7. Establish reliability, security, privacy, performance, and cost targets.
8. Validate the technology choices against team skills, hiring availability, operational capacity, and target markets.

## 11. Change control

A technology listed as a candidate is not an approved dependency. A decision becomes approved only when its rationale, alternatives, consequences, validation evidence, and owner/status are recorded in the decision register. Product requirements must not be silently weakened to accommodate a preferred framework.
