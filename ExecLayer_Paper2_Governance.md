# Execution Layer Governance: A Technical Substrate for Global AI Safety

## From Risk Scoring to Runtime Enforcement

**James Benton**  
ExecLayer Inc., Wilmington, Delaware, United States
press@execlayer.io

---

## Abstract

Global AI governance frameworks increasingly rely on risk classification taxonomies and self-reported compliance mechanisms that cannot provide verifiable enforcement guarantees. Current approaches treat AI governance as a documentation and assessment problem rather than an execution control problem. This creates a fundamental verification gap: organizations can claim compliance with governance frameworks while lacking technical mechanisms to prevent non-compliant AI operations from executing.

This paper presents execution layer governance as an alternative paradigm that shifts enforcement from organizational process to technical infrastructure. Rather than classifying AI systems by risk level and trusting organizations to implement appropriate controls, execution layer governance imposes mandatory authorization validation at the operational boundary where AI intent transitions to real-world action.

We introduce the concept of **governed execution substrates**—technical infrastructure that provides deterministic enforcement of authority constraints, policy compliance verification, and cryptographically verifiable audit evidence. The paper examines how such substrates address structural limitations in current governance approaches, including the inability to verify compliance claims, cross-jurisdictional policy fragmentation, and post-incident attribution challenges.

Using ExecLayer as a reference implementation, we demonstrate how execution layer governance enables:

1. **Pre-execution permission verification** that prevents unauthorized operations rather than detecting them retrospectively
2. **Machine-verifiable compliance evidence** that regulatory bodies can validate without access to proprietary systems
3. **Cross-jurisdictional policy reconciliation** through declarative policy abstraction
4. **Immutable audit lineage** establishing accountability chains from operational outcomes to authorizing decisions

The paper evaluates execution layer governance against emerging regulatory frameworks (EU AI Act, ISO 42001, NIST AI RMF) and proposes integration pathways for international AI safety standards. We argue that execution layer governance provides essential technical infrastructure for translating governance intent into operational reality, transforming AI safety from an aspirational goal to an architecturally enforced property.

The implications extend beyond individual organizations to international AI governance: execution layer substrates could serve as technical foundation for treaty-level verification mechanisms, enabling nations to demonstrate AI system compliance through cryptographic evidence rather than trust-based assertions.

---

## 1. The Verification Crisis in AI Governance

### 1.1 The Current Governance Paradigm

Contemporary AI governance operates through a familiar pattern inherited from traditional software regulation: classify systems by risk level, document compliance procedures, conduct periodic audits, and respond to incidents when they occur. This model has served adequately for conventional information systems where operational boundaries are well-defined and execution authority is explicitly programmed.

AI systems fundamentally break this model.

When an AI agent decides to execute a database modification, initiate a financial transaction, or communicate sensitive information, that decision emerges from probabilistic inference over learned patterns rather than deterministic execution of explicitly authorized code paths. The authorization decision is implicit in model weights and prompt contexts rather than explicit in access control lists.

This creates what we term the **governance verification gap**: the inability to verify that an AI system's actual operational behavior aligns with documented governance commitments. Organizations can assert compliance with frameworks like ISO 42001 or the EU AI Act, but lack technical mechanisms to prove those assertions hold at execution time.

### 1.2 Why Risk Taxonomies Are Insufficient

Every major AI governance framework relies fundamentally on risk classification:

- **EU AI Act**: Four-tier risk taxonomy (unacceptable, high, limited, minimal) with requirements scaled by tier
- **NIST AI RMF**: Risk assessment and categorization driving control selection
- **ISO 42001**: Risk-based approach to AI management system requirements

The theory is sound: higher-risk systems receive more stringent oversight. The practice reveals structural problems:

**Classification Instability**: An AI system's risk level is not fixed but depends on deployment context, operational parameters, and evolving capabilities. A "limited risk" customer service chatbot becomes high-risk when granted database write access or financial transaction authority. Static classification cannot capture dynamic risk.

**Self-Assessment Failure**: Organizations classify their own systems' risk levels with obvious incentive misalignment. Under-classification reduces compliance burden. External auditors reviewing risk classifications lack visibility into actual operational behavior.

**Control Ambiguity**: Risk tiers specify *what* controls are required (logging, human oversight, transparency) but not *how* those controls are technically enforced. Organizations can document compliance while maintaining technical capability to bypass controls.

**Cross-Jurisdictional Incoherence**: Different jurisdictions classify identical systems differently based on local risk tolerance and regulatory philosophy. A single AI system operating globally faces fragmented, potentially contradictory requirements.

### 1.3 The Audit Theater Problem

Traditional compliance audits examine:
- Documentation of governance procedures
- Evidence of training completion
- Samples of system outputs
- Review of incident response records

What audits cannot examine:
- Whether documented controls actually prevent non-compliant operations
- Whether sampled outputs represent systematic behavior or cherry-picked examples
- Whether incident response records are complete or selectively disclosed
- Whether the audited system configuration matches production deployment

This creates **audit theater**: organizations demonstrate compliance through documentation while maintaining technical capability to execute non-compliant operations. Auditors verify that governance *processes exist*, not that governance *actually constrains execution*.

The problem intensifies with AI systems because traditional audit evidence (code review, configuration inspection) becomes uninformative. Reviewing model weights provides no insight into operational behavior. Analyzing training data reveals little about production responses to novel inputs.

### 1.4 Cross-Border Verification Impossibility

International AI governance faces unique challenges that domestic regulation does not:

**Sovereignty Barriers**: Nations cannot compel foreign organizations to provide unfettered access to AI systems for compliance verification. Cross-border audits require cooperation that geopolitical tensions may preclude.

**Technical Opacity**: Even with cooperation, verifying foreign AI system compliance requires technical expertise, access to proprietary infrastructure, and understanding of implementation details that organizations legitimately protect as trade secrets.

**Enforcement Asymmetry**: International governance frameworks lack enforcement mechanisms comparable to domestic regulation. Treaty violations may carry reputational costs but rarely face meaningful sanctions.

The result is governance based on trust: nations trust foreign organizations' compliance claims, foreign nations' regulatory oversight, and treaty signatories' good faith implementation. This trust assumption is increasingly untenable as AI systems operate across adversarial geopolitical boundaries.

### 1.5 The Incident Attribution Challenge

When AI systems cause harm—financial losses, privacy violations, discriminatory outcomes, safety failures—accountability depends on reconstructing authorization decisions from audit evidence. Current approaches fail systematically:

**Incomplete Audit Trails**: Organizations log events selectively. Critical authorization decisions may occur in components outside logging scope.

**Temporal Gaps**: Time between authorization decision and operational effect creates attribution ambiguity. Which policy version was in effect? Who held authority when execution occurred?

