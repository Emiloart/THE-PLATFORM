# Contributing to Axiely

Thank you for considering a contribution to Axiely.

This guide defines how contributions are proposed, discussed, reviewed, and integrated. Its purpose is to protect product coherence, technical quality, security, and the integrity of project decisions as the work grows.

## 1. Current project stage

Axiely is in product discovery and definition, with an initial technical architecture proposal. The feature catalogue is intentionally broad. Not every listed capability is fully specified, prioritised, technically validated, or approved for implementation.

Contributors must check the current documentation and decision records before treating an idea, technology, workflow, or implementation detail as a requirement.

The principal project documents are:

- [Product vision](docs/PRODUCT_VISION.md)
- [Feature catalogue](docs/FEATURE_CATALOGUE.md)
- [Product principles](docs/PRODUCT_PRINCIPLES.md)
- [Open questions and decisions](docs/OPEN_QUESTIONS.md)
- [Technical architecture](docs/TECHNICAL_ARCHITECTURE.md)

## 2. Contribution principles

All contributions are expected to follow these principles:

1. **Preserve product intent.** Changes should strengthen the coherent, multi-destination experience without collapsing distinct product domains into one generic experience.
2. **Respect decision status.** Distinguish confirmed requirements, proposals, assumptions, experiments, and unresolved questions. Do not silently promote a proposal into an approved decision.
3. **Prefer evidence.** Support technical recommendations with relevant documentation, reproducible experiments, benchmarks, threat analysis, or operational evidence.
4. **Keep scope explicit.** Avoid unrelated refactors, speculative features, and broad rewrites within narrowly scoped contributions.
5. **Design for security and privacy.** Consider identity, authorisation, data exposure, abuse, retention, auditability, and failure behaviour as part of the change.
6. **Consider global operation.** Avoid assumptions that only hold in one jurisdiction, language, currency, network environment, or app distribution channel.
7. **Document consequential changes.** Update the relevant product or technical documentation when behaviour, requirements, interfaces, dependencies, or decisions change.
8. **Do not invent project facts.** Do not claim a feature exists, a test passed, a provider is integrated, or a decision was approved unless the repository or verifiable evidence supports that statement.

## 3. Ways to contribute

### Product and research

Product contributions may include:

- Clarifying user journeys, workflows, constraints, and edge cases.
- Identifying dependencies between product destinations.
- Researching regulatory, accessibility, safety, privacy, or operational requirements.
- Comparing existing approaches and documenting trade-offs.
- Identifying ambiguity, contradiction, or missing acceptance criteria.

Research should identify its sources, publication dates where relevant, assumptions, limitations, and the markets or platforms to which it applies. Separate observed facts from interpretation and recommendations.

### Documentation

Documentation contributions should:

- Use precise, direct language.
- State whether content is confirmed, proposed, experimental, or unresolved.
- Preserve important context and rationale.
- Link related decisions and specifications where useful.
- Avoid duplicating authoritative information across multiple files.
- Update indexes and cross-references when adding or moving documents.

Do not rewrite established product decisions merely to make a document shorter. If a decision appears inconsistent or outdated, raise the discrepancy and explain the evidence.

### Engineering

Before implementation begins, check whether the relevant feature has an agreed scope and sufficient acceptance criteria. If not, propose the missing specification or raise the question before building on an assumption.

Engineering contributions should:

- Respect documented domain boundaries and ownership.
- Use established interfaces and conventions in the affected area.
- Include tests appropriate to the change.
- Handle validation failures, retries, timeouts, cancellation, and partial failure where relevant.
- Avoid unnecessary dependencies and premature distributed-system complexity.
- Include migrations and compatibility considerations when data or interfaces change.
- Avoid introducing a technology as a permanent platform dependency without an approved decision.

The technical architecture document contains candidate technologies and unresolved choices. A technology appearing there is not, by itself, approval to use it.

## 4. Before opening a pull request

1. Read the relevant product and technical documents.
2. Search existing issues and pull requests for related work.
3. Confirm that the proposed change has an agreed direction or clearly label it as a proposal.
4. For substantial work, open an issue or discussion describing the problem, proposed scope, alternatives, risks, and acceptance criteria.
5. Keep the contribution focused on one coherent change.
6. Do not include generated files, local configuration, credentials, private keys, tokens, or unrelated formatting changes.

