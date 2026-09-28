```markdown
# Phase 3: Project Design

## 1. System Architecture & Component Interaction
The solution combines UI Policies for client-side state enforcement with specialized Client Scripts to handle user-driven events, form submissions, and list-level interactions[cite: 1].


```

```
                           ┌────────────────────────────────┐
                           │  User Action on Incident Form  │
                           └───────────────┬────────────────┘
                                           │
           ┌───────────────────────────────┼───────────────────────────────┐
           │                               │                               │
           ▼                               ▼                               ▼
[ Change Impact Field ]            [ Submit / Save Form ]             [ Edit State in List ]
           │                               │                               │
           ├──────────────────────┐        │                               │
           ▼                      ▼        ▼                               ▼

```

onChange Client Script     UI Policy Action  onSubmit Client Script   onCellEdit Client Script
(Auto-sets Urgency = 1)   (Sets Urgency      (Validates Assigned To   (Blocks list edit &
to Read-Only)      field presence)          displays alert message)

```

---

## 2. Dynamic Behavior & Logic Flow


```

[ Impact set to "1 - High" ]
│
├───► onChange Script Execution
│       ├── Set Urgency = '1' (High)
│       └── Add Info Message: "Urgency set to High for High impact incident."
│
├───► UI Policy Application ("High Impact Control")
│       └── Set Urgency Field -> Read-Only = true
│
└───► Condition Reversal ("Reverse if false = true")
└── When Impact != "1 - High", Urgency reverts to editable

```


```

[ User Clicks Submit / Save ]
│
└───► onSubmit Script Execution
├── Check: Is Impact == '1' AND Assigned To == '' ?
├── TRUE  ──► Show Error Box on Assigned To field
│             RETURN FALSE (Block Form Submission)
└── FALSE ──► RETURN TRUE (Allow Form Submission)

```


```

[ User Double-Clicks State Field in List View ]
│
└───► onCellEdit Script Execution
├── Trigger Alert: "State cannot be updated using list editing. Please open the Incident."
└── Call callback(false) (Cancel List Modification)

```

---

## 3. Configuration Specifications

### A. UI Policy Specification
| Attribute | Value | Description |
| :--- | :--- | :--- |
| **Name** | `High Impact Control` | Name of the policy[cite: 1]. |
| **Table** | `Incident [incident]` | Target ServiceNow table[cite: 1]. |
| **Active** | `true` | Policy status[cite: 1]. |
| **Condition** | `Impact IS 1 - High` | Trigger filter condition[cite: 1]. |
| **Reverse if false** | `true` | Auto-reverts action when condition is not met[cite: 1]. |
| **Global** | `true` | Applies across all form views[cite: 1]. |
| **On load** | `true` | Evaluates when the form finishes loading[cite: 1]. |

### B. UI Policy Action Specification
| Target Field | Read-only | Mandatory | Visible | Description |
| :--- | :---: | :---: | :---: | :--- |
| `Urgency` | `true` | `Leave unchanged` | `Leave unchanged` | Locks the Urgency field when Impact is High[cite: 1]. |

### C. Client Scripts Specifications
| Parameter | Script 1 | Script 2 | Script 3 |
| :--- | :--- | :--- | :--- |
| **Name** | `Auto set urgency for high impact`[cite: 1] | `Prevent save if Assigned To missing`[cite: 1] | `Prevent state change via list edit`[cite: 1] |
| **Table** | `Incident [incident]`[cite: 1] | `Incident [incident]`[cite: 1] | `Incident [incident]`[cite: 1] |
| **Type** | `onChange`[cite: 1] | `onSubmit`[cite: 1] | `onCellEdit`[cite: 1] |
| **Field Name** | `Impact`[cite: 1] | *N/A* | `State`[cite: 1] |
| **Active** | `true`[cite: 1] | `true`[cite: 1] | `true`[cite: 1] |
| **Primary Function** | Auto-populates `Urgency` to High (`1`)[cite: 1]. | Prevents record save if `Assigned To` is blank[cite: 1]. | Restricts modifying `State` via list view[cite: 1]. |

```
