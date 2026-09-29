<h1 align = 'center'> Permission Matrix </h1>
<a href="https://karet.vercel.app/">
<h1 align = 'center'> Karet </h1>
</a>
<h2 align = "center">AI-Powered Writing Tool</h2>
<a href="https://www.lemonconfidence.site">
<h4 align='right'> Product Owner and Engineer: Lemon Confidence </h4>
</a>

# Table of Content
>- 1.0 [Plan Entitlement Matrix](#10-plan-entitlement-matrix)
>- 2.0 [Collaboration Permission Matrix](#20-collaboration-permission-matrix)
>   - 2.1 [Collaboration Workflow Matrix](#21-collaboration-workflow-matrix)
>- 3.0 [Permission Boundaries Matrix](#30-permission-boundary-matrix)
>- 4.0 [Plan vs Role Validation Matrix](#40-plan-vs-role-validation-matrix)
>- 5.0 [Analytics Event Ownership Matrix](#50-analytics-event-ownership-matrix)
>- 6.0 [Memo](#60-memo)



# 1.0 Plan Entitlement Matrix

| Capability / Entitlement        | Free           | Paid         |
| ------------------------------- | -------------- | ------------ |
| Account registration and access | ✓              | ✓            |
| Core writing experience         | ✓              | ✓            |
| Document creation               | ✓              | ✓            |
| Document editing                | ✓              | ✓            |
| Document organization           | ✓              | ✓            |
| AI-assisted editing             | 20 AI edits    | Unlimited    |
| AI edit character limit         | 500 characters | Longer limit |
| Attachments from writings       | ✓              | ✓            |
| Attachment usage                | Limited        | Unlimited    |
| Context window                  | Long           | Longer       |
| Theme customization             | ✓              | ✓            |
| Collaboration participation     | ✓              | ✓            |
| Document sharing                | ✓              | ✓            |
| Invitation acceptance           | ✓              | ✓            |
| Access to new features          | —              | ✓            |
| Priority support                | —              | ✓            |
| Subscription fee                | $0             | $10/month    |


# 2.0 Collaboration Permission Matrix

This matrix defines document-level permissions irrespective of subscription status.

| Action                             | Owner | Collaborator | Invited User       | Unauthorised User | System |
| ---------------------------------- | ----- | ------------ | ------------------ | ----------------- | ------ |
| Create document                    | ✓     | —            | —                  | —                 | —      |
| View owned document                | ✓     | —            | —                  | —                 | —      |
| View shared document               | ✓     | ✓            | Pending Acceptance | —                 | —      |
| Edit document                      | ✓     | ✓           | —                  | —                 | —      |
| Share document                     | ✓     | —            | —                  | —                 | —      |
| Invite collaborator                | ✓     | —            | —                  | —                 | —      |
| Remove collaborator                | ✓     | —            | —                  | —                 | —      |
| Manage permissions                 | ✓     | —            | —                  | —                 | —      |
| Accept invitation                  | —     | —            | ✓                  | —                 | —      |
| Access document without permission | —     | —            | —                  | ✗                 | —      |
| Enforce access rules               | —     | —            | —                  | —                 | ✓      |
| Record collaboration events        | —     | —            | —                  | —                 | ✓      |



## 2.1 Collaboration Workflow Matrix

| Workflow Stage      | Owner                 | Collaborator                | Invited User        | System              |
| ------------------- | --------------------- | --------------------------- | ------------------- | ------------------- |
| Create document     | Initiates             | —                           | —                   | Persists document   |
| Share document      | Initiates             | —                           | —                   | Sends invitation    |
| Invitation sent     | Receives confirmation | —                           | Receives invitation | Records event       |
| Invitation accepted | —                     | Becomes active collaborator | Accepts invitation  | Grants access       |
| Document opened     | Views document        | Views document              | —                   | Validates access    |
| Document edited     | Edits content         | Edits content              | —                   | Saves changes       |
| Access revoked      | Removes collaborator  | Loses access                | —                   | Enforces revocation |


## 3.0 Permission Boundary Matrix

This matrix is useful for audit evidence because it focuses on what must **not** happen.

| Scenario                                       | Expected Result   |
| ---------------------------------------------- | ----------------- |
| Unauthorised user accesses document URL        | Access denied     |
| Collaborator attempts owner-only action        | Action denied     |
| Invitation link is invalid                     | Access denied     |
| Invitation link is expired                     | Access denied     |
| Removed collaborator accesses document         | Access denied     |
| Free user exceeds AI edit quota                | Action restricted |
| Free user exceeds character limit              | Action restricted |
| Paid user accesses premium capability          | Access granted    |
| User accesses another user's private document  | Access denied     |
| User attempts collaboration without invitation | Access denied     |


# 4.0 Plan vs Role Validation Matrix

This is usually the most valuable matrix for release testing because it identifies all combinations requiring validation.

| Plan | Role              | Primary Validation Focus                               |
| ---- | ----------------- | ------------------------------------------------------ |
| Free | Owner             | Document creation, editing, sharing, Free-plan limits  |
| Free | Collaborator      | Shared document access, editing, Free-plan limits      |
| Paid | Owner             | Full feature access, sharing, collaboration management |
| Paid | Collaborator      | Shared document access, editing, premium entitlements  |
| Free | Invited User      | Invitation acceptance flow                             |
| Paid | Invited User      | Invitation acceptance flow                             |
| Free | Unauthorised User | Access restriction                                     |
| Paid | Unauthorised User | Access restriction                                     |


# 5.0 Analytics Event Ownership Matrix

Since one of the release objectives is establishing measurable analytics, the PRD should identify which actor generates key events.

| Event                  | Actor                |
| ---------------------- | -------------------- |
| User registration      | User                 |
| Document created       | Owner                |
| Document edited        | Owner / Collaborator |
| Document shared        | Owner                |
| Invitation sent        | Owner                |
| Invitation received    | Invited User         |
| Invitation accepted    | Invited User         |
| Shared document viewed | Collaborator         |
| Access denied          | Unauthorised User    |
| AI edit used           | Free / Paid User     |
| Subscription upgraded  | User                 |



# 6.0 Memo
These five matrices together usually provide enough coverage for a release audit to validate **entitlements, permissions, workflows, security boundaries, and analytics instrumentation** without needing to infer behaviour from scattered requirements.
