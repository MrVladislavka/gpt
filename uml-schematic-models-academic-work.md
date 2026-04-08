# UML SCHEMATIC MODELS

## 1. Define UML (Ref)
Unified Modeling Language (UML) is a standardized visual modeling language used to specify, visualize, construct, and document software-intensive systems. UML provides a common notation for stakeholders (analysts, developers, testers, and business users) to communicate system structure and behavior. In this project, UML is used to model online-banking requirements and design through use-case, class, ERD, activity, sequence, and collaboration views.

> **Reference definition source:** Booch, Rumbaugh, and Jacobson describe UML as a language for visualizing, specifying, constructing, and documenting artifacts of software systems.

---

## 2. Define each UML schematic model

### 2.1 Use Case Diagram (UCD)
A Use Case Diagram represents functional requirements from the user perspective. It identifies actors, use cases, system boundary, and relationships such as `<<include>>`, `<<extend>>`, and generalization.

### 2.2 Class Diagram
A Class Diagram models static structure: classes, attributes, operations, inheritance, associations, multiplicities, aggregation/composition.

### 2.3 Entity Relationship Diagram (ERD)
An ERD models data entities, primary/foreign keys, and relationships. It complements the class diagram by emphasizing data persistence and integrity.

### 2.4 Activity Diagram
An Activity Diagram models workflow behavior: start/end nodes, actions, control flows, decisions, merges, forks/joins, and swimlanes.

### 2.5 Sequence Diagram
A Sequence Diagram models time-ordered interactions between object instances (lifelines), showing messages and control fragments (`alt`, `loop`, `par`).

### 2.6 Collaboration (Communication) Diagram
A Collaboration Diagram emphasizes object links and message flow topology. It complements sequence diagrams by highlighting **who communicates with whom**.

---

## 3. Use Case Diagram and 4–6 Use Case Descriptors

### 3.1 Use Case Diagram
(add use case diagram here — `online-banking-usecase` exemplar)

### 3.2 Construction quality checklist (rubric alignment)
- **Actors and Use Cases:** Customer, Bank Administrator, Underwriter, Notification Service, Fraud Monitoring System, Payment Network.
- **Generalizations:** Example: `Registered Customer` generalized to `Account Holder`.
- **System Boundary:** “Online Banking System” boundary enclosing all internal use cases.
- **Correct notation:** Actor stick figures, ovals for use cases, association lines.
- **`<<include>>` / `<<extend>>`:**
  - `Transfer Funds` `<<include>>` `Authenticate User`.
  - `High-Value Transfer` `<<extend>>` `Fraud Review`.
- **Conceptual understanding:** Relationship semantics match business behavior and exceptions.

### 3.3 Selected Use Cases (descriptive paragraphs)

#### UC-01: Login with 2FA
The customer authenticates with username/password and completes a second-factor challenge. The system validates credentials, sends OTP/push, verifies challenge response, and establishes an authenticated session with risk checks.

#### UC-02: External Transfer
The customer submits an external transfer request. The system validates account balance and beneficiary details, performs compliance checks, submits to gateway/network, and returns settlement status.

#### UC-03: New Payee Setup
The customer enters payee details. The system validates format and ownership through directory/validation services, performs risk checks, and activates the payee if all controls pass.

#### UC-04: Loan Application
The applicant submits loan information and documents. The system validates completeness, obtains credit data, runs rules/underwriting checks, and produces approval/decline outcomes.

#### UC-05: Fraud Response for High-Value Transfer
Fraud engine flags a transfer. Case management and operations investigate, verify with customer, and either release transaction or block/freeze depending on final disposition.

#### UC-06: Admin Freeze Account
A bank administrator requests account freeze for fraud or compliance reasons. System validates authority, applies restrictions, notifies stakeholders, and records immutable audit logs.

---

## 4. Use Case Descriptor Tables (2-column Actor/System Response)

