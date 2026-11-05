.. raw:: latex

   \pagestyle{plain}
   \thispagestyle{plain}

.. _wg-charter:

FG-TIDA WG2: Identity, Behaviour and Enforcement for AI Agents (IBEA)
=====================================================================


Charter Information
-------------------

.. list-table::
   :header-rows: 0
   :widths: 30 70

   * - **Charter version**
     - 0.4

   * - **Date**
     - 2026-11-03

   * - **Status**
     - Draft (provisional working group, subject to approval at the first FG-TIDA meeting)


1. Group Information
--------------------

..
   MANDATORY

.. list-table::
   :header-rows: 1
   :widths: 38 62

   * - Field
     - Content

   * - Working group name and acronym
     - WG2: Identity, Behaviour and Enforcement for AI Agents (IBEA); name to be confirmed by the co-chairs

   * - FG-TIDA theme(s) covered
     - FG-TIDA/themes#4 and FG-TIDA/themes#6, joined in FG-TIDA/themes#36, with any further themes grouped into this working group by the FG-TIDA management

   * - Chair(s) / co-chairs
     - Artur Hecker (Huawei Technologies); Cyril Gorlla (CTGT). Provisional, subject to approval at the first FG-TIDA meeting

   * - Editor(s) of the main deliverables
     - To be agreed by the working group

   * - Mailing list
     - Moderated WG2 list, to be created by the FG-TIDA Secretariat

   * - Repository and issue tracker
     - https://github.com/fg-tida-wg2 (charter: wg2-ibea-charter)

   * - Charter status and version
     - Draft, version 0.4


2. Background and Problem Statement
-----------------------------------

..
   MANDATORY

A verified identity and a valid authorization say little about what an AI agent will do on a given task. The non-deterministic, creative behaviour of AI agents is what distinguishes them from conventional software, and it is also why the security policies written for conventional software fit them poorly.

1. Identity does not determine behaviour. An AI agent that passes every identity and authorization check can still take an action outside the authority it was granted. A re-run is generally not the same as the run: the same agent may respond differently to the same request even when its model, tools and composition are unchanged. When major components or the configuration change (for example the model or the guardrails), the behaviour changes further. An identity issued at one point therefore says less about the agent that acts later.

2. Security policy is not written for agents. Classical security policy names subjects, objects and the operations allowed between them. Agents are deployed because their action space cannot be listed in advance: they are meant to handle known unknowns. A policy written as a list of permitted operations either confines the agent until its purpose is lost or leaves its behaviour unconstrained. There is no agreed way to express a policy in terms of wanted and unwanted outcomes, so that it can be enforced when an agent is the subject or the object of an action.

3. Revocation does not reliably stop conduct. Revoking an identity or a right takes effect only where an enforcement point checks it again before the next action.

4. Enforcement decisions are not portable. Where an action is checked at all, the decision usually ends as an internal log entry that another party can neither recompute nor rely on.

Existing work addresses agent identity (ITU-T X.1285, X.402, IETF WIMSE, IETF AgentProto, the W3C Agentic Web charter, Poppy/PACT), what an agent may access in general (OASIS XACML and attribute-based access control, PACT JWT) and the platform it runs on (IETF RATS, Trusted Computing, secure enclaves). None of it addresses how a security policy is expressed and enforced when its subjects or objects are agents whose behaviour changes from one run to the next. The working group addresses that gap. Whether a third party can later check an enforcement decision is a secondary property, examined together with FG-TIDA WG1.

The unit of analysis is the enforcement decision for one action: the decision taken at an enforcement point, when the action is attempted, against the policy in force. Sequences of actions, delegation chains and longer-running tasks are treated as series of such decisions, which keeps the paths comparable without limiting the work to single actions.


3. Goals
--------

..
   MANDATORY

* The working group will describe the problem: terminology, environment, threat cases and a requirements set against which every solution path is assessed.

* The working group will specify requirements for enforcing security policy when the subject or the object is an AI agent: how a policy must be expressed so that it can be enforced, the decisions an enforcement point can reach and what each one means, how a decision is reached when policies collide, and how the absence of any decision is stated. It will specify requirements, not encodings or protocols.

* The working group will describe and compare solution paths against the shared requirements, starting with identity based on agent design properties that do not change, and with security policy expressed as intent, in terms of wanted and unwanted outcomes rather than the subjects and objects involved.

* The working group will maintain shared evaluation fixtures so that paths can be compared on the same cases.

