<h1 align = 'center'> Product Analytics (Template) </h1>
<a href="https://karet.vercel.app/">
<h1 align = 'center'> Karet </h1>
</a>
<h2 align = "center">AI-Powered Writing Tool</h2>
<a href="https://www.lemonconfidence.site">
<h4 align='right'> Product Owner and Engineer: Lemon Confidence </h4>
</a>



# 7.0 Product Analytics Specification (Template)

Product analytics for <code>v1.3.0</code> is intended to establish measurable evidence of how users discover, adopt, and interact with the product capabilities included in the release.

The analytics specification translates the release objectives and acceptance criteria into measurable user and system events. It should enable the release owner and product team to evaluate not only whether a feature is functioning, but whether users are successfully progressing through the intended workflows.

Analytics should support four primary areas of release evaluation:

1. **User activation and Time-to-First-Value**
2. **Collaboration adoption and workflow completion**
3. **Permission and subscription entitlement behaviour**
4. **Product reliability and workflow friction**

## 7.1 Analytics Principles

Analytics instrumentation for the release should:

* capture meaningful user actions rather than passive interface activity where possible;
* provide sufficient event properties to segment results by relevant user type and workflow;
* distinguish Free and Paid subscription experiences;
* distinguish document ownership and collaboration roles;
* support funnel and conversion analysis;
* support identification of workflow drop-off and failure points;
* provide timestamps required for time-based metrics such as TTFV;
* maintain consistency across web and product surfaces; and
* enable the defined release success criteria to be calculated from available data.

Analytics should not be considered complete solely because events exist. Events must also contain the information required to interpret the resulting data.



## 7.2 User and Account Attributes

The following attributes should be available where required for release analysis.

| Attribute          | Purpose                                                                |
| ------------------ | ---------------------------------------------------------------------- |
| User ID            | Identify unique users while maintaining consistent event attribution   |
| Subscription Plan  | Distinguish Free and Paid experiences                                  |
| Account Status     | Identify relevant account state                                        |
| Document ID        | Associate activity with a specific document                            |
| Document Owner ID  | Identify document ownership                                            |
| Collaboration Role | Distinguish Owner, Collaborator, Invited User, or other supported role |
| Invitation Status  | Analyse invitation progression                                         |
| Session ID         | Connect related actions within a session                               |
| Timestamp          | Support sequencing and time-based analysis                             |



# 7.3 Core Analytics Events

| Event                    | Trigger                                        | Key Properties                              | Primary Use                  |
| ------------------------ | ---------------------------------------------- | ------------------------------------------- | ---------------------------- |
| `account_created`        | User successfully creates an account           | User ID, plan, timestamp                    | Acquisition and activation   |
| `session_started`        | User begins a product session                  | User ID, plan, timestamp                    | Activation and TTFV baseline |
| `document_created`       | User creates a new document                    | User ID, document ID, plan                  | Product engagement           |
| `document_opened`        | User opens a document                          | User ID, document ID, role                  | Engagement and TTFV          |
| `document_edited`        | User performs a meaningful edit                | User ID, document ID, role                  | Writing engagement           |
| `ai_edit_requested`      | User initiates an AI edit                      | User ID, plan, document ID                  | AI usage                     |
| `ai_edit_completed`      | AI edit successfully completes                 | User ID, plan, character count              | AI adoption and usage        |
| `ai_edit_limit_reached`  | User reaches applicable AI limit               | User ID, plan, usage count                  | Entitlement validation       |
| `share_initiated`        | Owner opens/initiates sharing workflow         | User ID, document ID                        | Collaboration discovery      |
| `invitation_sent`        | Collaboration invitation is successfully sent  | Owner ID, document ID, recipient, timestamp | Collaboration funnel         |
| `invitation_opened`      | Recipient opens invitation                     | Recipient ID/status, document ID            | Invitation funnel            |
| `invitation_accepted`    | Recipient accepts invitation                   | User ID, document ID, timestamp             | Collaboration adoption       |
| `shared_document_opened` | Collaborator opens shared document             | User ID, document ID, role                  | Collaboration engagement     |
| `collaborative_edit`     | Collaborator performs a permitted edit         | User ID, document ID, role                  | Collaboration activity       |
| `permission_denied`      | User attempts an unauthorised action           | User ID, document ID, role, action          | Permission reliability       |
| `access_granted`         | Valid access is successfully granted           | User ID, document ID, role                  | Permission validation        |
| `access_revoked`         | Existing access is removed where supported     | User ID, document ID, role                  | Permission lifecycle         |
| `workflow_error`         | Critical workflow produces an unexpected error | User ID, workflow, error type               | Reliability and friction     |


# 7.4 Activation Measurement

Activation should measure whether a new user progresses beyond initial product access into meaningful product activity.

### Proposed measurement funnel

**Session Started → Document Opened/Created → Meaningful Edit → First Value Event**

The final **Activation Event** should be confirmed before release measurement begins.

