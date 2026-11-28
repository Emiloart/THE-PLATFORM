# Open Questions and Decision Register

This document separates current direction from matters that still require investigation or an explicit decision.

## Recorded direction

| ID | Topic | Current direction | Status |
|---|---|---|---|
| D-003 | Experience model | One coherent platform with dedicated experiences for different activities. | Confirmed direction |
| D-004 | Social and media feeds | Text/social, video, and audio should have distinct experiences rather than being indiscriminately mixed. | Confirmed direction |
| D-005 | Marketplace | Managed and verified commerce, beyond a basic peer-to-peer classifieds model. | Confirmed direction |
| D-006 | Marketplace role | The platform intends to act as an intermediary in commerce, with trust and transaction protections. Exact operating and legal model remains open. | Direction; details open |
| D-007 | Services | Include restaurant ordering, transportation, appointments, and other on-demand services. | Confirmed direction |
| D-008 | Work and gatherings | Include meetings, appointments, movie parties, conferences, and other group experiences. | Confirmed direction |
| D-009 | Identity | HDIP is intended to provide the verification foundation for verified participation. | Confirmed direction |
| D-010 | Monetisation | Aim for monetisation eligibility from successful required identity verification, subject to method-specific requirements. | Confirmed direction |
| D-011 | Revenue | Do not rely only on ads and premium subscriptions; commerce and services are important potential revenue engines. | Confirmed direction |
| D-012 | Scope | The full feature vision is long-term; implementation will be staged. | Confirmed direction |
| D-013 | Individual accounts | Each individual has one primary platform account; multiple personal profiles are not required for different roles. | Confirmed |
| D-014 | Organisation accounts | Organisations have independent accounts, add individuals, and assign scoped roles and permissions. | Confirmed |
| D-015 | Organisation membership | Individuals may belong to multiple organisations; relevant identity and affiliation claims are established through HDIP, while the platform governs permissions. | Confirmed direction |
| D-016 | Multiple organisation owners | Organisations may have multiple authorised owners, with authority established through HDIP and explicit recovery, transfer, and succession rules. | Confirmed direction; rules open |
| D-017 | Acting context | Users can switch between their individual account and an organisation they are authorised to represent; the active identity must remain clear. | Confirmed |
| D-018 | Minors | Kids Mode and age-appropriate access are based on the user's HDIP-established age grade. | Confirmed |
| D-019 | Guardian privileges | HDIP-established parents or guardians can assign privileges to relevant sections, subject to platform policy and applicable law. | Confirmed direction |
| D-020 | Navigation | Persistent primary navigation is user-configurable; users can arrange and prioritise destinations. | Confirmed |
| D-021 | Global search | Search spans the platform and supports destination-specific filters. | Confirmed |
| D-022 | Background activity | Music and audio continue during navigation, with pause and stop controls. | Confirmed |
| D-023 | Offline video | Offline viewing has a dedicated mode that can switch off other platform activities, subject to content rights and technical constraints. | Confirmed direction |
| D-024 | Progressive enablement | Keep initial installation lean; optional experience modules and role-specific tools can be installed or enabled when needed. Delivery mechanisms may differ by operating system and app-distribution rules. | Confirmed product direction; implementation open |
| D-025 | Social relationships | Support following and mutual friendship relationships where appropriate. | Confirmed |
| D-026 | Communities | Users can create and manage communities with membership, administration, moderation, and governance. | Confirmed |
| D-027 | Visibility | Individuals can choose public or private visibility; organisations have appropriate visibility controls. | Confirmed |
| D-028 | Communication | Support direct and group messaging, organisation-to-customer communication, community channels, voice and video calls, and further communication capabilities. | Confirmed direction |
| D-029 | Encryption | Encryption policy varies by communication type and use case. | Confirmed direction; policy details open |
| D-030 | Social video routing | A video attached to a social post is represented by a preview in the feed and opens in the dedicated video experience. Related videos follow playback; back navigation returns to the originating post. | Confirmed |
| D-031 | Mobile client strategy | Flutter is not an approved platform decision. Axiely's media requirements require a comparative evaluation of native-first and cross-platform/hybrid approaches before selection. | Open; Flutter proposal challenged |
| D-032 | Media-critical client capabilities | Background audio, offline video, live streaming, synchronised watch experiences, media-session integration, downloads, and lifecycle behaviour must be evaluated as core native-platform requirements. | Confirmed architectural constraint |

## Open product questions