* The working group will take account of previous work and the state of the art, including ITU-T X.1285, OASIS XACML, IRTF RFC 9315, IETF RATS and EAT, and IETF WIMSE, adding further work as it starts.


4. Scope and Non-Goals
----------------------

In Scope
~~~~~~~~

* Characterization of the identity-behaviour-enforcement mismatch, grounded in use cases submitted to FG-TIDA.

* State of the art of the relevant standardization and research on agent identity and on methods, including cryptographic methods, for enforcing behaviour.

* Requirements for enforcement decisions on agent actions. The decision outcomes are permit, remediate, block, escalate and indeterminate, with an attributed statement that no decision was taken kept apart from them. The mechanisms an enforcement point can apply to reach or carry out a decision, such as identifying, limiting or correcting an action, are described separately from the outcomes. The requirements also cover an escalated action while it awaits release, and an action whose delegation or credential is revoked between authorization and execution.

* Identity schemes for agents whose composition changes, based on design invariants and their dependencies.

* Expression of security policy as intent, and the coexistence of intent-based and legacy security policies at a common enforcement point.

* Further solution paths proposed for the same problem, such as least-agency enforcement and cryptographic enforcement boundaries, assessed against the same requirements.

* Shared fixtures and test cases for comparing paths, including use on the FG-TIDA use-case testbed.


Out of Scope / Non-Goals
~~~~~~~~~~~~~~~~~~~~~~~~

* The working group will not define encodings, schemas, wire formats or protocols.

* The working group will not rank, certify or recommend products, nor run evaluations as a service.

* The working group will not make legal determinations of any party's standing or liability.

* The provenance and standing of the authority behind a policy is addressed by the work under FG-TIDA/themes#5. This working group takes the authored policy as an input.

* The record that carries a decision, and the properties any carried claim needs, are addressed by the work under FG-TIDA/themes#1.

* Remote attestation mechanisms are addressed by FG-TIDA WG1.

* Release authority for escalated actions, and human oversight operations generally, are addressed by the work under FG-TIDA/themes#16.

* The declaration of collective-choice operators is addressed by the work under FG-TIDA/themes#18; the design-time method for choosing them is addressed by SG17 Question 1 (X.dmst).

* Population-scale reading of decisions is addressed by the work under FG-TIDA/themes#21.

* Whether a connection between parties should exist and remain in force is addressed by the work under FG-TIDA/themes#29.

* Identity issuance and lifecycle in general are addressed by ITU-T X.1285 and related SG17 work.


5. Programme of Work and Deliverables
-------------------------------------

..
   MANDATORY

.. list-table::
   :header-rows: 1
   :widths: 6 29 45 20

   * - #
     - Deliverable
     - Short description
     - Input documents

   * - 1
     - Problem statement and requirements (technical report)
     - Terminology, environment, threat cases and the requirements set against which every path is assessed.
     - FG-TIDA/themes#4, #6 and #36; submitted use cases

   * - 2
     - Enforcing security policy on agent actions: requirements (technical specification)
     - Policy expression for enforceability, decision outcomes and their meaning, decisions under policy collision, escalation pending release, and the statement that no decision was taken.
     - FG-TIDA/themes#6; least-agency requirements contributed on #4

   * - 3
     - Agent identity under changing composition: solution paths and analysis (technical report)
     - Identity based on design invariants and their dependencies, and further identity paths, each assessed against deliverable 1.
     - FG-TIDA/themes#4 path one

   * - 4
     - Intent-based security policy: solution paths and analysis (technical report)
     - Policy expressed as wanted and unwanted outcomes, its coexistence with legacy policy at a common enforcement point, and further policy paths, each assessed against deliverable 1.
     - FG-TIDA/themes#4 path two; #6 tasks 1 and 2; #26

   * - 5
     - Shared evaluation fixtures (technical report with versioned fixture set)
     - Versioned cases with expected outcomes and negative controls, usable across paths and on the use-case testbed.
     - TIDA6-FX fixture posted on FG-TIDA/themes#6; FG-TIDA/use-cases#4 mappings; evidence-graded verdict worked examples with expected outcomes (one positive and three negative cases), contributed on FG-TIDA/themes#42


6. Milestones
-------------

