---

title: ai-tm
displaytext: AI and Agentic Threat Modeling
layout:  null
tab: true
order: 4
tags: threatmodeling

---

## AI and Agentic Threat Modeling

This page extends the "When to Threat Model" guidance on the [Application Threat Modeling tab](https://owasp.org/www-project-threat-modeling/#div-application-tm) for adaptive and agentic components. It assumes you are already familiar with the general threat modeling process described there.

### Refresh Triggers for Adaptive and Agentic Components

The general guidance assumes a change is visible in the architecture diagram or dataflow. Agentic components do not always meet that assumption: their behaviour, authority, or effects can shift between deployments without any visible change to the diagram. A threat model can become stale even when the system diagram looks unchanged.

Adaptive and agentic components may gain new authority, new context, or the ability to create external effects. Refresh the relevant part of the threat model when any of these change:

- **Tools and actions:** APIs, plugins, MCP servers, commands, write operations, or other executable capabilities.
- **Identity and authority:** Credentials, service identities, delegated permissions, impersonation rights, scopes, or tenant access.
- **Instructions and policy:** System instructions, agent policies, routing rules, guardrails, or approval conditions.
- **Models and providers:** Model versions, hosting providers, model routing, or fallback behaviour.
- **Memory and context:** Retrieval sources, long term memory, vector stores, user history, or shared context.
- **Human oversight:** Approval steps that are added, removed, delayed, bypassed, or moved after an action.
- **Orchestration:** A component becomes multi-agent, delegates work, or assigns tools and permissions dynamically.
- **Consequences:** An advisory output can now modify infrastructure, transfer value, contact users, change records, or execute code.
- **Detection and recovery:** Logging, evaluation thresholds, anomaly detection, rollback, revocation, or emergency stop behaviour.

Do not repeat the entire exercise. Focus on the change.

Ask four questions:

1. What new authority or trusted context was introduced?
2. Which untrusted inputs can influence its use?
3. What security, privacy, safety, or operational consequence can result?
4. How is the action constrained, approved, observed, tested, and reversed?

For example, a customer support agent may initially search documentation and draft replies.

It is later allowed to issue refunds. The architecture may look similar, but its authority and potential consequences have changed.

Refresh the model around:

- the identity that authorises the refund
- transaction and frequency limits
- influence from customer controlled content
- duplicate or recursive execution
- human approval
- audit evidence
- detection and reversal of an incorrect refund

This is a refresh heuristic, not a separate threat modeling methodology.

### Further Reading

- [OWASP Multi-Agentic System Threat Modeling Guide](https://genai.owasp.org/resource/multi-agentic-system-threat-modeling-guide-v1-0/)
- [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
