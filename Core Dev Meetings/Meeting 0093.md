Filecoin Core Devs 93 — Meeting Minutes

Meeting: Core Devs 93
Date: August 5th, 2026
Duration: Approximately 24 minutes

Agenda

The meeting covered:

• FIP-0117: Repeated SnapDeals
• FIP-0118: Solstice
• JSON-RPC HTTP Conventions FRC
• Additional proposals in discussion
• NV29 network upgrade timeline
• Governance and proposal-tracking updates

The FIP proposal tracking board is active again and is being updated to show open pull requests, proposal stages, and monthly status changes.

FIP-0117: Repeated SnapDeals

Proposal Overview

FIP-0117 would allow storage providers to update sectors through SnapDeals more than once. A previously snapped committed-capacity sector could be re-snapped to replace some or all of its data without terminating and resealing the sector.

Key technical points:

• Reuses existing SnapDeals cryptography.
• Does not require new cryptographic parameters.
• Preserves the original sector key.
• May use optional unsealed CID storage for on-chain verification.
• Uses PoDSI proofs to verify preserved pieces against the old and new CommD.
• Existing FIP-0083 events could support off-chain verification without additional state.

Discussion and Concerns

Questions were raised about whether the original committed-capacity sector would need to remain available and whether the proposal is intended to support faster or hot-storage use cases.

Additional concerns included:

• The storage overhead of retaining approximately 64 GB to support 32 GB of storage.
• Whether the proposal addresses a clearly established problem.
• Whether improving SnapDeals should be prioritized while PoRep economic challenges remain unresolved.
• Whether the implementation effort would be justified by the expected business value.

Follow-Up Questions

• Must the original committed-capacity sector remain available?
• What specific use case or customer problem is FIP-0117 intended to solve?
• Is fast or hot storage the primary intended use case?
• What are the expected storage overhead and economic implications?
• How should this work be prioritized against broader PoRep economic concerns?

No formal decision was recorded on advancing FIP-0117.

FIP-0118: Solstice

Proposal Overview

FIP-0118 would deprecate the Filecoin Plus program and DataCap system and replace them with a two-level block-reward split.

Under the proposal:

• All new sectors would automatically receive 10× quality-adjusted power.
• Governance layers involving allocators and root key holders would be removed.
• Block rewards would be divided among consensus rewards, service rewards, and burning.


Tell me if you’d like this condensed into an action-only tracker.