For significant architectural changes, include the alternatives considered, operational consequences, security implications, migration path, and rollback strategy.

## 5. Pull request requirements

A pull request should provide:

- **Problem:** What is incorrect, missing, or being improved?
- **Scope:** What changes, and what is explicitly out of scope?
- **Approach:** How does the change work?
- **Decision status:** Is this implementing an approved decision, proposing a change, or recording an experiment?
- **Verification:** Which tests, checks, benchmarks, or manual scenarios were run?
- **Risks:** What compatibility, security, privacy, data, performance, or operational risks remain?
- **Documentation:** Which documents were updated, or why no documentation change is needed?

For user-facing changes, include relevant screenshots or recordings when they materially help reviewers. For API or data-contract changes, include representative request/response examples and compatibility implications.

Do not report checks as passing unless they were actually run and their results were observed. If a check could not be run, state that plainly.

## 6. Testing and quality

Choose verification proportional to the risk of the change.

- Unit tests for isolated logic and validation.
- Integration tests for database, service, and external-system boundaries.
- Contract tests for APIs and events.
- End-to-end tests for critical user journeys.
- Security tests for authentication, authorisation, input handling, data isolation, and abuse-sensitive workflows.
- Performance and resilience tests for latency-sensitive, high-throughput, media, and transaction-critical paths.

Tests should be deterministic where practical and should not depend on production credentials or uncontrolled external services. Document any manual verification and its limitations.

## 7. Security and privacy

Never commit:

- API keys, access tokens, passwords, private keys, certificates containing private material, or production connection strings.
- Real user identity evidence, private messages, payment data, or other sensitive personal information.
- Unredacted production logs, database exports, or private support records.

Use synthetic data in examples and tests. Report suspected vulnerabilities privately to the project maintainer rather than publishing exploit details in an issue or pull request. Do not test against systems or accounts without authorisation.

Security-sensitive changes must explain the trust boundary, attacker assumptions, authorisation behaviour, data handled, audit requirements, and failure modes.

## 8. Product and architecture decision records

A contribution that changes a confirmed product requirement or an approved technical decision must identify the affected decision record and provide the reason for changing it.

Where a decision is not yet settled:

- Record the question and relevant context.
- Present viable alternatives.
- Explain trade-offs and dependencies.
- Identify evidence still needed.
- Leave the status unresolved until the authorised project decision is made.

Experiments and prototypes should be labelled as such. Their results may inform a later decision but do not automatically establish production architecture.

## 9. Commit and branch practices

- Use descriptive branch names that communicate the work.
- Keep commits focused and messages specific.
- Avoid committing unrelated generated output or editor state.
- Rebase or update against the target branch when needed to resolve conflicts cleanly.
- Do not force-push shared branches unless explicitly coordinated.
- Do not merge your own pull request unless repository policy or explicit maintainer instruction permits it.

Suggested commit message format:

`<type>: <short description>`

Examples:

- `docs: clarify organisation permission boundaries`
- `feat: add community membership controls`
- `fix: prevent duplicate booking confirmation`
- `test: cover offline media recovery`
- `refactor: isolate notification policy evaluation`

These are examples, not a requirement to introduce a commit-linting tool.

## 10. Review and acceptance

Maintainers may request changes, additional evidence, narrower scope, or a separate proposal before implementation.

A contribution may be declined when it:

- Conflicts with confirmed product direction.
- Treats an unresolved proposal as an approved requirement.
- Introduces disproportionate complexity or unsupported dependencies.
- Weakens security, privacy, accessibility, reliability, or user control.
- Lacks sufficient tests or evidence for its risk.
- Duplicates existing work without a clear reason.
- Expands beyond its stated scope.

Review feedback should focus on correctness, maintainability, product coherence, and documented requirements.

## 11. Licensing and third-party material

Do not assume a project licence or contribution agreement that is not explicitly present in the repository. Before contributing third-party code, assets, datasets, fonts, models, or documentation, identify their source and licence and confirm that their use is compatible with the project.

Do not submit material whose ownership or permission to use it is unclear.

## 12. Questions

If the correct scope or decision status is unclear, raise the question before making a change that depends on an assumption. A concise proposal with alternatives and consequences is preferable to implementing an unapproved direction.

## 13. Attribution

human supervised developments should not be attributed to artificial intelligence as co developers, you can use them as tool but I want the repo to maintain human environment, simply put: I don't want to see coding agents listed as co developers.
