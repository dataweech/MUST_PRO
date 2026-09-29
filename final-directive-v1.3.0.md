<h1 align = 'center'> FormaL Release Directive </h1>
<a href="https://karet.vercel.app/">
<h1 align = 'center'> Karet </h1>
</a>
<h2 align = "center">AI-Powered Writing Tool</h2>
<a href="https://www.lemonconfidence.site">
<h4 align='right'> Product Owner and Engineer: Lemon Confidence </h4>
</a>


## Table of Contents
>1. [Executive Summary & Background](#1-executive-summary--background)
>2. [Release Acceptance Test Matrix](#2-release-acceptance-test-matrix)
>3. [Functional Audit & Risk Evaluation](#3-functional-audit--risk-evaluation)
>4. [Release Decision & Governance Sign-Off](#4-release-decision--governance-sign-off)
>5. [Release Candidate Remediation Plan (v1.3.1)](#5-release-candidate-remediation-plan-v131)
>6. [Product Analytics & Telemetry Specification](#6-product-analytics--telemetry-specification)
>     - 6.1 [Telemetry Core Principles](#61-telemetry-core-principles)
>     - 6.2 [Global Identity & Common Dimensions](#62-global-identity--common-dimensions)
>     - 6.3 [Core Event Dictionary](#63-core-event-dictionary)
>     - 6.4 [Funnel Architecture & Success Formulas](#64-funnel-architecture--success-formulas)
>     - 6.5 [Entitlement & RBAC Security Verification](#65-entitlement--rbac-security-verification)
>     - 6.6 [Data Quality Gates & Verification Checklist](#66-data-quality-gates--verification-checklist)
<h2 align='right'>
Release Version: <b>v1.3.0</b>  |  Release Date: September 25, 2026 </h2>

## 1. Executive Summary & Background

This document serves as the formal release directive, verification reference, and telemetry guide for **Karet v1.3.0**.

Karet is an AI-native writing and decision-support workspace designed for technical writing, research synthesis, storytelling, and knowledge-intensive workflows. Release `v1.3.0` transitions the platform from a single-player document editor into a multi-user workspace by introducing collaborative document sharing, role-based access controls (RBAC), and team-oriented editing foundations.

### 1.1 Core Release Objectives
* **Collaborative Foundations:** Enable document owners to invite external collaborators via transactional email with distinct permission levels (Viewer vs. Editor).
* **Frictionless Activation:** Shorten Time-to-First-Value (TTFV) through single-click Google OAuth authentication and immediate canvas readiness.
* **Subscription & Entitlement Guardrails:** Implement quota metering between Free and Paid tiers to prevent infrastructure cost overruns.
* **Telemetry Instrumentation:** Establish baseline analytics tracking to diagnose user friction, drop-offs, and feature adoption.


## 2. Release Acceptance Test Matrix

*Test verification performed across staging and production preview environments.*

| Test ID | Capability / Scope | Test Scenario & Verification Method | Expected Operational State | Observed Behavior & Findings | Status |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **TC-01** | **Email Invitation** | Document owner enters recipient email in sharing modal and submits. | System dispatches transactional email containing unique access token. | Recipient email displays in modal list, but email dispatch fails silently. No email is sent. | <span style="color:red; font-weight:bold;">FAIL</span> |
| **TC-02** | **Invitation Claim** | Recipient clicks tokenized invite link received via email. | Recipient joins workspace with access boundaries reflected accurately. | Blocked by TC-01; full acceptance flow cannot complete end-to-end. | <span style="color:orange; font-weight:bold;">BLOCKED</span> |
| **TC-03** | **Access Boundaries** | Document owner modifies collaborator privileges (Viewer vs. Editor). | Permissions update dynamically; unauthorized actions are rejected. | Owner UI updates successfully, but role changes fail to propagate to active collaborator sessions. | <span style="color:red; font-weight:bold;">FAIL</span> |
| **TC-04** | **Unauthorized Routing** | Unauthenticated user visits protected document URL directly. | System denies access, displaying explicit 403 state or sign-in gate. | Direct unauthenticated routing blocked; fallback redirects safely to login. | <span style="color:green; font-weight:bold;">PASS</span> |
| **TC-05** | **AI Writing Flow** | User submits inline prompt or triggers generative text expansion. | Model processes input and streams completions directly into editor. | Standard rich text editing works; AI generation frequently hangs or fails to stream. | <span style="color:red; font-weight:bold;">FAIL</span> |
| **TC-06** | **Usage Metering** | Free-tier user exhausts daily generation allowance. | System blocks further calls, preserves content, and displays upgrade prompt. | Metering fails to increment; free tier users can trigger unbounded calls. | <span style="color:red; font-weight:bold;">FAIL</span> |
| **TC-07** | **Authentication** | User attempts registration or authentication via Google OAuth. | Auth succeeds immediately and routes to active workspace dashboard. | Google OAuth integration operates with zero friction. | <span style="color:green; font-weight:bold;">PASS</span> |
| **TC-08** | **Canvas Usability** | First-time user opens empty editor canvas to begin writing. | Editor surfaces discovery affordances (e.g., slash-commands `/`). | Canvas provides no discovery hints or shortcut helpers during active writing. | <span style="color:orange; font-weight:bold;">PARTIAL</span> |
| **TC-09** | **Instrumentation** | User executes core actions (doc creation, editing, sharing). | Client dispatches formatted analytics payloads to tracking pipeline. | Tracking pipelines are unmapped and events do not fire. | <span style="color:red; font-weight:bold;">FAIL</span> |


## 3. Functional Audit & Risk Evaluation

### 3.1 Collaboration & Access Control
* **Email Delivery Pipeline:** The UI successfully validates email input, but the dispatch service (transactional mail provider/worker) fails silently. This prevents external collaboration loops from closing.
* **Role Desynchronization:** Role mutations made by the owner are saved locally but do not broadcast to active collaborator sessions, creating severe data integrity and document security risks.

### 3.2 AI Assistant & Quota Enforcement
* **Streaming Reliability:** AI request lifecycles fail intermittently during active writing, which undermines Karet’s primary positioning as an AI-powered editor.
* **Entitlement Leakage:** The usage tracking service does not decrement or cap free tier consumption, exposing the platform to unmonitored LLM token costs.

### 3.3 Discoverability & Telemetry Gaps
* **Interaction Friction:** The absence of empty-state discoverability (e.g., `"Type '/' for commands..."`) increases user cognitive load, directly risking first-session drop-off.
* **Zero Observability:** Without functional telemetry, measuring activation funnels, TTFV, and retention remains impossible.


## 4. Release Decision & Governance Sign-Off

| Evaluation Pillar | Assessment | Executive Finding |
| :--- | :---: | :--- |
| **Core Rich Text & Editor** | **Pass** | Canvas handles baseline text operations reliably. |
| **AI Processing Reliability** | **Fail** | High generation failure rate on streaming completions. |
| **Collaboration Engine** | **Fail** | Outbound transactional invite emails fail silently. |
| **Access Control & RBAC** | **Fail** | Permission state mutations do not propagate across client sessions. |
| **Subscription Entitlements**| **Fail** | Quota gates and token metering fail to execute. |
| **Identity & Authentication**| **Pass** | Google OAuth functions smoothly across all entry funnels. |
| **Telemetry & Observability**| **Fail** | Analytics pipelines are completely unmapped and inactive. |
| **Identified Risk Profile** | **CRITICAL** | Cost exposure from unbounded AI usage; high user bounce rate. |
| **Release Gate Decision** | **NO-GO** | **BLOCKED.** `v1.3.0` does not satisfy minimum release criteria. |


## 5. Release Candidate Remediation Plan (v1.3.1)

Before promoting build `v1.3.1` to general availability, engineering must complete and verify the following remediations:

1. **Transactional Email Pipeline:** Audit and wire the outbound transactional email worker (e.g., Resend, SendGrid) to verify invite tokens dispatch reliably.
2. **Session Role Synchronization:** Implement dynamic permission revalidation or WebSocket updates to ensure collaborator role modifications apply immediately.
3. **AI Generation Middleware:** Resolve upstream streaming timeouts and add pre-execution middleware checks that strictly enforce user quota limits before sending requests to the LLM.
4. **Editor Discoverability:** Insert empty-state placeholder hints (`"Type '/' for commands..."`) to guide new users through key features.
5. **Telemetry Deployment:** Implement the telemetry events detailed in Section 6.


## 6. Product Analytics & Telemetry Specification

### 6.1 Telemetry Core Principles
* **Capture Intentionality:** Track explicit user actions (e.g., initiating an AI edit, updating permissions) rather than noisy, passive UI clicks.
* **Uniform Identity Envelope:** Ensure every event contains the standard properties: `user_id`, `session_id`, and `plan_tier`.
* **Measure Both Success and Failure:** Log operational failures (`permission_denied`, `workflow_error`) with the same rigor as successful user actions.


### 6.2 Global Identity & Common Dimensions

The analytics provider must inject these global dimensions into every telemetry payload:

| Property | Format | Sample Value | Definition |
| :--- | :--- | :--- | :--- |
| `user_id` | UUID | `usr_91b7e41a` | Unique identifier of the authenticated user. |
| `session_id` | UUID | `sess_88a31e02` | Tracks actions across a single contiguous user session. |
| `subscription_tier`| Enum | `free` \| `paid` | The active subscription plan at execution time. |
| `document_id` | UUID | `doc_3310fa89` | Target document identifier (null if workspace-level). |
| `user_role` | Enum | `owner` \| `editor` \| `viewer` | Active permissions of the user for the target document. |
| `timestamp_utc` | ISO-8601 | `2026-09-25T12:00:00.000Z` | Standard UTC timestamp for sequence and TTFV calculations. |


### 6.3 Core Event Dictionary

| Domain | Event Name | Trigger Condition | Critical Properties |
| :--- | :--- | :--- | :--- |
| **Auth** | `account_created` | User completes signup. | `{ provider: "google", referral_source: string }` |
| **Auth** | `session_started` | User initializes workspace session. | `{ entry_url: string, is_returning: boolean }` |
| **Editor** | `document_created` | User opens a new document. | `{ document_type: "blank" \| "template" }` |
| **Editor** | `document_opened` | Canvas finishes loading a document. | `{ access_method: "direct" \| "shared_link" }` |
| **Editor** | `meaningful_edit_saved` | User adds or updates $\ge 50$ characters. | `{ delta_chars: number, save_type: "auto" \| "manual" }` |
| **AI Assist** | `ai_edit_requested` | User submits an AI prompt or inline command. | `{ trigger_type: "inline" \| "toolbar", prompt_length: number }` |
| **AI Assist** | `ai_edit_completed` | Model completion renders in editor. | `{ latency_ms: number, generated_tokens: number }` |
| **Entitlement**| `ai_limit_reached` | User hits free or paid tier usage limit. | `{ current_tier: "free", quota_limit: number }` |
| **Collab** | `share_modal_opened` | User opens the sharing interface. | `{ collaborator_count: number }` |
| **Collab** | `invitation_dispatched`| Invite email successfully sends. | `{ recipient_email_hash: string, assigned_role: enum }` |
| **Collab** | `invitation_accepted` | Recipient claims invite access. | `{ time_to_accept_sec: number }` |
| **Collab** | `collaborative_edit` | Non-owner edits a shared document. | `{ editor_role: "editor" }` |
| **Security** | `permission_denied` | System rejects an unauthorized action. | `{ target_action: string, attempted_role: enum }` |
| **System** | `workflow_error` | Critical workflow fails unexpectedly. | `{ error_code: string, component: string }` |


### 6.4 Funnel Architecture & Success Formulas

#### Activation & Time-to-First-Value (TTFV)
* **Funnel Sequence:**  
  `session_started` $\rightarrow$ `document_created` $\rightarrow$ `meaningful_edit_saved` $\rightarrow$ `ai_edit_completed`
* **Activation Definition:** A user who creates a document, inputs $\ge 50$ characters, and successfully completes at least one AI generation in their first session.
* **TTFV Formula:**  
  $$\text{TTFV} = \text{Timestamp}_{\text{ai\_edit\_completed}} - \text{Timestamp}_{\text{session\_started}}$$

$$\text{Activation Rate} = \left( \frac{\text{Activated Users}}{\text{Total New Signups}} \right) \times 100 \quad [\text{Target: } \ge 45\%]$$

$$\text{Document Engagement Rate} = \left( \frac{\text{Users with } \ge 1 \text{ Document}}{\text{Total Active Sessions}} \right) \times 100 \quad [\text{Target: } \ge 70\%]$$

$$\text{Median TTFV Target} \le 120\text{ seconds}$$



#### Multi-Player Collaboration Funnel
**Invite Delivery Rate**

`(invitation_dispatched / share_modal_opened) × 100`

Target: **≥ 80%**

**Viral Acceptance Rate**

`(invitation_accepted / invitation_dispatched) × 100`

Target: **≥ 50%**

**Collaboration Edit Rate**

`(collaborative_edit / invitation_accepted) × 100`

Target: **≥ 40%**

### 6.5 Entitlement & RBAC Security Verification

| Audit Area | Analytical Metric | Acceptance Threshold |
| :--- | :--- | :---: |
| **AI Quota Gating** | Number of `ai_edit_completed` events firing after an `ai_limit_reached` event. | **0 (Zero tolerance)** |
| **RBAC Security** | Percentage of unauthorized actions that trigger `permission_denied`. | **100% Rejection** |
| **AI Success Reliability**| Ratio of `ai_edit_completed` to `ai_edit_requested`. | $\ge 98.0\%$ |


### 6.6 Data Quality Gates & Verification Checklist

Before closing the analytics verification phase for the upcoming release candidate, the engineering team must confirm the following:

- [ ] **Payload Integrity:** Every emitted event adheres to its schema and includes all required fields.
- [ ] **Attribute Uniformity:** `user_id`, `session_id`, and `plan_tier` are present across all client and server events.
- [ ] **Deduplication:** Rapid button clicks trigger debounce logic and do not emit duplicate tracking records.
- [ ] **Zero-Latency Ingestion:** Test events arrive in the analytics processing stream within 60 seconds of invocation.
