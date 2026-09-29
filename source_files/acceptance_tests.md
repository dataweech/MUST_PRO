<h1 align = 'center'>  Product Release & Acceptance Verification </h1>
<a href="https://karet.vercel.app/">
<h1 align = 'center'> Karet </h1>
</a>
<h2 align = "center">AI-Powered Writing Tool</h2>
<a href="https://www.lemonconfidence.site">
<h4 align='right'> Product Owner and Engineer: Lemon Confidence </h4>
</a>

## Table of Contents
>1. [Executive Summary & Background](#1-executive-summary--background)
>2. [Release Acceptance Matrix](#2-release-acceptance-matrix)
>3. [Product Evaluation & Functional Audit](#3-product-evaluation--functional-audit)
>4. [Release Decision & Sign Off](#4-release-decision--sign-off)


<h2 align='right'>
Release Version: <b>v1.3.0</b>  |  Release Date: September 25, 2026 </h2>



## 1. Executive Summary & Background
This document serves as the formal release directive and quality gate assessment for **Karet v1.3.0**.

Karet is an AI-native writing and decision-support workspace built for technical documentation, research synthesis, storytelling, and knowledge management. Release `v1.3.0` marks the platform’s transition from a single-player document editor into a multi-user collaborative workspace by introducing email-based collaborator invitations and permission boundaries.

### Core Release Objectives
* **Collaborative Foundations:** Enable document sharing via direct email invitations with enforced read/edit permissions.
* **Frictionless Activation:** Maintain single-click onboarding via Google OAuth and shorten Time-to-First-Value (TTFV).
* **Entitlement Guardrails:** Implement clear usage metering and tier enforcement across Free and Paid plans.
* **Observability:** Establish core telemetry and product analytics instrumentation to evaluate user activation and workflow adoption.


## 2. Release Acceptance Matrix
| Test ID | Feature / Scope | Test Scenario & Verification Criteria | Expected Outcome | Evidence / Observed Notes | Status |
| --- | --- | --- | --- | --- | --- |
| **TC-01** | **Email Invitation** | Document owner triggers share modal and inputs collaborator email. | System dispatches transactional email containing document invite link. | Recipient email is recorded in modal, but no dispatch trigger/email is received. | FAIL |
| **TC-02** | **Document Sharing** | Collaborator attempts access via direct invitation link. | User joins document workspace with appropriate workspace visibility. | Blocked by TC-01; cannot test invitation acceptance flow end-to-end. | BLOCKED |
| **TC-03** | **Permission Enforcement** | Document owner modifies collaborator roles (Viewer vs Editor). | Permissions update immediately; unauthorized write actions are rejected. | Owner UI updates successfully, but role changes fail to reflect on the collaborator side. | FAIL |
| **TC-04** | **Unauthorized Access** | Unauthenticated or uninvited user visits document URL directly. | System redirects to authentication or displays an explicit 403 Forbidden state. | Direct unauthorized routing prevented; fallback redirects properly. | PASS |
| **TC-05** | **AI Writing Assistant** | User triggers inline prompt command or selection-based AI rewrite. | LLM processes selection and streams completion without editor hang. | Basic rich-text writing works; AI requests degrade, fail to complete, or hang. | FAIL |
| **TC-06** | **Usage & Entitlements** | Free-tier user exhausts daily/monthly AI generation allocation. | System gates execution, preserves text, and displays upgrade prompt. | Free-tier limit enforcement is bypassed; token counters fail to increment/persist. | FAIL |
| **TC-07** | **Authentication & Onboarding** | New or returning user signs in via supported provider. | User completes single-step Google OAuth and enters dashboard immediately. | Google OAuth operates seamlessly; redirects directly to active workspace. | PASS |
| **TC-08** | **In-Editor Discoverability** | First-time user opens empty canvas to write. | Editor surfaces command discovery cues (e.g., slash-commands `/`, shortcuts). | Canvas lacks empty-state affordances or command hints during active writing. | PARTIAL |
| **TC-09** | **Analytics Instrumentation** | User completes signup, doc creation, share, and AI completion. | Telemetry captures event payloads in analytics pipeline. | Event tracking not wired; pipeline is non-operational. | FAIL |

## 3. Product Evaluation & Functional Audit

### 3.1 Collaboration Workflow & Security
* **Invitation Delivery Failure:** While the UI captures invite inputs without error, the underlying SMTP/messaging dispatch fails silently. Collaborators never receive invitation emails.
* **Permission Desynchronization:** Role mutations executed by the document owner do not propagate to active sessions, exposing the document to state drift and inconsistent access rights.

### 3.2 Core Intelligence & Entitlements
* **AI Generation Stability:** AI request lifecycles fail intermittently during active writing, undermining Karet's core proposition as an AI-powered editor.
* **Entitlement Leakage:** The usage tracking service does not decrement or cap free tier consumption, posing an unmonitored infrastructure cost risk.

### 3.3 UX & Telemetry Gaps
* **Discoverability:** The editor has contextual prompts (such as `/` slash commands or contextual shortcut tooltips), but no way out of the format enabled for non-technical users.
* **Observability Deficit:** Zero telemetry prevents the team from calculating Time-to-First-Value (TTFV), drop-off rates, or feature engagement post-launch.


## 4. Release Decision & Sign-off
| Evaluation Pillar | Assessment | Technical & Functional Findings |
| --- | --- | --- |
| **Functional Editor & AI** | **Partial** | Rich-text baseline is stable; AI prompt executions fail intermittently. |
| **Collaboration Engine** | **Fail** | Outbound invite emails fail; collaborator lifecycle cannot complete. |
| **Access Control & RBAC** | **Fail** | Access control state changes do not synchronize to target collaborator accounts. |
| **Subscription Entitlements** | **Fail** | Tier restrictions and AI generation metering fail to execute. |
| **Auth & Workspace UX** | **Pass** | Google OAuth authentication and direct dashboard entry operate reliably. |
| **Telemetry & Analytics** | **Fail** | Tracking instrumentation is unmapped and inactive across all key funnels. |
| **Identified Critical Risks** | **High** | Cost exposure from unbounded AI usage; high bounce risk from discovery friction. |
| **Overall Release Verdict** | **NO-GO** | **Blocked.** Release does not satisfy critical acceptance criteria for general availability. |

## 5. Required Remediations for Engineering Team (v1.3.1)
1. **Fix Email Dispatch Pipeline:** Audit webhook/transactional email provider integrations (e.g., Resend, SendGrid) to verify invite tokens trigger and route correctly.
2. **Synchronize Document Permissions:** Ensure role updates in the metadata store immediately revalidate and sync with collaborator session states.
3. **Stabilize AI Endpoint & Enforce Quotas:** Stabilize streaming completion handlers and patch middleware to decrement plan limits before completing generation calls.
4. **Deploy Core Telemetry:** Instrument minimal viable tracking for `user_signed_up`, `doc_created`, `invite_sent`, `ai_invoked`, and `quota_hit`.