### 4.1 Descriptor for UC-01 Login with 2FA
| Actor Task | System Response |
|---|---|
| Enters username/password | Validates against USER/CUSTOMER credentials |
| Requests login | Creates AUTH_SESSION and risk context |
| Chooses OTP channel | Sends OTP via Notification Service |
| Submits OTP | Verifies OTP_CHALLENGE hash/expiry |
| Waits for result | Approves session or increments failure counter |
| Opens dashboard | Returns ACCOUNT summary and entitlement profile |

### 4.2 Descriptor for UC-02 External Transfer
| Actor Task | System Response |
|---|---|
| Selects source account and beneficiary | Validates ACCOUNT status and beneficiary details |
| Enters transfer amount | Checks limits, fees, and available balance |
| Confirms transfer | Performs compliance/fraud screening |
| Submits instruction | Creates TRANSFER/TRANSACTION and sends to gateway |
| Waits settlement | Receives success/failure from payment network |
| Reviews receipt | Publishes receipt and notification records |

### 4.3 Descriptor for UC-03 New Payee Setup
| Actor Task | System Response |
|---|---|
| Enters payee details | Validates input structure and duplicate payee rules |
| Saves payee | Queries directory/validation services |
| Completes SCA challenge | Applies risk controls and ownership checks |
| Confirms setup | Activates BENEFICIARY record |
| Views status | Sends activation notification and audit entry |

### 4.4 Descriptor for UC-04 Loan Application
| Actor Task | System Response |
|---|---|
| Submits application form | Validates completeness and required documents |
| Provides financial details | Pulls credit report and liabilities |
| Accepts terms (if approved) | Computes affordability and underwriting decision |
| Signs digitally | Creates loan account and repayment schedule |
| Tracks application | Returns lifecycle updates and notifications |

### 4.5 Descriptor for UC-05 Fraud Response
| Actor Task | System Response |
|---|---|
| Initiates high-value transfer | FraudEngine scores transaction risk |
| Responds to verification call/challenge | CaseMgr updates investigation status |
| Provides confirmation or denial | OpsConsole records disposition |
| Waits outcome | CoreAPI releases or blocks transaction |
| Receives notification | AuditSvc stores immutable incident record |

### 4.6 Descriptor for UC-06 Admin Freeze Account
| Actor Task | System Response |
|---|---|
| Requests account freeze | Validates administrator permissions |
| Provides reason/case id | Links action to active case |
| Confirms freeze action | Applies ACCOUNT status=FROZEN |
| Monitors result | Stops sessions and outbound transactions |
| Closes operation | Notifies customer and logs audit evidence |

---

## 5. Class Diagram and corresponding Entity Relationship Diagram

### 5.1 Class Diagram
(add class diagram here — `class-diagram-online-banking` exemplar)

**Interpretation highlights:**
- Attributes are attached to domain-appropriate classes (e.g., Account has balance/currency).
- Operations are behaviorally coherent (e.g., FraudCase has evaluate()/close()).
- Inheritance used where role specialization is needed (e.g., User → Customer/Admin/Underwriter).
- Multiplicities reflect business rules (e.g., Customer 1..* Account).
- Composition/aggregation relationships represent lifecycle ownership (e.g., Application contains Documents).

### 5.2 ERD
(add ERD here — `erd-online-banking` exemplar)

**Interpretation highlights:**
- PK/FK mappings align with class relationships.
- Main entities: USER, CUSTOMER, ACCOUNT, AUTH_SESSION, OTP_CHALLENGE, TRANSFER, TRANSACTION, BENEFICIARY, LOAN_APPLICATION, FRAUD_ALERT, NOTIFICATION.
- Cardinalities support transactional consistency and auditability.

---

## 6. 4–6 Activity Diagrams

1. (add activity diagram 1 here — Login & 2FA)
2. (add activity diagram 2 here — External Transfer)
3. (add activity diagram 3 here — New Payee Setup)
4. (add activity diagram 4 here — Loan Application)
5. (add activity diagram 5 here — Fraud High-Value Transfer)
6. (add activity diagram 6 here — Admin Freeze Account)

**Quality points addressed:**
- Correct start/end symbols, decisions, and fork/join logic.
- Activities named with clear verbs.
- Explicit rationale per diagram via linked use case.

---

## 7. 4–6 Sequence Diagrams and corresponding Collaboration Diagrams