**Multi-Agent Obfuscation**: Complex AI workflows involving multiple agents create responsibility diffusion. Which agent's decision caused the harmful outcome? Did upstream agents delegate authority appropriately?

**Adversarial Tampering**: Sophisticated attackers manipulate audit logs to conceal unauthorized actions or shift blame. Without cryptographic tamper-evidence, logs cannot serve as authoritative evidence.

These attribution failures prevent effective accountability. Organizations claim unauthorized actions resulted from AI system "errors" rather than governance failures. Regulators cannot disprove these claims without access to comprehensive audit evidence—which organizations control.

### 1.6 The Case for Execution Layer Governance

The verification crisis demands a paradigm shift: from governance as organizational process to governance as technical infrastructure.

**Execution layer governance** positions enforcement at the operational boundary where AI intent transitions to system action. Rather than trusting organizations to implement controls, governance is architecturally imposed through mandatory authorization checkpoints that AI systems cannot bypass.

This shift provides several critical properties:

**Verifiable Enforcement**: Authorization decisions produce cryptographic artifacts that external parties can validate without access to internal systems.

**Pre-Execution Prevention**: Non-compliant operations are blocked before execution rather than detected retrospectively.

**Cross-Jurisdictional Portability**: Governance evidence is portable across regulatory frameworks through declarative policy abstraction.

**Adversarial Resistance**: Cryptographic binding and immutable audit structures resist manipulation even by privileged insiders.

The remainder of this paper formalizes execution layer governance, demonstrates how it addresses verification gaps in current frameworks, and proposes integration pathways for international AI safety standards.

---

## 2. Execution Layer Governance: Core Principles

### 2.1 Definition and Scope

**Execution layer governance** is the imposition of deterministic authorization constraints at the technical boundary where AI-generated intent is transformed into operational system actions. It operates as infrastructure rather than process—a technical substrate that makes governance violations architecturally difficult rather than merely policy-prohibited.

Three core principles define execution layer governance:

**P1: Intent-Execution Separation**  
AI systems generate operational intent (natural language descriptions, structured commands, API invocations) but do not directly execute those operations. Intent must pass through a governance layer that validates authority, verifies policy compliance, and generates audit evidence before execution authorization.

**P2: Fail-Closed Enforcement**  
The default state is denial. Operations execute only upon explicit authorization following successful validation. Authorization failures, policy conflicts, or validation errors block execution rather than proceeding with warnings.

**P3: Machine-Verifiable Evidence**  
Every authorization decision produces cryptographic artifacts that external parties can validate independently. Evidence includes authority chains, policy evaluation results, and execution outcomes—all bound through cryptographic signatures and tamper-evident structures.

### 2.2 Why "Execution Layer" Matters

The term "execution layer" is deliberate. Governance must enforce at the layer where intent becomes action—not at the intent generation layer (which may be opaque, probabilistic, and impossible to constrain) nor at the outcome assessment layer (which operates retrospectively after potential harm occurs).

Consider three possible enforcement points:

**Intent Generation Layer**: Attempting to prevent AI models from generating non-compliant intent through training, fine-tuning, or prompt engineering. This approach is fundamentally probabilistic—models may generate harmful intent despite training constraints. Enforcement is unreliable.

**Execution Layer**: Validating that operations about to execute are authorized according to applicable policies, regardless of how intent was generated. This approach is deterministic—unauthorized operations are blocked with cryptographic certainty. Enforcement is reliable.

**Outcome Assessment Layer**: Evaluating whether executed operations complied with governance requirements by analyzing outcomes. This approach is retrospective—harm has already occurred by the time non-compliance is detected. Enforcement is too late.

Execution layer enforcement is the only layer providing both reliability (deterministic prevention) and timeliness (pre-execution validation).

### 2.3 Governed Execution Substrates

A **governed execution substrate** is technical infrastructure implementing execution layer governance. It provides:

**Authorization Validation**: Mandatory checkpoints verifying that operations possess required authority before execution.

**Policy Evaluation**: Declarative policy frameworks evaluated against operations to determine compliance.

**Audit Generation**: Immutable, cryptographically verifiable records of authorization decisions and execution outcomes.

**Cross-System Coordination**: Enforcement operates consistently across distributed systems, heterogeneous infrastructure, and organizational boundaries.

Substrates operate as foundational infrastructure analogous to operating system security mechanisms (access control, authentication) extended to AI operational semantics.

### 2.4 The Blueprint Abstraction

Execution layer governance requires a formal intermediate representation capturing operational intent in machine-verifiable form. We term this representation a **Blueprint**.

A Blueprint encodes:
- **Operations**: Specific actions to be executed (database updates, API invocations, system commands)
- **Targets**: Resources those operations will affect
- **Parameters**: Inputs and configuration for each operation
- **Authority Requirements**: Permissions needed to execute each operation
- **Risk Classifications**: Sensitivity levels assigned to operations
- **Dependencies**: Ordering constraints and prerequisite relationships
- **Compliance Metadata**: Tags identifying applicable policy frameworks

Blueprints serve multiple critical functions:

**Inspectability**: Unlike opaque prompts or model internals, Blueprints are human-readable structured specifications that can be reviewed before execution.

**Verification**: Blueprints provide formal targets for policy evaluation—policies check whether Blueprint operations comply with requirements.

**Audit Evidence**: Blueprints bind authorization decisions to specific operational intent, preventing post-hoc claims that "the AI system did something unexpected."

**Portability**: Blueprints abstract over execution environments, enabling identical governance semantics across cloud platforms, edge devices, or air-gapped systems.

### 2.5 Authority Chains and Verifiable Delegation

Execution layer governance must support authority delegation while maintaining accountability. Authority chains track delegation from ultimate authority sources (authenticated humans, designated systems) through intermediaries to current execution requests.

Each link in an authority chain includes:
- Identity of the delegating authority
- Identity of the delegate receiving authority
- Scope of delegated permissions
- Constraints on delegation (temporal limits, operation restrictions)
- Cryptographic binding to upstream delegation artifacts

This creates **verifiable delegation** where external parties can validate that execution authority traces to legitimate sources through valid delegation steps—without trusting organizational claims.

### 2.6 Trust Artifacts: Making Governance Verifiable

The breakthrough enabling execution layer governance is **Trust Artifacts**: cryptographically signed records of authorization decisions that can be verified independently.

A Trust Artifact captures:
- The Blueprint being authorized
- The authorization decision (approve/deny/escalate)
- Evaluated policies and validation outcomes
- Complete authority chain
- Timestamp and cryptographic signature

Trust Artifacts provide:

**Non-Repudiation**: Signing authorities cannot later deny making authorization decisions—signatures provide cryptographic proof.

**Tamper-Evidence**: Any modification to artifact content invalidates signatures, enabling detection of manipulation.

