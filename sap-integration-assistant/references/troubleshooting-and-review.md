# Troubleshooting template and review checklist

## Contents
- Troubleshooting template
- Common failure areas
- Review checklist

## Troubleshooting template

Use this structure for every troubleshooting answer.

1. **Evidence** (only what the log, payload, or config actually shows): error text, status codes, step where it fails, timestamps, sizes.
2. **Not known yet**: what is missing that would change the diagnosis.
3. **Hypotheses**, ranked by likelihood, each labeled Likely or Hypothesis, with the reasoning.
4. **Verification** for each hypothesis: the quickest check that confirms or rules it out (which log or trace to open, which setting to compare, which test call to make).
5. **Fix options** once a cause is confirmed, with side effects.

Never state a cause as fact until a verification step supports it.

## Common failure areas (starting points, not conclusions)

- Connectivity and TLS: certificate chain or trust store problems, hostname mismatch, proxy or firewall, timeouts.
- Authentication: expired or wrong credentials or tokens, wrong scope or audience, clock skew, wrong credential alias.
- Payload and mapping: null or missing nodes, namespace mismatch, wrong encoding, unexpected structure, oversized messages.
- Processing: exceptions swallowed in scripts, wrong routing conditions, splitter or aggregator misconfiguration.
- Delivery and retries: duplicate messages, retry loops, queue backlog, missing idempotency handling.

## Review checklist

**Correctness**: matches the contract, handles optional and repeated elements, correct routing and conditions.
**Robustness**: null and blank handling, meaningful errors, no swallowed exceptions, sensible retries and timeouts.
**Data handling**: namespaces, JSON/XML structure, encoding, date and time zone conversion, number formats.
**Security**: no secrets in code or logs, secure parameters or credential store, least privilege, no sensitive payload logging, input validation.
**Compatibility**: uses only APIs available in the target runtime, no deprecated features, adapter options verified against current documentation.
**Maintainability**: clear naming, small focused scripts, comments for non-obvious logic, reuse instead of copy-paste.
**Performance**: payload size, parsing approach, repeated calls, batching, logging overhead.
**Operations**: monitoring and alerting, traceable identifiers in the message log, recovery path for failed messages.

Report findings by severity (high, medium, low), each with a concrete fix.