### 7.1 Sequence Diagrams
1. (add sequence diagram 1 here — TPS Internal Transfer)
2. (add sequence diagram 2 here — TPS External Transfer)
3. (add sequence diagram 3 here — Payee Validation)
4. (add sequence diagram 4 here — Loan Processing/Underwriting)
5. (add sequence diagram 5 here — MIS Daily Reporting)
6. (add sequence diagram 6 here — Fraud Detection/Response)

### 7.2 Collaboration Diagrams
1. (add collaboration diagram 1 here — TPS Internal Transfer)
2. (add collaboration diagram 2 here — TPS External Transfer)
3. (add collaboration diagram 3 here — Payee Validation)
4. (add collaboration diagram 4 here — Loan Processing/Underwriting)
5. (add collaboration diagram 5 here — MIS Daily Reporting)
6. (add collaboration diagram 6 here — Fraud Detection/Response)

**Quality points addressed:**
- Each sequence explicitly maps to a use case.
- Lifelines/object instances identified correctly.
- Temporal order logically modeled.
- Message semantics consistent with activity/use-case logic.

---

## 8. 4–6 User Interfaces with HCI (Nielsen’s Heuristics)

1. **Login + 2FA UI**
   - Visibility of system status: clear “OTP sent” timer.
   - Error prevention: lockout warnings before max attempts.

2. **Transfer UI**
   - Match between system and real world: banking terms users understand.
   - User control/freedom: cancel transfer before submission.

3. **Payee Setup UI**
   - Recognition rather than recall: bank lookup/autocomplete.
   - Consistency and standards: common form patterns and validation messages.

4. **Loan Application UI**
   - Aesthetic/minimalist design: progressive form sections.
   - Help users recover from errors: inline corrections and document guidance.

5. **Fraud Verification UI**
   - Visibility of status: transfer under review timeline.
   - Help and documentation: “what happens next” guidance.

6. **Admin Freeze UI**
   - Error prevention: mandatory reason code and confirmation modal.
   - Audit transparency: visible action history and evidence IDs.

(add UI wireframe 1–6 here)

---

## 9. Conclusion
The UML artifacts collectively provide a multi-view system model for online banking. Use-case diagrams establish functional scope; class/ERD define structural and data integrity boundaries; activity diagrams show process logic; sequence/collaboration diagrams show interaction behavior; and UI/HCI considerations connect technical models to user-centered design quality.

---

## References (books / highly reputable sources)
1. Booch, G., Rumbaugh, J., & Jacobson, I. (2005). *The Unified Modeling Language User Guide* (2nd ed.). Addison-Wesley.
2. Fowler, M. (2004). *UML Distilled: A Brief Guide to the Standard Object Modeling Language* (3rd ed.). Addison-Wesley.
3. Larman, C. (2004). *Applying UML and Patterns* (3rd ed.). Prentice Hall.
4. Ambler, S. W. (2005). *The Elements of UML 2.0 Style*. Cambridge University Press.
5. Rumbaugh, J., Jacobson, I., & Booch, G. (2004). *The Unified Modeling Language Reference Manual* (2nd ed.). Addison-Wesley.
6. Nielsen, J. (1994). *Usability Engineering*. Morgan Kaufmann.
7. Pressman, R. S., & Maxim, B. R. (2019). *Software Engineering: A Practitioner’s Approach* (9th ed.). McGraw-Hill.
8. Dennis, A., Wixom, B. H., & Tegarden, D. (2015). *Systems Analysis and Design: An Object-Oriented Approach with UML* (5th ed.). Wiley.
9. Schaum’s Outlines. (various editions). *UML* / *Systems Analysis and Design* (descriptor-style worked tables and exercises).

---

## 10. UI Design Support Narrative (for Report Integration)

This section provides the explanatory text that supports the six UI pages in the report and links them directly to the UML artifacts.

### 10.1 Design objective
The UI layer is designed to operationalize the same use cases represented in the UML models. Each page maps to a primary use case and corresponding activity/sequence behavior. The design priorities are:
- **Security with usability** (especially for login, transfer, and admin actions),
- **Error prevention before irreversible actions**,
- **Clear system feedback and recoverability**,
- **Consistency of layout and interaction patterns** across all pages.