**Portable Verification**: External parties (regulators, auditors, treaty verification bodies) can validate artifacts without access to internal systems.

**Audit Lineage**: Artifacts reference upstream artifacts in verifiable chains, enabling reconstruction of complete authorization history.

### 2.7 From Compliance Claims to Cryptographic Proofs

Traditional governance produces compliance claims:
- "Our AI system complies with GDPR Article 32"
- "We implement appropriate human oversight for high-risk decisions"
- "Our audit logs capture all relevant events"

Execution layer governance produces cryptographic proofs:
- Trust Artifact demonstrating GDPR-required controls were enforced for specific operation
- Authority Receipt showing human review occurred before high-risk execution
- Immutable audit ledger with merkle proofs of complete event history

This transformation—from claims to proofs—addresses the verification crisis. Regulators no longer depend on trusting organizational assertions. They independently verify cryptographic evidence.

---

## 3. Addressing Structural Failures in Current Governance

This section demonstrates how execution layer governance addresses specific failure modes identified in Section 1.

### 3.1 Solving the Risk Classification Problem

**Current Failure**: Static risk classifications cannot capture dynamic operational risk based on context, delegation, and environmental factors.

**Execution Layer Solution**: Risk classification occurs at operation granularity within Blueprints rather than at system level.

When an AI agent generates operational intent, Blueprint generation analyzes each operation individually:
- Database read operations: Low risk
- Database write operations modifying PII: High risk
- Financial transactions below $1000: Medium risk  
- Financial transactions above $10,000: Critical risk

The same AI agent exhibits different risk profiles based on actual operations requested, not static system classification.

**Dynamic Risk Elevation**: Risk levels automatically escalate based on:
- Authority chain delegation depth (deeper chains = higher risk)
- Temporal factors (off-hours execution = higher risk)
- Environmental signals (geolocation anomalies = higher risk)
- Historical patterns (unusual operation combinations = higher risk)

This enables **contextual governance** where identical AI systems receive different oversight based on what they're actually trying to do rather than abstract capability assessments.

### 3.2 Eliminating Audit Theater

**Current Failure**: Auditors review documentation and samples without verifying that documented controls actually prevent non-compliant execution.

**Execution Layer Solution**: Auditors receive cryptographic proofs of enforcement rather than documentation claims.

**Example Audit Flow**:

*Traditional Audit*:
- Auditor requests evidence of GDPR compliance
- Organization provides documentation: policies, training records, sample logs
- Auditor reviews samples for apparent compliance
- Auditor issues compliance opinion based on reviewed documentation

*Execution Layer Audit*:
- Auditor requests Trust Artifacts for GDPR-applicable operations during audit period
- Organization provides signed Trust Artifacts
- Auditor cryptographically verifies:
  - Artifacts signed by organization's enforcement infrastructure
  - Authority chains trace to legitimate sources  
  - Policy evaluation included GDPR framework
  - Operations matched documented GDPR controls
- Auditor issues compliance opinion based on verified cryptographic evidence

The critical difference: auditor independently verifies that controls were enforced, not merely documented.

**Continuous Compliance Verification**: Regulators can verify ongoing compliance by periodically requesting Trust Artifacts for random operation samples without full audits. Organizations cannot selectively disclose favorable samples—cryptographic artifacts are verifiable against immutable audit ledgers.

### 3.3 Enabling Cross-Border Verification

**Current Failure**: International governance relies on trust because nations cannot verify foreign AI system compliance without invasive access.

**Execution Layer Solution**: Portable cryptographic proofs enable verification without system access.

**Treaty Verification Scenario**:

Nation A and Nation B sign AI safety treaty prohibiting autonomous weapons targeting without human authorization.

*Traditional Enforcement*:
- Nations trust each other's compliance claims
- Treaty violations detected through intelligence gathering or incidents
- Enforcement is political rather than technical

*Execution Layer Enforcement*:
- Nations deploy governed execution substrates enforcing treaty requirements
- AI systems generating weapons targeting intent must pass through substrates
- Substrates generate Trust Artifacts proving human authorization occurred
- Treaty verification bodies periodically sample Trust Artifacts
- Non-compliant operations are architecturally prevented, not merely prohibited

The transformation: treaty compliance becomes technically verifiable through cryptographic evidence rather than trust-dependent.

**Sovereignty Preservation**: Nations verify compliance without accessing each other's AI systems. Trust Artifacts are generated domestically and shared with treaty bodies—no foreign access to systems required.

### 3.4 Solving Incident Attribution

**Current Failure**: Post-incident attribution fails due to incomplete logs, temporal gaps, and adversarial tampering possibilities.

**Execution Layer Solution**: Immutable audit lineage with cryptographic tamper-evidence ensures attribution integrity.

**Incident Reconstruction**:

When harmful AI action occurs, investigators retrieve:

1. **Authority Receipt** documenting what executed and when
2. **Trust Artifact** showing authorization decision and evaluated policies
3. **Blueprint** specifying operational intent
4. **Authority Chain** identifying who held authority
5. **Policy Versions** showing which rules were in effect
6. **Upstream Artifacts** reconstructing complete authorization history

This evidence forms cryptographically-bound chain that investigators can verify:
- Signatures prove authenticity
- Merkle proofs demonstrate inclusion in immutable audit ledger
- Timestamps establish temporal ordering
- Authority chains identify accountability

**Adversarial Resistance**: Even privileged insiders cannot manipulate historical artifacts without invalidating cryptographic proofs. Tampering is detectable by external investigators.

### 3.5 Policy Fragmentation Reconciliation

**Current Failure**: AI systems operating globally face contradictory requirements across jurisdictions with no technical mechanism for reconciliation.

**Execution Layer Solution**: Declarative policy abstraction with multi-framework evaluation and conflict detection.

**Multi-Jurisdictional Workflow**:

AI system operates across EU (GDPR + AI Act), US (state-level privacy laws), and China (PIPL).

Blueprint generation tags operations with applicable frameworks:
- Operation involving EU resident data: tagged with GDPR, AI Act
- Operation involving California resident data: tagged with CCPA
- Operation involving Chinese resident data: tagged with PIPL

Policy evaluation engine evaluates Blueprint against all tagged frameworks in parallel:
- GDPR evaluation: Check purpose limitation, data minimization, consent
- AI Act evaluation: Check risk classification, human oversight requirements  
- CCPA evaluation: Check disclosure obligations, opt-out rights
- PIPL evaluation: Check cross-border transfer restrictions

**Conflict Handling**:
- If frameworks impose contradictory requirements → Escalate for human policy reconciliation
- If one framework prohibits operation others allow → Deny execution (most restrictive wins)
- If frameworks impose complementary requirements → Require satisfaction of all

