# SAP Business AI Platform, MCP and API-to-AI reference

Context as of October 2026, taken from SAP documentation and SAP Community. Everything here is version-dependent. Exact UI labels, availability, regions, licensing and prerequisites (for example the Integration Cell runtime) change quickly, so tell the user to verify on help.sap.com before acting. If asked about something newer than this file or not listed here, say you are not sure and point to help.sap.com, SAP Community or the SAP Business Accelerator Hub.

## Contents
1. SAP Business AI Platform (BAIP) and naming
2. MCP Server in Integration Suite (MCP Gateway)
3. Creating an MCP server: typical flow
4. API-to-AI design guidance
5. Other AI features in Integration Suite
6. MCP, A2A and where Integration Suite fits
7. Answering questions in this area

## 1. SAP Business AI Platform (BAIP) and naming

- At SAP Sapphire (May 2026) SAP introduced SAP Business AI Platform. It unifies SAP Business Technology Platform (BTP), SAP Business Data Cloud and SAP Business AI into one governed foundation for building, running and governing agentic AI.
- SAP Integration Suite, SAP Build, CAP, Kyma, Generative AI Hub, AI Core and Joule Studio remain the building blocks. Existing iFlows, APIs and skills stay valid.
- Naming can be mixed in documentation, UIs and contracts during the transition. Say "BAIP (formerly SAP BTP)" when it helps the reader, and use the specific service names (for example Cloud Integration, API Management) for technical detail.

## 2. MCP Server in Integration Suite (MCP Gateway)

- The MCP Server capability is realized through the MCP Gateway. It exposes APIs, tools and backend services as MCP-compatible endpoints for AI agents.
- The gateway provides authentication, authorization, rate limiting, payload protection and monitoring.
- The MCP server can be synchronized when the source API changes.
- For multi-system orchestration, SAP guidance is to build an iFlow, expose it as a managed API artifact, then create the MCP server from that artifact.
- AI-assisted OpenAPI specification generation exists for APIs that have no specification.

## 3. Creating an MCP server: typical flow

1. In Integration Suite go to Design > Integrations and APIs > Artifacts > Add > MCP Server.
2. Choose a source: an API artifact deployed on Integration Cell, an HTTP endpoint with an OpenAPI 3.0 specification, or an RFC-based backend.
3. Select the operations to expose as tools. Write clear tool descriptions.
4. Apply policies: authentication (inherited from a source API), quota, spike arrest.
5. Deploy to Integration Cell.
6. Optionally publish to Developer Hub.
7. Test with an MCP client such as MCP Inspector, VS Code, Cline or Claude Desktop.

Label menu paths and step order as version-dependent and ask the user to confirm against current documentation.

## 4. API-to-AI design guidance

- Do not expose every endpoint one-to-one as a tool.
- Design a small set of tools around business outcomes.
- Write precise tool descriptions and input schemas so an agent knows when and how to call each tool.
- Start read-only.
- Apply least privilege, rate limits and audit logging.
- Keep humans in the loop for write actions.

## 5. Other AI features in Integration Suite

- The AI adapter (receiver) connects iFlows to Generative AI Hub.
- AI-assisted development can build iFlows from natural-language prompts.
- Validate AI-generated iFlows and mappings like any other artifact: review, deploy to a non-production tenant, trace and test with realistic payloads.

## 6. MCP, A2A and where Integration Suite fits

- MCP is agent-to-tool. A2A is agent-to-agent. Joule can act as an A2A client.
- SAP Integration Suite is positioned as the integration and governance layer for agents.

## 7. Answering questions in this area

- State what is documented, what is reasoned and what needs verification (Confirmed, Likely, Hypothesis).
- For "how do I expose API X as an MCP server", give the flow above with tool-design advice from section 4, then list prerequisites to verify (Integration Cell runtime, licensing, region, permissions).
- For "what does BAIP mean for my landscape", explain that existing BTP services and artifacts remain valid, flag naming transitions, and recommend checking contracts and documentation for exact service names.
- Never invent menu names, policy names, service plans, limits or release dates.