### 10.2 Mapping UI pages to UML use cases

1. **Login UI** → UC-01 Login with 2FA  
   Supports credential entry, MFA challenge, lockout/retry messaging, and session feedback.

2. **Bank Transfer UI** → UC-02 External Transfer  
   Supports account selection, beneficiary selection, amount/fee review, risk/limit validation, and confirmation.

3. **Mobile Vertical Dashboard/App** → post-auth customer operations (UC-01, UC-02, UC-03 linkage)  
   Supports quick navigation to balance, recent activity, transfer, and support pathways.

4. **Customer Support UI** → issue resolution and escalation extension use cases  
   Supports search-first help, ticket creation, chat/status tracking, and SLA visibility.

5. **Bank Admin Dashboard UI** → UC-06 Admin Freeze + fraud operations linkage  
   Supports high-risk queue review, freeze/unfreeze actions, and audit-oriented operational control.

6. **Loan Application UI** → UC-04 Loan Application  
   Supports staged form progression, document upload, eligibility preview, and submit/save draft outcomes.

### 10.3 Nielsen heuristic application by page

#### A. Login UI
- **Visibility of system status**: OTP sent timer, login security status, last-login context.
- **Error prevention**: password masking controls, field validation, attempt handling.
- **User control and freedom**: show/hide password, forgot-password recovery path.

#### B. Bank Transfer UI
- **Match with real world**: familiar banking terms (from account, beneficiary, amount, fee, ETA).
- **Error prevention**: pre-confirmation validation banner for limits/risk checks.
- **Recognition over recall**: account and beneficiary selectors reduce memory load.

#### C. Mobile Dashboard UI
- **Aesthetic/minimalist design**: prominent balance card + concise action shortcuts.
- **Visibility of status**: security status card and recent transactions.
- **Flexibility and efficiency**: one-tap access to common tasks.

#### D. Customer Support UI
- **Help and documentation**: search box and category entry points.
- **Visibility of status**: ticket timeline, ownership, and ETA indicators.
- **Error recovery**: clear issue description fields and escalation path.

#### E. Bank Admin Dashboard UI
- **Visibility of system status**: KPI tiles (alerts, frozen accounts, pending reviews).
- **Consistency and standards**: action center aligns with queue details.
- **Error prevention**: explicit freeze/unfreeze controls tied to case context.

#### F. Loan Application UI
- **Recognition rather than recall**: guided stepper and structured form grouping.
- **Error prevention**: document checklists and validation-friendly field grouping.
- **User control**: save draft in addition to submit.

### 10.4 UI quality controls used in the design set
- **Primary CTA hierarchy** (single dominant action per major step),
- **Secondary safety actions** (cancel/save draft/back),
- **Inline validation placement** near relevant fields,
- **Status messaging components** (warning/info/success cards),
- **Form chunking** to reduce cognitive load,
- **Accessible color contrast strategy** (dark text on light surfaces, high-emphasis CTA contrast),
- **Consistent spacing and card/grid rhythm** for learnability.

### 10.5 How UI design stays consistent with technical UML models
- **Use-case consistency**: each UI corresponds to a modeled use case and scenario.
- **Activity consistency**: decision points in activity diagrams map to visible UI states (e.g., validation banner, pending settlement, decline/approval message).
- **Sequence consistency**: backend steps that cause user-facing effects (notifications, delays, approvals) are surfaced as explicit status and feedback components.
- **Data consistency**: fields displayed in UI correspond to ERD/class entities (Account, Beneficiary, Transfer, LoanApplication, Notification, FraudAlert).

### 10.6 Suggested paragraph for report body
The six UI pages were intentionally designed as front-end realizations of the UML behavioral models rather than standalone mockups. Each interface maps to a defined use case and exposes the key decision and status transitions present in activity and sequence diagrams. Nielsen’s heuristics guided the interaction decisions to balance banking-grade control requirements with user comprehension and task efficiency. As a result, the UI artifacts are traceable to model semantics and suitable for design-to-engineering handoff.
