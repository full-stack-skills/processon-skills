# Operations Reference

## Error decisions

| Signal | User-facing response | Retry |
|---|---|---|
| Missing environment value | Identify `PROCESSON_MCP_AUTHORIZATION` and show the placeholder form | None |
| 401 | Authentication is unavailable or expired | None |
| 407 | ProcessOn rate limit was reached | At most 3 attempts with backoff |
| Transient connection or 5xx | ProcessOn is temporarily unavailable | At most 3 attempts |
| Invalid input | Name the missing structural fact or correct a deterministic formatting issue | No blind retry |
| Empty or inaccessible artifact | Preserve diagnostic metadata and request one regeneration | At most once |

Never reveal raw headers, stack traces containing request data, session identifiers that grant access, or credential-like strings.

## Multi-part requests

When one request genuinely needs different diagram families, split it into named deliverables and process them in the user's priority order. Do not merge unrelated topologies into a crowded single canvas. Reuse terminology and palette across the set.

## Acceptance checks

For live acceptance, record only diagram category, result URL or non-secret ID, timestamp, and review verdict. A visually inspected architecture diagram, swimlane, and infographic demonstrate breadth; they do not prove every upstream ProcessOn template.

## Common anti-patterns

- Directory tree presented as architecture: replace it with runtime boundaries, dependencies, protocols, and flows.
- Decorative prompt with no topology: define entities and relationships before style.
- Unlimited aesthetic regeneration: review once, correct specific defects once, then stop.
- Credential embedded in `.mcp.json`: map the header to the runtime environment instead.
- Claiming edit support without a returned editable artifact: state the upstream limitation.

## Deep FAQ

1. **Can the plugin edit any existing ProcessOn document?** Only when the available MCP result or future tool contract identifies and supports that document.
2. **Why not always request DSL?** The default visual tool is the shortest route; DSL is useful for audit, reuse, and debugging.
3. **What if the desired diagram type is unsupported?** Choose the closest documented family and disclose the mapping before generation.
4. **What if labels are too long?** Condense them while preserving meaning; move supporting prose outside node labels.
5. **What if the result URL is inaccessible?** Preserve non-secret metadata and perform at most one regeneration.
6. **Can a token be saved in the repository?** No. Configure the complete authorization value in the runtime environment.
7. **Can attachments be sent automatically?** No. Uploading requires explicit authorization for the files and destination.
8. **How are multiple outputs kept consistent?** Reuse terminology, palette, shape grammar, and reading direction across the set.

## Customization examples

- Developer review: dark-blue technical palette, dense but readable, explicit protocols and trust boundaries.
- Executive report: light neutral surface, few high-value nodes, outcome-first reading order.
- Chinese operations training: approachable blue-green palette, left-to-right flow, plain-language labels and visible exception paths.