..
   MANDATORY

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Target date
     - Milestone

   * - First FG-TIDA meeting, Paris (2026-12)
     - Charter presented; outline of deliverable 1 available in the repository.

   * - Second FG-TIDA meeting, Geneva (2027-01)
     - First draft of deliverable 1 and outline of deliverable 2 available; deliverable 5 fixture set aligned with the draft requirements.

   * - Third FG-TIDA meeting (2027)
     - Deliverable 1 agreed by the working group; first drafts of deliverables 2, 3 and 4 available.

   * - Fourth FG-TIDA meeting (2027)
     - Deliverables 2 and 5 agreed by the working group and submitted to the FG-TIDA plenary.

   * - Final FG-TIDA meeting
     - Deliverables 3 and 4 agreed and submitted to the FG-TIDA plenary.


7. Coordination, Dependencies and Liaisons
------------------------------------------

..
   MANDATORY

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Group / Organization
     - Coordination or dependency

   * - FG-TIDA WG1
     - Attestation results as inputs to enforcement decisions, and the interface between the two groups; design invariants as claims an attestation can carry.

   * - Work under FG-TIDA/themes#1
     - Record format that carries a decision and the statement that no decision was taken.

   * - Work under FG-TIDA/themes#5
     - Authored policy and the standing of its author.

   * - Work under FG-TIDA/themes#16
     - Release of escalated actions and handling of indeterminate decisions.

   * - Work under FG-TIDA/themes#18 and #21
     - Declared operators that decisions are checked against, and population-scale reading of decisions.

   * - Work under FG-TIDA/themes#44
     - Binding of evaluation results to the artefact, method and moment.

   * - ITU-T SG17 Question 1 and Question 16
     - X.dmst (design-time aggregation), XSTR.magAI-behavior and X.aplm-aia, complemented without duplication.

   * - IETF RATS and WIMSE
     - Followed as adjacent work; no liaison established.


8. Terminology
--------------

..
   OPTIONAL

The working group will use the common FG-TIDA terminology where applicable. New terms will be communicated to the FG-TIDA terminology and use cases working group.

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Term
     - Meaning

   * - Security policy
     - The versioned statement of authority that an action is checked against, whether expressed classically or as intent.

   * - Enforcement point
     - The place where an attempted action is checked against the policy in force and the decision is applied.

   * - Enforcement decision
     - The result of checking one action against the policy in force: permit, remediate, block, escalate or indeterminate.

   * - Stated absence of a decision
     - An attributed statement that no check was performed, distinct from any decision and never read as permission.


9. Working Methods
------------------

..
   OPTIONAL

Each deliverable will be tracked in its own issue in the working group repository. Fixtures will be versioned, and changes to expected outcomes will be listed in a changelog. Virtual interim calls will be held between plenary meetings. Contributions folded into a deliverable will remain attributed at clause level.


10. Security and Privacy Considerations
---------------------------------------

..
   OPTIONAL - RECOMMENDED

The deliverables will address the following: a decision or a policy can disclose information its owner needs to keep confidential, so verification without full disclosure is required; the enforcement point is itself an attack surface, including for injected instructions; a suppressed decision must be distinguishable from the absence of any check; and identifiers built from design invariants can make agents and their operators linkable.


11. Success Criteria and Conclusion
-----------------------------------

..
   OPTIONAL

The working group will have completed its chartered work when deliverables 1 to 5 have been submitted to the FG-TIDA plenary.

Following completion, the deliverables may be offered as input to ITU-T Study Groups or other relevant standards bodies, as decided by the Focus Group.


12. Revision History
--------------------

..
   MANDATORY

.. list-table::
   :header-rows: 1
   :widths: 18 22 60

   * - Version
     - Date
     - Change

   * - 0.1
     - 2026-10-26
     - First draft on the FG-TIDA charter template, from the first pass of 6 October 2026 and FG-TIDA/themes#36

   * - 0.2
     - 2026-10-27
     - WG2 designation, provisional co-chairs and repository added

   * - 0.3
     - 2026-10-30
     - Moved into the WG2 repository; destination of deliverables left open, per the co-chairs' preparation meeting

   * - 0.31
     - 2026-10-30
     - Wording changes throughout; non-determinism of agents even when their composition is unchanged, per FG-TIDA/themes#4; scope extended beyond third-party checking to enforcement. Comments added in the source.

   * - 0.4
     - 2026-11-03
     - Comments on 0.31 resolved: problems 1 and 2 merged, and a problem added on policy expression and enforcement; the gap stated as enforcement, with third-party checking secondary; the unit of analysis stated as the enforcement decision for one action, with sequences treated as series of decisions; decision outcomes kept apart from enforcement mechanisms; solution paths split into deliverables 3 (identity) and 4 (intent-based policy); wording made less specific throughout.
