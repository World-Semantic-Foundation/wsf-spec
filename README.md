# WSF Normative Specifications

> **The normative, machine-readable specifications of WSF semantics.**

This repository (`wsf-spec/`) contains the formal specifications that downstream implementations must conform to. Per CR-WSF-17 Rev.1, WSF maintains **platform neutrality** — these specifications describe what must be true, not how to implement it.

---

## Repository Structure

```
wsf-spec/
├── README.md (this file)
├── core-specifications/    ← Core WSF semantics (YAML/JSON/RDF/OWL)
├── conformance/            ← Conformance requirements and test suites
├── serialization/          ← Serialization format specifications
└── namespace/              ← Namespace strategy and identity scheme
```

---

## What Lives Here

### `core-specifications/`

The formal, machine-readable specifications of WSF semantics. Initially authored as YAML; serializations to JSON-LD, RDF/Turtle, OWL XML defined by subsequent ADRs.

### `conformance/`

The 9 conformance dimensions from CR-WSF-17 Rev.1 §25:

- Semantic Conformance
- Identity Conformance
- Reference Conformance
- Relationship Conformance
- Assertion Conformance
- Provenance Conformance
- Specialization Conformance
- API Conformance
- Serialization Conformance

### `serialization/`

Specifications for representing WSF concepts in various formats. **Per CR-WSF-17 Rev.1 §9: technology choices implement the semantic architecture; they do NOT define it.**

### `namespace/`

The WSF namespace strategy. Will be specified by ADR-WSF-21.

---

## Status

This repository is being established per CR-WSF-17 Rev.1. Initial specifications will be authored under subsequent ADRs (ADR-WSF-18 through ADR-WSF-22).

**Platform neutrality principle**: RDF/OWL/JSON-LD are implementation choices, not semantic commitments. The semantic commitments live here.

---

## Related Repositories

- [wsf/](../wsf/) — Canonical semantic assets
- [wsf-governance/](../wsf-governance/) — ADRs, CRs
- [wsf-software/](../wsf-software/) — Engine implementation
- [wsf-examples/](../wsf-examples/) — Reference applications

---

*This is the normative home of WSF specifications. Changes occur only through the ADR/CR process.*
