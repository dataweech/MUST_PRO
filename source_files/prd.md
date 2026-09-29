<h1 align = 'center'> Product Requirement Document </h1>
<a href="https://karet.vercel.app/">
<h1 align = 'center'> Karet </h1>
</a>
<h2 align = "center">AI-Powered Writing Tool</h2>
<a href="https://www.lemonconfidence.site">
<h4 align='right'> Product Owner and Engineer: Lemon Confidence </h4>
</a>


# Table of Content
>- 1.0 [Business](#10-business-overview)
>   - 1.1 [Problem Statement](#11-problem-statement)
>   - 1.2 [Product Initiative](#12-product-initiative)
>- 2.0 [Methodology](#20-case-overview)
>   - 2.1 [Solution Approach](#21-solution-approach)
>   - 2.2 [Objectives](#22-objectives)
>   - 2.3 [Target Persona](#23-target-persona)
>       - 2.3.1 [Primary User](#231-primary-users)
>       - 2.3.2 [Secondary User](#232-secondary-users)
>- 3.0 [MVP Scope](#30-mvp-scope)
>   - 3.1 [Release v1.3.0](#31-release-v130)
>       - 3.1.1 [Release Objective](#311-release-objectives)
>       - 3.1.2 [Actors, User Types, and Permissions](#312-actors-user-types-and-permissions)
>       - 3.1.2.1 [Subscription Types](#3121-subscription-types)
>       - 3.1.2.2 [Workspace & Collaboration Roles](#3122-workspace--collaboration-roles)
>       - 3.1.2.3 [Entitlement & Permission Rules](#3124-subscription-and-collaboration-access-model)
>       - 3.1.2.4 [Subscription and Collaboration Access Model](#3124-subscription-and-collaboration-access-model)
>   - 3.2 [Acceptance Criteria](#32-acceptance-criteria)
>- 4.0 [Expectations for the Release Memo](#40-expectations-for-the-release-memo)
>- 5.0 [Next Steps](#50-next-steps)


# 1.0 Product Overview

## 1.1 Problem Statement
The detailed problem statement and prioritization rationale are documented in [intent.md](../intent.md), Section 2.2.

For this release, the selected problem is the need for an AI-native writing workspace that enables users to create, organize, refine, and continue working on written content within a single environment, while reducing the friction associated with document management and collaborative workflows.

The <code>v1.3.0</code> release specifically extends this experience by introducing email-based collaboration and sharing, allowing users to provide controlled access to their writings without requiring external tools or manual file exchange.
The release therefore addresses two related product needs:

- Individual productivity: enabling users to move from opening the platform to meaningful writing activity with minimal friction.
- Collaborative continuity: enabling users to share and collaborate on written work within the product rather than moving the workflow to external tools.

The broader problem definition, evidence, and prioritization rationale remain governed by [intent.md](../intent.md).

## 1.2 Product Initiative
The product initiative is to develop an AI-native writing and decision-support workspace that combines focused writing, document management, AI-assisted workflows, and collaboration in one environment.

As described in [intent.md](../intent.md), the initiative responds to an increasingly accessible AI-assisted software landscape where generating content and building digital experiences have become easier, but users still require environments that help them think, create, refine, organize, and work with others effectively.

Karet therefore aims to position itself as the writing environment as more than a text editor. The product is intended to provide a structured workspace where users can:

1. create and edit content;
2. organize documents and files;
3. use AI assistance during the writing process (available styles: );
4. resume work without losing context;
5. format content according to its intended use;
6. personalize their working environment; and
7. collaborate with other users where required.

This release directive narrows that broader initiative to the capabilities and validation objectives defined for <code>v1.3.0</code>.

# 2.0 Methodology
## 2.1 Solution Approach
An AI-native writing and decision-support workspace tailored for technical writing and storytelling.
## 2.2 Objectives
The product is intended to establish a focused workspace that supports the complete writing lifecycle from document creation through refinement, organization, and collaboration.
| Objective                                           | Intended outcome                                                                                                      |
| --------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Distraction-free writing environment**            | Enable users to focus on creating and editing content without unnecessary interface complexity with a fragmented experience.                       |
| **Document and file management**                    | Enable users to create, organize, access, and manage their written work within the platform.                          |
| **AI-assisted writing workflows**                   | Enable users to use AI assistance as part of their writing and refinement process.                                    |
| **Multi-tenant real-time collaboration**            | Enable multiple users to work within controlled collaborative spaces while maintaining appropriate access boundaries. |
| **Flexible file exporting**                         | Allow users to download built content from the workspace, into supported formats (such as <code>.txt</code>).                 |
| **Seamless document upload and editing resumption** | Reduce the friction involved in returning to previously uploaded or unfinished work from personal computer.                                  |
| **Diverse content formatting options**              | Support different writing and storytelling requirements through flexible formatting.                                  |
| **Customizable theme configurations**               | Allow users to configure the workspace according to their preferred visual experience.                                |

These objectives describe the broader product direction. <code>v1.3.0</code> does not need to independently deliver every objective; the release scope defines which aspects are being introduced, validated, or carried forward.

That distinction is important for the audit because it prevents the release from being evaluated against capabilities that were not part of the release commitment.

## 2.3 Target Persona
### 2.3.1 Primary Users
1. Technical Writers: Users who create structured technical documentation and require an environment for drafting, editing, organizing, and refining technical information.

2. Research Writers: Users who work with research-driven content and require a persistent workspace for developing, revising, and organizing written material.

3. Storytellers: Users who create narrative or creative content and require a focused writing environment with flexible formatting and AI-assisted refinement.

4. Knowledge Workers: Professionals whose work involves producing, organizing, refining, or communicating information through written documents.

### 2.3.2 Secondary Users
5. Content Teams: Teams that produce and review written content collaboratively.

6. Collaborative Writing Groups: Multiple users who need controlled access to shared writing projects.

7. Independent Creators: Individuals who manage their writing and content production independently but may occasionally require collaboration.

8. External/Integrated Tools: Third-party or adjacent productivity and project-management tools that could potentially consume, extend, or integrate with Karet functionality through future integrations or plugins.

        Audit note: These secondary users should not automatically be interpreted as v1.3.0 users. Their inclusion establishes the broader product ecosystem and potential future use cases; the release-specific requirements determine which personas are actually in scope for validation.

# 3.0 MVP Scope
## 3.1 Release v1.3.0
*Release date: 25 September 2026*

<code>v1.3.0</code> introduces email-based collaboration and document sharing to extend Karet from an individual writing environment toward a collaborative workspace.

The release is intended to validate whether users can successfully understand and adopt the new collaboration workflow while maintaining the usability of the existing writing experience.

### 3.1.1 Release objectives
The <code>v1.3.0</code> release evaluation is intended to:

- Enable users to understand the platform and its primary workflows without external assistance.
- Improve user activation by reducing friction between account access and meaningful product interaction.
- Improve Time-to-First-Value (TTFV) by helping users reach a meaningful writing or collaboration outcome sooner.
- Validate the collaboration and permission workflows introduced in v1.3.0.
- Establish measurable product analytics for the release.
- Generate sufficient evidence to support an informed release decision.

**In-scope release capabilities**

The release should therefore be evaluated around:

- user access and onboarding;
- document creation/access;
- document sharing;
- email-based collaborator invitation;
- collaborator access;
- permission behaviour;
- collaboration workflow;
- document editing continuity;
- appropriate access boundaries;
- analytics instrumentation associated with the above workflows.

The exact functional requirements should subsequently be expressed through the acceptance criteria rather than being implied by this overview.

### 3.1.2 Actors, User Types and Permissions
Because collaboration is the key <code>v1.3.0</code> change, permissions should be treated as a first-class release requirement, not simply a UI detail.
Karet operates across two dimensions of access:

- Subscription type: determines the features and usage limits available to the user.
- Workspace/document role: determines what the user can do within a document or collaborative workspace.

#### 3.1.2.1 Subscription Types
| User Type     | Description                                      | Key Entitlements                                                                                                                 |
| ------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| **Free User** | User accessing Karet without a paid subscription | 20 AI edits, 500-character AI edit limit, attachments from writings, long context window                                         |
| **Paid User** | User subscribed to the $10/month plan            | Unlimited AI edits, unlimited attachments, longer AI edit limit, priority support, longer context window, access to new features |

#### 3.1.2.2 Workspace & Collaboration Roles
| Actor                    | Description                                                              | Core permissions                                                             |
| ------------------------ | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------- |
| **Document Owner** | User who owns the document/workspace                                     | Create, access, edit, share and manage permitted collaborators               |
| **Collaborator**         | User invited to access shared content                                    | Access and perform actions permitted by the assigned collaboration level     |
| **Invited User**         | Recipient of a collaboration invitation who has not yet completed access | Receive invitation and proceed through the access flow                       |
| **Unauthorised User**    | User without permission to access the platform or the document without an invitation                         | Must not access platform and/or protected document content                                   |
| **System**               | Platform responsible for enforcing access and workflow rules             | Validate permissions, invitations, access states, and record relevant events |

#### 3.1.2.3 Entitlement & Permission Rules
The user's ability to perform an action should be determined by the intersection of their subscription entitlement and document/workspace permission.

    User Story for free subscription plan: As a user, I may have permission to edit a document as a Collaborator, but my AI editing functionality remains subject to the Free plan's usage limits.

    User Story for paid subscription plan: As a user, I may have unlimited AI edits, but payment status does not automatically grant access to a document owned by another user.

#### 3.1.2.4 Subscription and Collaboration Access Model
Karet's access model operates across two independent dimensions: *subscription entitlements* and *document or collaboration permissions*.

Subscription status determines the features, usage limits, and service entitlements available to a user based on their plan. Document or collaboration permissions determine what the user is authorised to do within a specific writing or shared workspace.

*`v1.3.0` represents the full product capability and is not limited to paid users.* Free and Paid users may therefore participate in the product and its collaboration workflows, subject to the entitlements and permissions applicable to their account and role.

Subscription status and collaboration permission represent different access-control decisions. A user's plan does not automatically determine their permission to access another user's document, and having permission to access or edit a document does not override the usage limits or feature entitlements associated with the user's subscription.

For example, a Free User may be authorised as a collaborator on a document while remaining subject to the Free plan's AI usage limits. Similarly, a Paid User may have access to the full set of paid product entitlements but cannot access a document for which they have not been granted permission.

This separation provides the basis for validating both *plan-level entitlements* and *document-level permissions* during the <code>v1.3.0</code> release evaluation.

This distinction is important for <code>v1.3.0</code> because subscription status and collaboration permission represent different access-control decisions. The <code>v1.3.0</code> is for the full capability of the product.

## 3.2 Acceptance Criteria
For the release audit, acceptance criteria would connect the

<p align='centre'>feature → scenario → expected user behaviour → product value → urgency.</p>


| Feature                  | User Scenario                                                                     | User Case                                                                           | Value                                                              | Urgency |
| ------------------------ | --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------ | ------- |
| Document sharing         | A document owner wants another person to access their writing                     | Owner initiates document sharing through the available sharing workflow             | Enables collaboration without external file-sharing tools          | High    |
| Email invitation         | Owner wants to invite a collaborator who is not currently working in the document | Owner enters the collaborator's email and sends an invitation                       | Reduces friction in initiating collaboration                       | High    |
| Invitation access        | Invited user receives an invitation to collaborate                                | User is taken to the onboarding flow as unregistered user before accessing the document. User follows the invitation and is directed to the appropriate document/access flow | Converts an invitation into an actionable collaboration experience | High    |
| Permission enforcement   | A collaborator attempts to access a document                                      | System grants only the permissions assigned to that collaborator                    | Protects document ownership and access boundaries                  | High    |
| Collaborative editing    | An authorised collaborator needs to contribute to shared content                  | Collaborator can perform permitted document actions                                 | Enables the core collaboration use case                            | High    |
| Access restriction       | An unauthorised user attempts to open protected content                           | System prevents unauthorised access                                                 | Maintains workspace and document security                          | High    |
| Collaboration continuity | A user returns to a shared document                                               | User can continue working from the document state available to them                 | Reduces workflow interruption                                      | Medium  |
| User onboarding          | A new user encounters the product for the first time                              | User can identify how to begin without external guidance                            | Supports activation and TTFV                                       | High    |
| Analytics                | Product team needs to understand adoption of `v1.3.0`                               | Relevant workflow events are captured consistently                                  | Enables evidence-based release evaluation                          | High    |

# 4.0 Expectations for the Release Memo

The release memo serves as the final release assessment and decision-support artifact for <code>v1.3.0</code>.

It is expected to consolidate evidence gathered throughout the release lifecycle, including implementation outcomes, testing activities, analytics validation, identified risks, release readiness observations, and post-release considerations.

The release memo should provide sufficient information for stakeholders to:

1. evaluate whether the release objectives were achieved;
2. assess the completeness of the committed release scope;
3. review testing and validation outcomes;
4. understand known issues, risks, and mitigation plans;
5. assess product analytics readiness and measurement coverage;
6. determine overall release readiness; and
7. support an informed release recommendation.

The release memo should not redefine requirements or introduce new scope. Its purpose is to evaluate delivery against the expectations established within this directive and supporting product documentation.

For the final release assessment, evidence summary, and release recommendation, refer to the Release Directive: [final-directive-v1.3.0.md](../final-directive-v1.3.0.md)

# 5.0 Next Steps
- [Permission Matrix](./permission_matrix.md)
- [Acceptance Tests](./acceptance_tests.md)