This enables **simultaneous compliance** across jurisdictions rather than fragmented compliance attempts.

### 3.6 Governance at Scale

Traditional governance imposes linear overhead: more AI operations require proportionally more human review, documentation, and audit effort.

Execution layer governance scales sublinearly:

**Automated Enforcement**: Policy evaluation is computational—scales with infrastructure rather than human review capacity.

**Risk-Based Human Involvement**: Only operations exceeding risk thresholds require human review. Routine low-risk operations execute with automated validation.

**Audit Automation**: Cryptographic verification replaces manual audit review. Auditors sample Trust Artifacts and verify signatures rather than reviewing complete operational histories.

This scaling property is essential for environments deploying thousands or millions of AI-driven operations daily.

---

## 4. Regulatory Framework Integration

This section maps execution layer governance to specific requirements in emerging regulatory frameworks, demonstrating how the paradigm addresses mandated controls.

### 4.1 EU AI Act Compliance Pathways

The EU AI Act imposes requirements on high-risk AI systems including:

**Article 9 - Risk Management System**

*Requirement*: "High-risk AI systems shall be designed and developed with risk management system consisting of continuous iterative process..."

*Execution Layer Implementation*:
- Blueprint risk classification provides continuous risk assessment at operation granularity
- Policy frameworks encode risk acceptance thresholds
- Runtime enforcement implements "continuous iterative process" through per-operation validation
- Trust Artifacts document risk assessment decisions for regulatory review

**Article 12 - Record-Keeping**

*Requirement*: "High-risk AI systems shall be designed with capabilities enabling automatic recording of events ('logs') relevant for identification of risks and functioning throughout lifetime..."

*Execution Layer Implementation*:
- Immutable audit ledger automatically records all authorization decisions and execution outcomes
- Cryptographic tamper-evidence ensures log integrity
- Logs capture "events relevant for identification of risks" through Blueprint risk metadata
- Portable verification enables regulators to access logs without production system access

**Article 13 - Transparency and Provision of Information to Users**

*Requirement*: "High-risk AI systems shall be designed to enable users to interpret system output and use it appropriately..."

*Execution Layer Implementation*:
- Blueprints provide human-readable explanation of what operations will execute
- Trust Artifacts document why operations were authorized
- Authority Receipts show what actually executed
- Users receive complete transparency without depending on AI system internals

**Article 14 - Human Oversight**

*Requirement*: "High-risk AI systems shall be designed to enable effective oversight by natural persons during period in which AI system is in use..."

*Execution Layer Implementation*:
- Enforcement pipeline includes escalation to humans for high-risk operations
- Blueprints enable human review before execution
- Override mechanisms allow humans to deny operations that passed automated validation
- Authority chains document human oversight decisions with cryptographic non-repudiation

**Article 72 - Post-Market Monitoring**

*Requirement*: "Providers shall establish and document post-market monitoring system appropriate to nature of AI technologies and risks..."

*Execution Layer Implementation*:
- Continuous audit trail enables real-time monitoring of AI system behavior
- Trust Artifacts aggregation reveals operational patterns and anomalies
- Risk classification trends identify emerging risks
- Automated analysis detects policy violations or concerning behavioral shifts

### 4.2 NIST AI RMF Alignment

The NIST AI RMF organizes risk management into four functions: GOVERN, MAP, MEASURE, MANAGE. Execution layer governance addresses each:

**GOVERN Function**

*Core Requirement*: "Establish governance structures, policies, and processes to cultivate culture of risk management..."

*Execution Layer Implementation*:
- Policy frameworks encode governance structures as declarative rules
- Authority chains implement governance hierarchies
- Trust Artifacts provide verifiable evidence of governance enforcement
- Audit trails document governance process execution

**MAP Function**

*Core Requirement*: "Context is established and risks are identified, assessed, and documented..."

*Execution Layer Implementation*:
- Blueprint generation identifies operations and associated risks
- Risk classification documents risk levels at operation granularity
- Policy frameworks assess risks against acceptance criteria
- Trust Artifacts document complete risk assessment process

**MEASURE Function**

*Core Requirement*: "Identified risks are tracked and measured through defined metrics..."

*Execution Layer Implementation*:
- Audit ledger provides quantitative metrics: operations executed, authorization denials, policy violations detected, escalations triggered
- Risk classification distribution analysis reveals system risk profile
- Trust Artifact analysis measures governance effectiveness
- Trends identify risk trajectory over time

**MANAGE Function**

*Core Requirement*: "Risks are prioritized and responded to on regular basis..."

*Execution Layer Implementation*:
- Runtime enforcement manages risks through pre-execution prevention
- Risk thresholds automatically prioritize oversight based on operation sensitivity
- Policy updates enable responsive risk management
- Escalation mechanisms handle risks exceeding automated management

### 4.3 ISO 42001 AI Management System

ISO 42001 specifies requirements for AI management systems. Key execution layer alignments:

**Control 6.1.2 - Risk Assessment Process**

*Requirement*: Organization must identify risks associated with AI systems considering failures, misuse, bias, security vulnerabilities...

*Execution Layer Implementation*:
- Blueprint risk classification identifies operational risks
- Threat model (referenced from technical paper) catalogs misuse and security vulnerabilities
- Policy frameworks encode risk acceptance criteria
- Runtime enforcement prevents identified risks from materializing

**Control 8.4 - Data for AI System**

*Requirement*: Organization must ensure data used for AI system development and operation is suitable...

*Execution Layer Implementation*:
- Operations accessing data tagged with sensitivity classifications
- Policy frameworks enforce data minimization and purpose limitation
- Authority chains verify data access authorization
- Audit trail documents all data access with justifications

**Control 8.7 - Transparency**

*Requirement*: Organization must provide stakeholders with appropriate level of transparency about AI system...

*Execution Layer Implementation*:
- Blueprints provide transparency into what AI systems will do
- Trust Artifacts explain why operations were authorized
- Authority Receipts document what actually occurred
- Stakeholders receive verifiable evidence rather than organizational claims

**Control 9.1 - Monitoring, Measurement, Analysis, Evaluation**

*Requirement*: Organization must determine what needs to be monitored and measured, methods for ensuring valid results, when monitoring shall be performed...

*Execution Layer Implementation*:
- Continuous audit capture provides comprehensive monitoring
- Trust Artifact metrics enable quantitative measurement
- Cryptographic verification ensures valid results
- Real-time enforcement enables immediate evaluation

### 4.4 Positioning for Future Frameworks

Execution layer governance is designed as **framework-agnostic substrate** that can enforce requirements from emerging frameworks without architectural changes.

**Extension Mechanism**:
1. New framework requirements formalized as declarative policies
2. Policies integrated into policy evaluation engine
3. Blueprint compliance tags updated to include new framework
4. Enforcement begins automatically for tagged operations

