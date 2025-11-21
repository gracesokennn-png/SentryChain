
# SentryChain — Decentralized Web Threat Intelligence & Sentinel System (DW-TISS)**

## **Overview**

This project implements a **decentralized security and threat-monitoring framework** built on the Stacks blockchain using the Clarity smart-contract language.
It facilitates:

* **Registration of secure websites** with on-chain collateral
* **Sentinel-driven threat reporting**
* **Validation and confirmation of malicious website alerts**
* **Reputation-based monitoring of reporting entities (Sentinels)**
* **Configurable protection levels and system governance**

The contract acts as a **trustless registry and adjudication layer** for web threat intelligence, enabling community-driven security assessments backed by STX collateral and a provable reputation system.

---

## **Core Components**

### **1. Website Registration**

Websites can be onboarded through `register_secure_site`.
On registration:

* Input validation ensures sanitized identifiers.
* Collateral is locked based on the current **protection_intensity**.
* A new entry is created in `registered_sites`.

### **2. Threat Reporting**

Sentinels can submit alerts using `submit_threat_alert`, which:

* Logs an incident in `malicious_site_registry`.
* Increases sentinel credibility after each valid submission.
* Enforces inactivity windows and minimum credibility levels.

### **3. Threat Validation**

The function `validate_threat_report` allows Sentinel operators to confirm or reject submitted threats.
Depending on the decision:

* Site threat weight is adjusted via `modify_site_risk`.
* Sentinel performance metrics are updated.

### **4. Sentinel Registry**

Sentinels join via `enlist_sentinel` by staking collateral.
Tracked attributes include:

* `reserved_amount`
* `assessment_count`
* `precision_metric`
* `recent_activity_epoch`
* Operational mode

### **5. Governance & System Control**

The system uses role-based access:

* `system_controller` holds admin authority.
* Admin can modify protection levels, pause the system, or transfer authority.

Key functions:

* `modify_protection_level`
* `toggle_system_state`
* `reassign_system_control`
* `initialize_system`

---

## **Error Handling**

The contract defines explicit error codes such as:

* `ACCESS_FORBIDDEN`
* `DUPLICATE_ENTRY_ERROR`
* `INVALID_WEB_IDENTIFIER`
* `COLLATERAL_MISSING_ERROR`
* …and more.

These codes ensure predictable, explicit failure modes for app builders.

---

## **Data Structures**

Major Clarity maps include:

* `registered_sites`: Stores verified website details.
* `malicious_site_registry`: Holds pending or confirmed threat reports.
* `sentinel_registry`: Sentinel staking and performance data.
* `sentinel_performance_log`: Sentinel activity tracked per target site.
* `site_inspection_records`: (Optional extension) for auditing & compliance.

---

## **Security Considerations**

* Strict string-based sanitization prevents malicious input.
* Collateral requirements discourage low-quality reporting.
* Inactivity windows prevent spam or rapid-fire submissions.
* Governance functions restricted to the controller.

---

