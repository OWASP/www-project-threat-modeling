---

title: ai-tm
displaytext: AI and Agentic Threat Modeling
layout:  null
tab: true
order: 3
tags: threatmodeling

---

## AI and Agentic Threat Modeling

This page extends the "When to Threat Model" guidance on the [Application Threat Modeling tab][apptm] for adaptive and agentic components. It assumes you are already familiar with the general threat modeling process described there.

### Refresh Triggers for Adaptive and Agentic Components

The general guidance assumes a change is visible in the architecture or dataflow. Agentic components do not always meet that assumption: their behaviour, authority, or effects can shift between deployments without any visible change to either. A threat model can become stale even when the architecture and dataflow look unchanged.

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

### Noticing that a Trigger has Fired

None of the changes above need a code change that appears in a normal diff of services or dataflow, and few of them respect a feature's development cycle: a tool is added, a policy flag flips, or a model is bumped long after the feature was considered done. They arrive in configuration, instructions, and tool registries instead, so the practical answer is to make those artifacts the thing that gets reviewed.

The unifying idea is that granting a tool or a permission to an agent is the same kind of act as granting an IAM permission to a service account, and deserves the same review cadence, the same record of who approved it, and the same periodic recertification. It usually does not get that, because it ships as a one line addition to a list rather than as an infrastructure change.

In practice:

- **Keep an explicit capability manifest, separate from the architecture diagram.** A versioned, checked in list of what the component can actually do: every tool it can call, and which of those cause an external effect such as moving value, contacting a user, deleting data, or calling a third party, rather than only reading. The architecture diagram answers "what services exist"; the capability manifest answers "what can this component make happen", and it is the second one that drifts silently.
- **Gate changes to that manifest the way an IAM policy change is gated.** Require a named reviewer from outside the feature team on any change to the tool registry, to the permissions described in the system instructions, or to a flag that unlocks a tool.
- **Pin the threat model to the manifest and check it in CI.** Record which version of the capability manifest the threat model was last reviewed against, and fail the build when the manifest changes but that pointer does not. This turns "did anyone notice" into a mechanical gate rather than something a person has to remember.
- **Ask the question in the pull request template.** "Does this add a tool, widen an existing tool's scope, or give the component a new data source it can act on?" Most changes answer no in a second; the ones that answer yes are exactly the ones that needed someone to stop and think.
- **Watch runtime tool invocation for drift, not only pre-deploy review.** A reworded instruction can make a model willing to reach for a tool it already had, in a context it had never used it in before. Alert on a rarely used tool spiking in use, or on a tool being invoked from an intent or code path it has never been paired with. No diff would show this, because the capability was there all along.
- **Scope model and provider changes to an evaluation rather than a blanket re-review.** An upgrade can change how liberally an ambiguous request is interpreted. Re-run the safety and red team evaluation suite before rollout and treat a material shift in those results as the trigger, rather than the version number itself.

As a checklist, each control paired with the drift it is there to catch:

| Check | What it catches |
| --- | --- |
| A capability manifest exists, is versioned in the repository, and marks which tools cause an external effect | A tool added or widened with no architecture change behind it |
| Changes to the manifest require a named reviewer from outside the feature team | A grant approved only by the person who wants it |
| The threat model records the manifest version it was last reviewed against, enforced in CI | A manifest change that nobody carried through to the model |
| The pull request template asks whether the change adds a tool, widens a tool's scope, or adds a data source the component can act on | The one line change that looked routine |
| Runtime alerting on unusual tool invocation: a rarely used tool spiking, or a tool called from an intent it has never been paired with | Behaviour drift with no diff behind it at all |
| The safety and red team evaluation suite is re-run before a model or provider change ships | An upgrade that interprets the same instructions more liberally |

Where none of this exists yet, the fallback is a standing agenda item: at each release review, ask what the component can do now that it could not do at the previous release.

### Refresh Heuristic: Four Questions

Do not repeat the entire exercise. Focus on the change, and ask four questions:

1. What new authority or trusted context was introduced?
2. Which untrusted inputs can influence its use?
3. What security, privacy, safety, or operational consequence can result?
4. How is the action constrained, approved, observed, tested, and reversed?

This is a refresh heuristic, not a separate threat modeling methodology.

### Example Scenario

Say a customer support agent starts out only searching documentation and drafting replies, then is later allowed to issue refunds. The architecture may look the same, but its authority and potential consequences have changed.

Refreshing the model around that change:

1. **What new authority or trusted context was introduced?**
    - the identity that authorises the refund, and the limit of what it may authorise
2. **Which untrusted inputs can influence its use?**
    - customer controlled content in tickets, messages, and attachments
    - retrieved documentation or conversation history the agent treats as instruction
3. **What security, privacy, safety, or operational consequence can result?**
    - value leaves the business on a mistaken or fraudulent request
    - duplicate or recursive execution repeats the same refund
4. **How is the action constrained, approved, observed, tested, and reversed?**
    - transaction and frequency limits
    - human approval above a threshold
    - audit evidence linking each refund to the request that caused it
    - detection and reversal of an incorrect refund

### Further Reading

- [OWASP Multi-Agentic System Threat Modeling Guide][masguide]
- [OWASP Top 10 for Agentic Applications][agentictop10]

[agentictop10]: https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/
[apptm]: https://owasp.org/www-project-threat-modeling/#div-application-tm
[masguide]: https://genai.owasp.org/resource/multi-agentic-system-threat-modeling-guide-v1-0/