This enables rapid adaptation as regulatory landscape evolves without modifying core enforcement infrastructure.

**Example - Hypothetical UN AI Treaty**:

Treaty requires:
- All autonomous weapons systems include human-in-loop authorization
- Lethal force operations logged with 50-year retention
- Treaty verification through periodic artifact sampling

Implementation:
- Policy framework encodes "autonomous weapons" operation classification
- Rules require human escalation for lethal force operations
- Audit retention configured for 50-year persistence
- Trust Artifacts made available to UN verification body

No infrastructure changes required—new requirements expressed through policy framework extensions.

---

## 5. Global AI Safety Standards: A Technical Foundation

### 5.1 The Treaty Verification Problem

International AI safety agreements face an intractable verification challenge: how can nations verify that treaty partners comply with commitments about AI system behavior without invasive access to sovereign systems?

Historical arms control treaties provide instructive parallels:

**Nuclear Non-Proliferation Treaty**: Verification through IAEA inspections of declared facilities, environmental sampling, and technical monitoring. Physical verification is possible because nuclear materials and facilities are observable.

**Chemical Weapons Convention**: Verification through routine inspections, challenge inspections, and investigation of alleged use. Chemical weapons production involves detectable precursors and facilities.

**AI Safety Treaties**: What would verification mechanisms look like? AI systems have no physical signatures. Training happens in distributed datacenters. Deployment is global and software-based. Compliance violations may be entirely digital and invisible to external monitoring.

Traditional verification approaches (inspections, sampling, technical monitoring) fail for AI because there's nothing physical to inspect and no environmental signature to detect.

### 5.2 Cryptographic Verification as Alternative

Execution layer governance enables a fundamentally different verification model: **cryptographic evidence-based verification**.

Rather than inspecting AI systems, treaty verification bodies receive Trust Artifacts proving that governed operations satisfied treaty requirements.

**Key Properties**:

**Non-Invasive**: Nations generate Trust Artifacts from domestic enforcement infrastructure. No foreign access to systems required.

**Verifiable**: Trust Artifacts contain cryptographic signatures and merkle proofs enabling independent validation.

**Selective Disclosure**: Nations can prove specific compliance claims (e.g., "human authorization occurred") without revealing operational details or capabilities.

**Continuous**: Verification happens through ongoing artifact sampling rather than periodic intrusive inspections.

**Tamper-Evident**: Historical artifacts cannot be modified without detection, preventing ex-post fabrication of compliance evidence.

### 5.3 Reference Treaty Architecture

Consider a hypothetical International AI Safety Treaty with three core requirements:

**R1: No Autonomous Lethal Targeting**  
AI systems may assist targeting decisions but cannot autonomously authorize lethal force without human approval.

**R2: High-Risk Operation Logging**  
Operations classified as high-risk must be logged with cryptographically verifiable audit trails retained for minimum 10 years.

**R3: Cross-Border Data Restrictions**  
AI systems cannot transfer sensitive personal data across borders without satisfying both source and destination jurisdiction privacy requirements.

**Execution Layer Implementation**:

Each signatory deploys governed execution substrate enforcing treaty requirements:

**Enforcement Infrastructure**:
- Policy framework encoding R1, R2, R3 as mandatory constraints
- Blueprint classification logic identifying lethal targeting, high-risk operations, cross-border data flows
- Human escalation for operations requiring R1 authorization
- Audit retention with 10-year persistence for R2 compliance
- Multi-jurisdictional policy evaluation for R3 compliance

**Verification Protocol**:
1. Treaty verification body periodically requests random samples of Trust Artifacts from signatory nations
2. Nations provide requested artifacts (50-200 samples per verification period)
3. Verification body validates:
   - Cryptographic signatures authentic
   - Authority chains include required human authorization (R1)
   - High-risk operations logged with proper retention (R2)
   - Cross-border transfers satisfied jurisdictional requirements (R3)
4. Statistical sampling provides high confidence in systemic compliance

**Violation Detection**:
- Missing artifacts for known operations suggests enforcement bypass
- Invalid cryptographic signatures indicate tampering
- Authority chains lacking required human authorization demonstrate R1 violation
- Incomplete audit retention violates R2

**Enforcement Escalation**:
- Technical violations trigger diplomatic engagement
- Persistent violations subject to treaty-defined consequences
- Public disclosure of verification results creates reputational pressure

### 5.4 Advantages Over Trust-Based Treaties

Execution layer governance provides several advantages over traditional treaty frameworks:

**Verifiability**: Compliance is cryptographically provable rather than trust-dependent.

**Granularity**: Verification operates at operation level (individual targeting decisions, data transfers) rather than system level (does the nation have compliant AI systems?).

**Timeliness**: Verification can detect violations within verification periods (quarterly, monthly) rather than years later through incident investigation.

**Attribution**: Violations trace to specific operations with complete authority chains identifying responsible parties.

**Resistance to Gaming**: Unlike inspection regimes that can be evaded by hiding non-compliant activities, cryptographic verification requires providing valid artifacts for sampled operations—fabricating artifacts is cryptographically infeasible.

### 5.5 Sovereignty and Trust Minimization

Critical concern: does execution layer governance require nations to trust foreign verification infrastructure or disclose sensitive capabilities?

**No Foreign Infrastructure Dependency**:
- Each nation deploys independent enforcement substrate under sovereign control
- Trust Artifacts generated by domestic infrastructure
- No requirement to use shared or foreign verification systems

**Selective Disclosure**:
- Trust Artifacts prove compliance claims without revealing operational details
- Zero-knowledge proof techniques can prove policy compliance without disclosing which policies were evaluated
- Nations control what metadata is included in shared artifacts

**Trust Minimization**:
- Verification depends on cryptographic signatures, not trusted parties
- Audit ledgers use distributed structures (e.g., blockchain) preventing unilateral tampering
- Multiple verification bodies can independently validate same artifacts

### 5.6 Incremental Adoption Pathway

Global adoption of execution layer governance for treaty verification could proceed incrementally:

**Phase 1: Bilateral Agreements**  
Two nations pilot execution layer governance in bilateral AI safety agreement. Develop verification protocols, artifact schemas, and dispute resolution mechanisms.

**Phase 2: Regional Frameworks**  
Successful bilateral implementations expand to regional frameworks (EU member states, allied nations). Standardize policy specification languages and artifact formats.

**Phase 3: Multilateral Treaties**  
Regional successes inform multilateral treaty negotiations. Execution layer governance becomes technical foundation for treaty verification.

**Phase 4: Universal Standards**  
Execution layer governance substrates become reference architecture in international standards bodies (UN, ISO, ITU). Compatible implementations ensure global interoperability.

This pathway enables experimentation and refinement before universal adoption.

