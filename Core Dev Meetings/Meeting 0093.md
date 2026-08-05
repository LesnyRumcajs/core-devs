# Filecoin Core Devs 93 — Meeting Minutes

**Meeting:** Core Devs 93
**Facilitator:** Christian Taylor
**Date:** August 5th, 2026
**Duration:** Approximately 24 minutes

## 1. Agenda

The meeting covered:

* FIP-0117: Repeated SnapDeals
* FIP-0118: Solstice
* JSON-RPC HTTP Conventions FRC
* Additional proposals in discussion
* NV29 network upgrade timeline
* Governance and proposal-tracking updates

Christian noted that the FIP proposal tracking board is active again and is being updated to show open pull requests, proposal stages, and monthly status changes. 

---

## 2. FIP-0117: Repeated SnapDeals

### Proposal Overview

FIP-0117 would allow storage providers to update sectors through SnapDeals more than once. A previously snapped committed-capacity sector could be “re-snapped” to replace some or all of its data without terminating and resealing the sector.

Key technical points included:

* Reuses existing SnapDeals cryptography.
* Does not require new cryptographic parameters.
* Preserves the original sector key.
* May use optional unsealed CID storage for on-chain verification.
* Uses PoDSI proofs to verify preserved pieces against the old and new CommD.
* Existing FIP-0083 events could support off-chain verification without additional state. 

### Discussion and Concerns

Andy Jackson asked whether the original committed-capacity sector would need to remain available and whether the proposal was intended to support faster or “hot” storage.

Additional concerns included:

* The storage overhead of retaining approximately 64 GB to support 32 GB of storage.
* Whether the proposal addresses a clearly established problem.
* Whether improving SnapDeals should be prioritized when the economic challenges associated with PoRep remain unresolved.
* Whether implementation effort would be justified by the expected business value.

### Follow-Up Questions for the Author

* Must the original committed-capacity sector remain available?
* What specific use case or customer problem is FIP-0117 intended to solve?
* Is fast or hot storage the primary intended use case?
* What are the expected storage overhead and economic implications?
* How should this work be prioritized against broader PoRep economic concerns?

No formal decision was recorded on advancing FIP-0117.

---

## 3. FIP-0118: Solstice

### Proposal Overview

Michael Madoff presented FIP-0118 on behalf of Irene, who was unable to attend.

The proposal would deprecate the Filecoin Plus program and DataCap system and replace them with a two-level block-reward split.

Under the proposal:

* All new sectors would automatically receive 10× quality-adjusted power.
* Governance layers involving allocators and root key holders would be removed.
* Block rewards would be divided among consensus rewards, service rewards, and burning.
* Service rewards would support client acquisition, paid storage deals, and recording qualifying deals on-chain. 

### Reward Weight Schedule

The proposed reward schedule includes:

* Consensus allocation decreasing from 95% to 50% over nine quarters.
* Service allocation beginning at 5%.
* Service allocation potentially increasing by five percentage points each quarter.
* Increases after the initial quarter being conditional on meeting quarterly Filecoin Pay Volume targets.
* Any unearned service allocation being burned and returned to the network.

Storage providers would not need to take a specific action for the reward split to apply. 

### Governance Structure

Two governance components were described:

**Stream Weights Actor**

* Controls reward-stream weights.
* May add or remove reward streams.
* Changes require a FIP.
* Changes require approval from two organizational SAFEs.
* Changes are subject to a seven-day timelock.
* Changes may be canceled during the timelock.

**Service Rewards Actor**

* Governs service-reward recipients and the Orchestrator Registry.
* Requires approval from two SAFEs and a public waiting period.
* Does not require a FIP for every change.
* Begins with a single Orchestrator.
* Is intended to expand toward multiple Orchestrators and eventually permissionless participation based on Filecoin Pay Volume. 

### Implementation Questions

The following implementation questions remain open:

* How should existing Filecoin Plus allocators and clients transition out of the DataCap system?
* How should the ecosystem communicate the end of DataCap minting and the removal of root key holders?
* How should quarterly payment and gating parameters be compressed for Calibration Network testing?
* How should existing sectors transition when using SnapDeals or extending their expiration?
* How should pledge requirements apply when all new sectors become eligible for 10× QAP?

