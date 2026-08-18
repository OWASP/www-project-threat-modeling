---

layout: col-sidebar
title: OWASP Threat Modeling Project
tags: threatmodeling
level: 2
type: documentation
pitch: Threat modeling information, techniques, and methodologies

---

**Status:** Maintained Project Guidance

This documentation project is the maintained entry point for OWASP Threat Modeling Project resources.
It connects current guidance, community references, tools, examples, and historical material while recognizing that there are various threat modeling methodologies.

This project provides information on threat modeling techniques for applications of all types, with a focus on current and emerging techniques.

## New to threat modeling? Start here

Use [Shostack's Four Question Framework][fourq] as a methodology-neutral starting point:
 
1. **What are we working on?** Understand the project scope, and possibly the system, users, dependencies, assumptions, or trust boundaries.
2. **What can go wrong?** Identify threats, misuse cases, design assumptions, and security or privacy concerns.
3. **What are we going to do about it?** Prioritize risks and define mitigations, design changes, tests, or follow-up work.
4. **Did we do a good job?** Review outcomes, track decisions and assumptions, and revisit remaining risks over time.

The [Threat Modeling tab][tmtab] introduces the practice, the [Application Threat Modeling tab][apptm] describes a practical application workflow, the [AI and Agentic Threat Modeling page][aitm] covers AI components, and the [Resources tab][res] lists tools, references, and related OWASP projects.

This project will gather techniques, methodologies, tools and examples. We will group these using the four questions. This will allow people to easily find advice they can use.

Example: if you are looking for different diagramming techniques you will want to look for all the techniques answering the question "What are we working on."

### Methodology-neutral positioning

The OWASP Threat Modeling Project does not define a single official OWASP threat modeling methodology. The project documents a wide range of approaches, including STRIDE, PASTA, LINDDUN, attack trees, abuse cases, and other community practices.

Different methods may be appropriate depending on system context, security and privacy goals, team maturity, delivery model, and regulatory needs. Contributions should explain their scope, assumptions, and intended use so practitioners can choose and adapt approaches responsibly.

### Guiding principles:

This project follows a number of principles that all contributions must adhere to:

- We are vendor, methodology and tool independent: we strive to have examples in as many methodologies and/or tools as possible. 
- Open discussion is promoted: all topics are open for discussion with just one rule: don't be a jerk. If you feel information is lacking or missing, let us know via the OWASP #threat-modeling slack channel.
- We come to an agreement: we discuss things mainly in google docs and on slack, if the project leaders feel a consensus is made, we will publish the content to our main website. All published content can be changed by submitting change requests on the Github repository that serves the website. 

[aitm]: https://owasp.org/www-project-threat-modeling/resources/ai-tm
[apptm]: https://owasp.org/www-project-threat-modeling/#div-application-tm
[fourq]: https://github.com/adamshostack/4QuestionFrame
[res]: https://owasp.org/www-project-threat-modeling/#div-resources
[tmtab]: https://owasp.org/www-project-threat-modeling/#div-threatmodeling