---

## 6. Implementation Considerations for Policymakers

This section addresses practical questions policymakers face when considering execution layer governance mandates.

### 6.1 Regulatory Mandate vs. Voluntary Adoption

**Question**: Should execution layer governance be mandated for certain AI systems or encouraged through voluntary frameworks?

**Considerations**:

**Mandate Arguments**:
- High-risk AI systems (autonomous vehicles, medical diagnosis, financial trading) require enforceable governance beyond organizational goodwill
- Competitive dynamics discourage voluntary adoption of costly governance infrastructure
- Mandatory governance creates level playing field preventing race-to-bottom

**Voluntary Arguments**:
- Technology remains nascent; mandates may constrain beneficial innovation
- Organizations should have flexibility in governance implementation approaches
- Market pressure and liability exposure may drive adoption without mandates

**Hybrid Approach**:
- Mandate execution layer governance for AI systems above specified risk thresholds (e.g., EU AI Act "high-risk" classification)
- Encourage voluntary adoption for lower-risk systems through regulatory incentives:
  - Liability protection for organizations with certified governed execution substrates
  - Streamlined compliance audits for organizations providing Trust Artifacts
  - Procurement preferences for government contracts requiring verifiable governance

### 6.2 Standardization Requirements

**Question**: What aspects of execution layer governance require standardization vs. competitive differentiation?

**Should Be Standardized**:

**Blueprint Schema Format**: Interoperability requires common schema for representing operational intent. Organizations should use compatible Blueprint formats enabling cross-system governance.

**Trust Artifact Structure**: Verification bodies and auditors need consistent artifact formats to validate compliance across organizations.

**Cryptographic Algorithms**: Governance evidence must use well-vetted, quantum-resistant cryptographic algorithms with standardized key management.

**Policy Specification Language**: Declarative policy frameworks should use standard languages (or interoperable languages) enabling policy portability.

**Can Remain Competitive**:

**Intent Resolution Mechanisms**: How organizations transform natural language or API calls into Blueprints can vary competitively.

**Policy Evaluation Optimization**: Performance optimizations in policy evaluation can differentiate implementations.

**User Interfaces**: How organizations present Blueprints and Trust Artifacts to users and auditors.

**Enforcement Infrastructure**: Deployment models (cloud, edge, hybrid) can vary based on organizational needs.

**Standardization Bodies**:
- ISO/IEC JTC 1/SC 42 (AI) for Blueprint and Trust Artifact schemas
- NIST for cryptographic algorithm specifications
- IEEE for policy specification languages
- W3C for web-based governance APIs and interfaces

### 6.3 Compliance Cost and Accessibility

**Question**: Does execution layer governance impose prohibitive costs on smaller organizations or open-source AI projects?

**Cost Analysis**:

**Infrastructure Costs**:
- Enforcement engine deployment: Comparable to existing security infrastructure (authentication systems, access control)
- Audit ledger persistence: Storage costs scale with operation volume but can leverage cost-effective blockchain or distributed ledgers
- Cryptographic operations: Minimal computational overhead (sub-millisecond signature generation)

**Operational Costs**:
- Policy framework development: Initial cost developing declarative policies from existing governance documentation
- Integration effort: Adapting AI systems to submit intent through enforcement layer
- Monitoring and maintenance: Ongoing oversight of enforcement infrastructure

**Cost Mitigation**:

**Open-Source Reference Implementations**: Government-funded or industry consortium open-source enforcement infrastructure reduces implementation costs.

**Governance-as-a-Service**: Cloud providers offer managed governance substrates that small organizations can adopt without infrastructure investment.

**Tiered Requirements**: Smaller organizations or lower-risk AI systems could use simplified governance with reduced audit retention or less frequent verification.

**Grants and Subsidies**: Government programs supporting governance infrastructure adoption for small businesses and open-source projects.

### 6.4 International Harmonization Challenges

**Question**: How can jurisdictions with different regulatory philosophies harmonize execution layer governance requirements?

**Divergence Points**:

**Risk Tolerance**: Jurisdictions may classify identical AI systems at different risk levels based on local values and risk acceptance.

**Privacy Standards**: Data protection requirements vary significantly (GDPR vs. CCPA vs. PIPL).

**Oversight Mechanisms**: Some jurisdictions may require governmental oversight bodies with direct access to Trust Artifacts; others may rely on industry self-regulation.

**Harmonization Strategies**:

**Mutual Recognition**: Jurisdictions recognize each other's governance frameworks as sufficient if they meet minimum baseline requirements. Trust Artifacts from one jurisdiction accepted as compliance evidence in others.

**Modular Compliance**: Execution layer governance supports simultaneous compliance with multiple frameworks through multi-framework policy evaluation. Organizations satisfy all applicable jurisdictional requirements in parallel.

**Treaty-Level Baseline**: International AI safety treaties establish minimum governance requirements that all signatories must enforce through execution layer substrates, while allowing jurisdictions to impose additional requirements.

**Policy Translation Services**: Automated tools translate policies from one jurisdiction's specification language to another's, enabling organizations to maintain single policy source with multi-jurisdictional enforcement.

### 6.5 Transition and Legacy System Integration

**Question**: How do organizations transition existing AI deployments to execution layer governance without disrupting operations?

**Phased Transition**:

**Phase 1 - Audit-Only Mode**:
- Deploy enforcement infrastructure in monitoring mode
- Generate Blueprints and Trust Artifacts but don't block operations
- Organizations review audit data to identify policy gaps and unexpected behaviors
- Refine policies before active enforcement

**Phase 2 - Graduated Enforcement**:
- Enable enforcement for low-risk operations first
- Escalate high-risk operations to humans for review
- Gradually expand enforcement coverage as confidence increases

**Phase 3 - Full Enforcement**:
- Enforce all operations through governance substrate
- Human escalation only for genuinely ambiguous cases
- Continuous monitoring and policy refinement

**Legacy System Strategies**:

**API Wrapper Approach**: Insert enforcement layer as API gateway between legacy AI systems and execution infrastructure. AI systems invoke gateway APIs instead of directly executing operations.

**Event-Driven Interception**: Deploy enforcement as event interceptor monitoring AI system outputs. When systems generate execution requests, enforcement validates before allowing execution.

**Gradual Refactoring**: Prioritize critical legacy systems for refactoring to native execution layer integration, while lower-risk systems use wrapper approaches.

**Sunset Timelines**: Establish regulatory timelines for full execution layer integration of existing AI systems based on risk classification (e.g., high-risk systems: 24 months, medium-risk: 48 months).

---

## 7. Limitations and Open Policy Questions

### 7.1 Human Authority Fallibility

**Limitation**: Execution layer governance ultimately depends on human authorities making authorization decisions. Compromised, coerced, or malicious authorities can authorize harmful operations while maintaining governance process compliance.