### Pledge Discussion

Andy raised concerns about the relationship between 10× QAP and pledge requirements.

Michael’s understanding was that:

* New sectors receiving 10× QAP would be expected to provide the corresponding higher pledge.
* Existing committed-capacity sectors may be able to increase their pledge when transitioning through SnapDeals.
* Sectors using proof-of-replication technology without seeking increased rewards might continue operating differently.

The group recognized that some form of pledge-based distinction could remain, particularly between sectors pursuing rewards and sectors using PoRep primarily for its technical properties. 

### Decision

A pull request will be opened to move FIP-0118 into Last Call. Participants were asked to review the proposal and raise any remaining questions. 

---

## 4. JSON-RPC HTTP Conventions FRC

The proposed FRC would standardize how Filecoin JSON-RPC 2.0 endpoints translate application-level errors into HTTP status codes.

The goal is to establish consistent behavior across:

* Lotus
* Forest
* Venus
* Third-party RPC providers

This would allow clients and monitoring systems to identify failures without always parsing the complete JSON response.

The proposal remains under review and had not yet been merged as Draft at the time of the meeting. 

---

## 5. Additional Proposals in Discussion

Two additional proposals remain in their discussion stage:

* Filecoin Encryption Envelope FRC
* ClearState Simplification proposal

The next step is to develop FIT drafts for these proposals. Participants were encouraged to provide comments in the relevant discussion threads. 

---

## 6. NV29 Network Upgrade

FIP-0118 is currently the only proposal expected to be in scope for NV29, reflecting the scale of work required to implement Solstice and replace Filecoin Plus.

### Working Timeline

* **Actor code freeze:** August 28
* **Calibration Network target:** Around the week of September 11
* **Mainnet upgrade:** Late September, subject to final scheduling

Michael noted that the proposed late-September timing may overlap with Golden Week for participants in the Asia-Pacific region.

Christian confirmed that the final Mainnet date would be announced after the scheduling impact is reviewed. 

### Deferred Scope

Several items have been deferred from NV29. Outstanding FIP-related work and proposal debt are expected to be addressed during NV30. 

---

## 7. Decisions and Outcomes

1. A pull request will be opened to move FIP-0118 into Last Call.
2. FIP-0117 requires additional clarification from its author before further progression.
3. The JSON-RPC HTTP Conventions FRC remains under review.
4. FIT drafts are still required for the Encryption Envelope and ClearState Simplification proposals.
5. NV29 will remain narrowly scoped, with FIP-0118 as the primary proposal.
6. The final NV29 Mainnet date must account for Golden Week and Asia-Pacific contributor availability.
7. Deferred proposals and FIP debt will be considered for NV30.

---

## 8. Action Items

| Action                                                                                              | Owner                               | Status      |
| --------------------------------------------------------------------------------------------------- | ----------------------------------- | ----------- |
| Open the pull request to move FIP-0118 into Last Call                                               | Christian / governance team         | Pending     |
| Confirm whether the original CC sector must remain available under FIP-0117                         | FIP-0117 author                     | Pending     |
| Clarify the specific problem, use case, and economics behind FIP-0117                               | FIP-0117 author                     | Pending     |
| Define the transition plan for Filecoin Plus allocators, clients, and existing DataCap arrangements | FIP-0118 team                       | Pending     |
| Clarify pledge requirements for new and existing sectors receiving 10× QAP                          | FIP-0118 and engineering teams      | Pending     |
| Define compressed parameters for Calibration Network testing                                        | FIP-0118 and engineering teams      | Pending     |
| Update and maintain the FIP proposal tracking dashboard                                             | Christian                           | In progress |
| Prepare FIT drafts for the Encryption Envelope and ClearState Simplification proposals              | Proposal authors                    | Pending     |
| Confirm the NV29 Mainnet date after reviewing Golden Week constraints                               | NV29 coordination team              | Pending     |
| Review deferred proposals and FIP debt for NV30                                                     | Governance and core developer teams | Future      |


