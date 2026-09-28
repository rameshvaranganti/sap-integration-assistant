# SAP Integration Assistant (Agent Skill)

An Agent Skill for SAP Integration Suite work: Cloud Integration (CPI), API Management, Event Mesh, Integration Advisor, and SAP-to-external-system integrations.

Created by Rameshkumar Varanganti.

## What it does

- **Development**: Groovy scripts, mappings, XSLT, headers and properties, payload transformations
- **Architecture**: sync vs async patterns, APIs and events, authentication, retries, idempotency, monitoring, error handling
- **Troubleshooting**: evidence-first analysis of logs, payloads, and configs, with ranked hypotheses and verification steps
- **Performance**: payload processing, mappings, external calls, batching, concurrency
- **Reviews**: correctness, security, runtime compatibility, null handling, namespaces, encoding, time zones, sensitive logging
- **Accuracy**: prefers official SAP documentation, never invents APIs or SAP Notes, and separates static analysis from tested behavior

## Install

**Claude.ai / Claude Desktop**: zip the `sap-integration-assistant` folder (the folder itself must be the top level of the zip), then go to Settings > Capabilities, enable code execution and Skills, and upload the zip.

**Claude Code**: copy the `sap-integration-assistant` folder into `~/.claude/skills/` (personal) or `.claude/skills/` in your project.

**Claude API**: upload it through the Skills API (see Anthropic's Skills documentation).

The skill follows the open Agent Skills format, so other compatible tools can use the same folder.

## Structure

```
sap-integration-assistant/
├── SKILL.md
└── references/
    ├── groovy-cpi-patterns.md
    └── troubleshooting-and-review.md
```

## Disclaimer

Not an official SAP product. Generated code and designs are AI-produced and are not tested on your SAP runtime. Review and test everything in a non-production tenant, verify against help.sap.com, and never share credentials, tokens, or personal data.

## License

Add a license of your choice (for example MIT) before publishing.