**Policy Question**: How should regulatory frameworks address insider threats where authorized humans intentionally approve harmful AI operations?

**Potential Approaches**:
- Multi-party authorization for critical operations (no single human can approve alone)
- Behavioral anomaly detection identifying unusual authorization patterns
- Periodic review of authorization decisions by independent oversight
- Legal liability frameworks holding authorizing parties accountable for harmful decisions

This remains an open governance challenge beyond execution layer governance's technical scope.

### 7.2 Policy Specification Completeness

**Limitation**: Declarative policy frameworks must comprehensively specify governance requirements. Incomplete policies create gaps that permit non-compliant operations to pass validation.

**Policy Question**: Who bears responsibility for policy specification errors—AI system operators, policy framework developers, or regulatory bodies?

**Potential Approaches**:
- Regulatory bodies publish reference policy frameworks for common risk scenarios
- Industry consortia develop standardized policy libraries that organizations customize
- Liability allocation based on whether organizations used standard policies vs. custom policies
- Continuous policy testing through adversarial simulation

### 7.3 Enforcement Latency Tradeoffs

**Limitation**: Comprehensive governance validation introduces latency. Some AI applications (autonomous vehicles, real-time trading, emergency response) may have latency constraints incompatible with thorough policy evaluation.

**Policy Question**: How should regulations balance governance rigor against operational latency requirements?

**Potential Approaches**:
- Tiered enforcement with reduced validation for latency-critical operations, compensated by enhanced post-execution auditing
- Pre-approved operation templates for common scenarios, enabling fast-path validation
- Risk-based latency budgets where higher-risk operations justify greater latency
- Innovation incentives for enforcement optimization reducing validation time

### 7.4 Cross-Jurisdictional Conflict Resolution

**Limitation**: When policy frameworks from multiple jurisdictions impose contradictory requirements, execution layer governance can detect conflicts but cannot resolve them.

**Policy Question**: What mechanisms should resolve conflicts between jurisdictional requirements for AI systems operating globally?

**Potential Approaches**:
- International AI governance body with authority to issue conflict resolution guidance
- Default to most restrictive requirement among conflicting jurisdictions
- Organizations must obtain waivers from less restrictive jurisdiction to satisfy more restrictive one
- AI systems partition operations geographically to satisfy local requirements

### 7.5 Adversarial Manipulation of Intent

**Limitation**: Sophisticated adversaries may craft operational intent that technically satisfies policies while achieving harmful outcomes through semantic manipulation.

**Policy Question**: Should regulations require organizations to implement adversarial testing of governance policies?

**Potential Approaches**:
- Mandatory red team exercises attempting to bypass governance through policy exploitation
- Continuous learning systems that update policies when adversarial evasions are discovered
- Liability frameworks penalizing organizations whose policies are demonstrably inadequate
- Information sharing requirements where discovered policy bypasses must be reported to regulators

### 7.6 Audit Retention and Privacy Tradeoffs

**Limitation**: Long-term audit retention creates tension with privacy principles minimizing data retention. Audit trails containing personal data may conflict with right-to-erasure requirements.

**Policy Question**: How should regulations balance audit retention for accountability against data minimization for privacy?

**Potential Approaches**:
- Pseudonymization or anonymization of personal data in audit records while preserving operational details
- Tiered retention where operational metadata retained longer than personal data details
- Explicit audit retention exemptions from right-to-erasure for compliance purposes
- Cryptographic commitments allowing privacy-preserving verification without revealing personal data

### 7.7 Open-Source AI and Governance Feasibility

**Limitation**: Open-source AI models distributed publicly cannot be forced through execution layer governance. Anyone can deploy models without governance infrastructure.

**Policy Question**: Should regulations focus on AI system operators rather than model developers, requiring governance regardless of model source?

**Potential Approaches**:
- Operator liability: Organizations deploying AI systems (open-source or proprietary) must implement execution layer governance
- Graduated requirements based on deployment context rather than model source
- Safe harbors for research and non-commercial deployments without governance mandates
- Developer incentives (liability protection, procurement preferences) for models designed for governed execution

---

## 8. Conclusion: Toward Verifiable AI Governance

### 8.1 The Paradigm Shift

This paper has argued for a fundamental shift in AI governance: from process-based compliance to infrastructure-enforced verification.

Current governance approaches ask: "Does this organization have appropriate policies?" Execution layer governance asks: "Can this operation execute without authorization?"

Current approaches trust organizational claims. Execution layer governance provides cryptographic proofs.

Current approaches detect violations retrospectively. Execution layer governance prevents violations pre-execution.

This shift is not merely technical—it is epistemic. It transforms what we can know about AI system compliance from probabilistic trust to cryptographic certainty.

### 8.2 Why Now?

Two factors make execution layer governance both necessary and feasible today:

**Necessity**: AI systems transition from research curiosities to operational infrastructure managing critical societal functions. Traditional governance approaches designed for human-operated systems prove structurally inadequate for AI's probabilistic decision-making and distributed execution.

**Feasibility**: Technical foundations exist—cryptographic signatures, blockchain audit trails, declarative policy languages, distributed trust mechanisms. These technologies were nascent a decade ago but are now proven at scale.

The window is closing for proactive governance infrastructure deployment. Once AI systems are deeply embedded in critical infrastructure without governance substrates, retrofitting becomes exponentially harder.

### 8.3 Implications for International AI Safety

The most significant implication extends beyond individual organizations to international AI governance:

**Execution layer governance makes AI safety treaties technically verifiable.**

For the first time, nations could demonstrate compliance with international AI commitments through cryptographic evidence rather than trust and inspection. This unlocks treaty possibilities previously infeasible:

- Autonomous weapons restrictions with verifiable human-in-loop requirements
- AI-driven cyberoperations limitations with provable attribution
- Data protection agreements with cryptographic transfer verification
- High-risk AI deployment standards with portable compliance proofs

The transformation is analogous to how cryptographic verification enabled secure internet commerce. Before public-key cryptography, online transactions required trusting counterparties. After, cryptographic signatures provided mathematical certainty.

Execution layer governance provides similar certainty for AI safety commitments.

### 8.4 The Path Forward for Policymakers

Policymakers considering execution layer governance should pursue three parallel tracks:

**Track 1: Pilot Programs**  
Fund pilot deployments in high-risk domains (healthcare, finance, autonomous systems) demonstrating feasibility and refining requirements before broad mandates.

**Track 2: Standardization Engagement**  
Actively participate in international standards bodies (ISO, IEEE, NIST) developing Blueprint schemas, Trust Artifact formats, and policy specification languages.

**Track 3: Regulatory Framework Development**  
Draft regulations incorporating execution layer governance as technical foundation, with clear timelines for adoption and transition support for existing deployments.