### Identity, accounts, and verification
- What exact HDIP proofs or credentials are needed for each role and organisation type?
- How are revoked, expired, compromised, or disputed credentials handled?
- What information is disclosed to the platform, and what can be verified through selective disclosure?
- What are the detailed rules for organisation ownership, transfer, succession, and recovery?
- How are organisational invitations, membership changes, role assignment, and permission revocation governed?
- Which actions require fresh or step-up authorisation?
- How should age-grade policies and guardian-assigned privileges vary by activity and jurisdiction?

### Navigation and experience
- What is the default destination and layout before users customise navigation?
- What limits, if any, apply to pinned destinations?
- How should global search rank and group results across destinations?
- Which activities beyond audio can continue in the background, and under what controls?
- What exactly does offline video mode disable, and how does a user exit it?
- How should notifications be prioritised across social, commerce, work, and finance?
- Which capabilities belong in the core installation, optional modules, or on-demand resources?
- How should optional modules be installed, updated, disabled, removed, and kept compatible across operating systems and app-store policies?

### Social and communication
- Which contexts use following, mutual friendship, or both, and what are the rules for each?
- What organisation visibility controls are required?
- What messaging encryption, retention, backup, reporting, and moderation policies apply to each communication type?
- What are the boundaries between personal and business messaging?
- What community discovery, membership, moderation, and governance models are needed?
- How should users return to the exact originating feed position after opening a video preview?

### Mobile architecture and platform capabilities
- Should Axiely use native-first clients (Swift for iOS and Kotlin for Android), a shared cross-platform application with native media modules, or another hybrid approach?
- Which media-critical destinations and capabilities require native UI and lifecycle ownership rather than platform-channel bridges?
- What are the measurable acceptance criteria for background audio, offline video, live streaming, synchronised watch parties, playback continuity, media controls, battery use, memory use, and low-connectivity behaviour on both operating systems?
- Which code, domain logic, design tokens, API contracts, and business rules can be shared without compromising native media control?
- What is the staffing, delivery-time, maintenance, and testing cost of each mobile approach across iOS and Android?

### Video, audio, and live
- Which upload formats, durations, resolutions, and streaming protocols are supported?
- What content licensing and rights-management model applies to music, audiobooks, films, and synchronised movie parties?
- What creator revenue calculations and reporting are required?
- How are copyright claims, takedowns, appeals, and repeat infringement handled?
- What live-stream latency, moderation, and recording policies are required?

### Marketplace and services
- Which product categories are allowed or restricted?
- What merchant due diligence is required by category and jurisdiction?
- What is the platform's role in payment custody, escrow-like protection, refunds, and chargebacks?
- Who is responsible for fulfilment, shipping, returns, warranties, and product authenticity?
- Which logistics providers or platform-operated delivery capabilities are contemplated?
- How are service-provider licensing, insurance, qualifications, and background checks handled?
- What is the initial scope for food ordering and transportation?
- How are disputes between customers, merchants, restaurants, drivers, and providers resolved?

### Finance and monetisation
- Is the wallet a stored-value product, a payment interface, or a ledger of balances held by licensed partners?
- Which licensed financial institutions and payment providers are required in each market?
- Which financial activities will the platform itself perform, and which will partners perform?
- How are creator, merchant, and service-provider earnings calculated and settled?
- What are the rules for reserves, refunds, chargebacks, taxes, and negative balances?
- Which monetisation methods are available to each account role and jurisdiction?

### Meetings, events, and collaboration
- What are the meeting size, duration, recording, and storage limits?
- Which calendar and conferencing integrations are required?
- How will ticketing, access control, refunds, and event organiser verification work?
- What licensing or rights are required for movie parties and other synchronised media experiences?
- Are collaborative documents, tasks, and workspaces in scope for the first major product phases?

### Trust, safety, privacy, and operations
- What are the platform's moderation policy and appeal model?
- Which actions require human review?
- What is the reputation model, and how can it resist manipulation?
- What privacy and data residency commitments will be made?
- What support coverage and service-level targets are required?
- What audit and transparency reporting should users and businesses receive?

### Global operations
- Which launch jurisdictions are considered first?
- Which languages and currencies are initial priorities?
- What local rules affect payments, commerce, food, transport, identity, privacy, and media licensing?
- Which capabilities require country-specific partners?

## Technical decision discipline

The earlier broad technology-stack recommendation is a proposal, not an approved implementation baseline. Flutter is specifically not approved as the primary mobile framework. The mobile-client strategy must be evaluated against Axiely's actual media requirements before a decision is recorded. Do not describe a candidate technology as selected until the comparison, validation criteria, and decision rationale are documented.

## Decision discipline

An item becomes a binding decision only when it is explicitly reviewed and recorded as such. Discussion, analogy to another platform, and feature brainstorming are not sufficient by themselves to establish a final requirement.