| Metric                   | Formula / Definition                                     | Target | Actual |
| ------------------------ | -------------------------------------------------------- | -----: | -----: |
| Activation Rate          | Activated users ÷ eligible new users × 100               |      — |      — |
| Document Engagement Rate | Users opening/creating a document ÷ eligible users × 100 |      — |      — |
| Meaningful Edit Rate     | Users completing meaningful edit ÷ eligible users × 100  |      — |      — |


# 7.5 Time-to-First-Value Measurement

TTFV measures the time required for a user to reach the defined First Value Event.

**TTFV = First Value Event Timestamp − Initial Product Entry Timestamp**

The analysis should report at minimum:

* median TTFV;
* distribution of TTFV;
* percentage reaching First Value within the defined activation window; and
* TTFV segmented by relevant user type where sample size permits.

| Metric                        | Target | Actual |
| ----------------------------- | -----: | -----: |
| Median TTFV                   |      — |      — |
| TTFV within activation window |      — |      — |


# 7.6 Collaboration Funnel

The collaboration workflow should be measured as a funnel rather than as isolated events.

### Collaboration Funnel

**Share Initiated → Invitation Sent → Invitation Opened → Invitation Accepted → Shared Document Opened → Collaborator Action**

| Funnel Stage        | Event                    | Users | Conversion Rate | Drop-off |
| ------------------- | ------------------------ | ----: | --------------: | -------: |
| Share initiated     | `share_initiated`        |     — |               — |        — |
| Invitation sent     | `invitation_sent`        |     — |               — |        — |
| Invitation opened   | `invitation_opened`      |     — |               — |        — |
| Invitation accepted | `invitation_accepted`    |     — |               — |        — |
| Document opened     | `shared_document_opened` |     — |               — |        — |
| Collaborator action | `collaborative_edit`     |     — |               — |        — |

This allows the release owner to identify whether friction occurs during **feature discovery, invitation delivery, invitation acceptance, document access, or actual collaboration**.

---

# 7.7 Subscription Analytics

Because Karet supports both Free and Paid experiences, product analytics should allow relevant behaviour to be segmented by subscription plan.

The release should be capable of answering:

* How do Free and Paid users engage with AI editing?
* How frequently are Free users reaching their usage limits?
* Are Paid users accessing their additional entitlements?
* Do Free and Paid users participate in collaboration differently?
* Are subscription restrictions being triggered as expected?
* Are entitlement-related failures occurring?

| Metric                   | Free | Paid | Overall |
| ------------------------ | ---: | ---: | ------: |
| AI edits per active user |    — |    — |       — |
| Users reaching AI limit  |    — |    — |       — |
| Document activity        |    — |    — |       — |
| Sharing initiation       |    — |    — |       — |
| Invitation acceptance    |    — |    — |       — |
| Collaboration activity   |    — |    — |       — |

---

# 7.8 Permission Analytics

Permission-related events should provide evidence that access controls operate as intended.

The analytics should distinguish between:

* successful authorised access;
* rejected unauthorised access;
* permitted collaborator actions;
* restricted owner-only actions;
* invitation states;
* access changes or revocation; and
* errors resulting from permission validation.

| Metric                        | Definition                                    | Expected Outcome | Actual |
| ----------------------------- | --------------------------------------------- | ---------------- | ------ |
| Authorised Access Success     | Valid access attempts successfully granted    | —                | —      |
| Unauthorised Access Rejection | Invalid access attempts correctly rejected    | 100%             | —      |
| Restricted Action Rejection   | Restricted actions correctly prevented        | 100%             | —      |
| Invitation Acceptance         | Valid invitations successfully accepted       | —                | —      |
| Access Revocation             | Revoked users prevented from continued access | 100%             | —      |

---

# 7.9 Analytics Quality and Completeness

Before analytics are used as evidence for the release assessment, instrumentation should be validated for:

| Validation Area       | Requirement                                            | Status |
| --------------------- | ------------------------------------------------------ | ------ |
| Event Presence        | Required events fire when expected                     | —      |
| Event Accuracy        | Events represent the intended user action              | —      |
| Property Completeness | Required properties are populated                      | —      |
| Timestamp Integrity   | Events contain usable timestamps                       | —      |
| User Attribution      | Events can be associated with the correct user/session | —      |
| Plan Attribution      | Free/Paid status is correctly represented              | —      |
| Role Attribution      | Collaboration role is correctly represented            | —      |
| Duplicate Events      | Events are not unintentionally duplicated              | —      |
| Failed Events         | Relevant failures are observable                       | —      |
| Funnel Continuity     | Events can be sequenced into the intended workflow     | —      |

---

# 7.10 Analytics Evidence for Release Assessment

The release owner should retain evidence demonstrating that the analytics specification has been implemented and validated.

Expected evidence may include:

* analytics event definitions;
* event payload samples;
* analytics dashboard or reporting views;
* tracking validation results;
* funnel analysis;
* activation analysis;
* TTFV calculation;
* subscription-level analysis;
* collaboration adoption analysis;
* permission-event validation; and
* documented analytics gaps or limitations.

Analytics findings should subsequently feed into the **Success Criteria**, **Known Limitations and Outstanding Risks**, and **Release Conclusion** sections of this directive.