### 8.5 From Advisory to Architectural

The central thesis of this paper: **AI governance must transition from advisory frameworks to architectural enforcement**.

Advisory frameworks document what organizations should do. Architectural enforcement makes non-compliance technically difficult.

Advisory frameworks depend on organizational discipline. Architectural enforcement depends on cryptographic mathematics.

Advisory frameworks are audited retrospectively. Architectural enforcement is verified continuously.

This transition is inevitable. The only question is whether it happens proactively through deliberate policy design, or reactively after governance failures create public demand.

Execution layer governance offers a proactive path: technical infrastructure that can be deployed today, refined through experience, and scaled to global AI safety challenges.

The verification crisis in AI governance is solvable. The solution requires treating governance not as compliance documentation but as execution infrastructure—as fundamental as access control in operating systems or encryption in communication networks.

Just as modern internet security would be unthinkable without cryptographic foundations, future AI safety will be unthinkable without execution layer governance.

The foundations are available. The need is urgent. The path is clear.

What remains is implementation.

---

## References

[1] European Parliament and Council. (2024). Regulation (EU) 2024/1689 on Artificial Intelligence (AI Act). Official Journal of the European Union.

[2] National Institute of Standards and Technology. (2023). Artificial Intelligence Risk Management Framework (AI RMF 1.0). NIST. https://doi.org/10.6028/NIST.AI.100-1

[3] International Organization for Standardization. (2023). ISO/IEC 42001:2023 - Information technology — Artificial intelligence — Management system. ISO.

[4] Organisation for Economic Co-operation and Development. (2019). OCED Principles on Artificial Intelligence. OECD Legal Instruments.

[5] United Nations. (2023). Governing AI for Humanity: Final Report of the UN Advisory Body on Artificial Intelligence. United Nations.

[6] Brundage, M., et al. (2020). Toward Trustworthy AI Development: Mechanisms for Supporting Verifiable Claims. arXiv:2004.07213.

[7] Scharre, P. (2023). Four Battlegrounds: Power in the Age of Artificial Intelligence. W. W. Norton & Company.

[8] Hoffmann, S., et al. (2023). Auditing AI: A Framework for Regulatory Compliance. Harvard Journal of Law & Technology, 36(2).

[9] Crootof, R., & Kaminski, M. E. (2023). AI Self-Regulation Isn't Enough. Stanford Technology Law Review, 26(1).

[10] Whittaker, M., et al. (2018). AI Now Report 2018. AI Now Institute.

[11] Raji, I. D., et al. (2020). Closing the AI Accountability Gap: Defining an End-to-End Framework for Internal Algorithmic Auditing. ACM Conference on Fairness, Accountability, and Transparency.

[12] Metcalf, J., & Moss, E. (2019). Owning Ethics: Corporate Logics, Silicon Valley, and the Institutionalization of Ethics. Social Research, 86(2), 449-476.

[13] Selbst, A. D. (2021). An Institutional View of Algorithmic Impact Assessments. Harvard Journal of Law & Technology, 35(1).

[14] Citron, D. K., & Pasquale, F. (2014). The Scored Society: Due Process for Automated Predictions. Washington Law Review, 89, 1-33.

[15] Crawford, K., & Schultz, J. (2014). Big Data and Due Process: Toward a Framework to Redress Predictive Privacy Harms. Boston College Law Review, 55(1), 93-128.

[16] Wachter, S., Mittelstadt, B., & Floridi, L. (2017). Why a Right to Explanation of Automated Decision-Making Does Not Exist in the General Data Protection Regulation. International Data Privacy Law, 7(2), 76-99.

[17] Partnership on AI. (2023). Guidelines for Safe Foundation Model Deployment. Partnership on AI.

[18] Anthropic. (2023). Core Views on AI Safety. Anthropic Blog.

[19] OpenAI. (2023). Democratic Inputs to AI. OpenAI Research.

[20] DeepMind. (2023). Frontier Safety Framework. DeepMind Safety.

[21] Rose, S., Borchert, O., Mitchell, S., & Connelly, S. (2020). Zero Trust Architecture. NIST Special Publication 800-207.

[22] Nakamoto, S. (2008). Bitcoin: A Peer-to-Peer Electronic Cash System. https://bitcoin.org/bitcoin.pdf

[23] Buterin, V. (2014). A Next-Generation Smart Contract and Decentralized Application Platform. Ethereum White Paper.

[24] Castro, M., & Liskov, B. (1999). Practical Byzantine Fault Tolerance. USENIX Symposium on Operating Systems Design and Implementation.

[25] Merkle, R. C. (1987). A Digital Signature Based on a Conventional Encryption Function. Advances in Cryptology — CRYPTO '87.

[26] Goldwasser, S., Micali, S., & Rackoff, C. (1989). The Knowledge Complexity of Interactive Proof Systems. SIAM Journal on Computing, 18(1), 186-208.

[27] Ben-Sasson, E., et al. (2014). Succinct Non-Interactive Zero Knowledge for a von Neumann Architecture. USENIX Security Symposium.

[28] Bernstein, D. J., et al. (2012). High-speed high-security signatures. Journal of Cryptographic Engineering, 2(2), 77-89.

[29] National Institute of Standards and Technology. (2024). Post-Quantum Cryptography Standardization. NIST.

[30] Decentralized Identity Foundation. (2023). Decentralized Identifiers (DIDs) v1.0. W3C Recommendation.

[31] MITRE Corporation. (2023). ATLAS: Adversarial Threat Landscape for Artificial-Intelligence Systems. MITRE.

[32] Brundage, M., et al. (2018). The Malicious Use of Artificial Intelligence: Forecasting, Prevention, and Mitigation. arXiv:1802.07228.

[33] International Atomic Energy Agency. (2019). Safeguards Implementation Report 2018. IAEA.

[34] Organisation for the Prohibition of Chemical Weapons. (2023). Verification Handbook. OPCW.

[35] Arms Control Association. (2023). Arms Control and Proliferation Profile: Biological Weapons Convention. ACA.

[36] Maas, M. M. (2019). How Viable is International Arms Control for Military Artificial Intelligence? Contemporary Security Policy, 40(3), 285-311.

[37] Horowitz, M. C., & Scharre, P. (2021). AI and International Stability: Risks and Confidence-Building Measures. Center for a New American Security.

[38] Allen, G., & Chan, T. (2017). Artificial Intelligence and National Security. Belfer Center for Science and International Affairs.

[39] Chinen, M. A. (2021). Law and Autonomous Weapons Systems: First Report of the Special Rapporteur. UNIDIR.

[40] United Nations Office for Disarmament Affairs. (2023). Developments in the Field of Information and Telecommunications. UNODA.

---

**END OF PAPER 2**