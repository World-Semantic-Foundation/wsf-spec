# wsf-spec : WSF Normative Specifications

> **The normative machine-readable specifications for the World Semantic Foundation.**
>
> Implements ADR-WSF-23 (Semantic Representation Architecture) and provides the canonical conformance artifacts for all 38 WSF concepts.

## Overview

The WSF specification artifacts provide machine-readable, normative definitions of:

- All 38 WSF concepts (12 Tier 1 + 9 Tier 2 + 16 Tier 3 + 1 Capability example)
- All core entity types (Concept, Relationship, Assertion, Proposition, Provenance, Validity, Evidence)
- All 12 relationship kinds (per ADR-WSF-19)
- The 6-stage semantic status model (per SEMANTIC-STATUS-MODEL)
- REST API surface (per ADR-WSF-24 §7.1)
- gRPC service definitions (per ADR-WSF-24 §7.2)
- SHACL validation shapes for conformance testing

These artifacts are the **single source of truth** for any WSF-compatible implementation. Conformance to wsf-spec is mandatory for the WSF Semantic Engine and any federation partner.

## Specification Artifacts

### OpenAPI 3.1 (`openapi/`)

- `wsf-semantic-engine.openapi.yaml` : 12 REST endpoints across 8 service modules

The OpenAPI spec covers all REST endpoints of the WSF Semantic Engine with full request/response schemas, JSON-LD content types, OAuth 2.0 + OIDC authentication, and 9 reusable component schemas (Concept, Relationship, Assertion, Proposition, Provenance, Validity, Evidence, Namespace, AuditEntry).

### SHACL Shapes (`shacl/`)

- `wsf-shapes.ttl` : 7 shapes for validating WSF entity conformance

The SHACL shapes cover Concept, Relationship, Assertion, Provenance, Validity, Proposition, and Evidence. Each shape enforces CURIE patterns, ISO 8601 timestamps, status enum membership, and closed-shape constraints (no additional properties).

### Protocol Buffers (`protobuf/`)

- `wsf-semantic-engine.proto` : gRPC service definitions for high-throughput consumers

The Protobuf schema defines 25 message types, 5 enums (SemanticStatus, ConceptTier, RelationshipKind, AssertionLifecycle, EvidenceType, ValidityStatus, Severity, ResolutionStrategy, ValidationLanguage, ChangeType, AuditAction, Modality), and 7 service interfaces with bidirectional streaming for change notifications.

### Turtle / RDF (`turtle/`)

- `wsf-vocabulary.ttl` : Canonical RDF representation of all 38 concepts

The Turtle serialization provides the SKOS-aligned, OWL-compatible machine-readable vocabulary for federation with external semantic web ecosystems (Schema.org, SKOS, Dublin Core, OWL ontologies).

### JSON Schema (`../wsf-software/schemas/json/`)

7 JSON Schema files for validating WSF entity representations in REST/JSON contexts:
- concept.schema.json
- relationship.schema.json
- assertion.schema.json
- proposition.schema.json
- provenance.schema.json
- validity.schema.json
- evidence.schema.json

## Conformance Levels

Per ADR-WSF-23 and CR-WSF-17 Rev.1 §17, the WSF specification defines 4 conformance levels:

| Level | Requirements | Profile |
|---|---|---|
| **Level 1 (Minimal)** | Turtle + JSON Schema for Concept | Read-only knowledge consumer |
| **Level 2 (Standard)** | Level 1 + SHACL validation | Read-write knowledge producer |
| **Level 3 (Full)** | Level 2 + Protobuf + OpenAPI | Full engine conformance |
| **Level 4 (Federation)** | Level 3 + connector adapters | Multi-system federation |

## Specification Mapping

| Specification | Covers | Format | Status |
|---|---|---|---|
| Concept Catalog | All 38 concepts | Turtle, JSON-LD, YAML | Baseline |
| Entity Schemas | 7 core entities | JSON Schema | Baseline |
| Validation | Concept, Relationship, Assertion | SHACL | Baseline |
| REST API | 12 endpoints | OpenAPI 3.1 | Baseline |
| gRPC API | 7 services, 25 messages | Protobuf | Baseline |
| Relationship Types | 12 kinds | Turtle, JSON Enum | Baseline |
| Status Model | 6 stages | JSON Schema, Protobuf | Baseline |

## Usage Examples

### Validate a Concept with SHACL

```bash
# Using pyshacl
pyshacl -s wsf-spec/shacl/wsf-shapes.ttl \
        -e turtle/wsf-vocabulary.ttl \
        --format turtle
```

### Generate gRPC stubs from Protobuf

```bash
protoc --go_out=. --go-grpc_out=. wsf-spec/protobuf/wsf-semantic-engine.proto
protoc --python_out=. --grpc_python_plugin=. wsf-spec/protobuf/wsf-semantic-engine.proto
```

### Validate REST request against OpenAPI

```bash
# Using swagger-cli
swagger-cli validate wsf-spec/openapi/wsf-semantic-engine.openapi.yaml
```

### Validate JSON against JSON Schema

```bash
# Using ajv-cli
ajv validate -s wsf-software/schemas/json/concept.schema.json \
              -d my_concept.json
```

### Load Turtle vocabulary into a triple store

```sparql
LOAD <https://raw.githubusercontent.com/World-Semantic-Foundation/wsf-spec/main/turtle/wsf-vocabulary.ttl>
INTO GRAPH <https://world-semantic-foundation.org/>
```

## Related Repositories

- [wsf/](https://github.com/World-Semantic-Foundation/wsf) : Human-readable concept documentation (38 Markdown files)
- [wsf-governance/](https://github.com/World-Semantic-Foundation/wsf-governance) : Architectural Decision Records
- [wsf-software/](https://github.com/World-Semantic-Foundation/wsf-software) : WSF Semantic Engine implementation
- [wsf-connectors/](https://github.com/World-Semantic-Foundation/wsf-connectors) : Federation adapters

## Architectural References

- **ADR-WSF-23** : Semantic Representation Architecture (5-layer stack)
- **ADR-WSF-25** : Integration Architecture (federation patterns)
- **SEMANTIC-STATUS-MODEL** : 6-stage lifecycle (Candidate, Investigating, Proposed, Normative, Deprecated, Retired)

## License

Apache-2.0

---

*The WSF Normative Specifications. Status: Baseline.*