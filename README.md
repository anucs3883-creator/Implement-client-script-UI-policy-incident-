# ServiceNow: Implement Client Script & UI Policy (Incident)

## Project Overview
This repository contains the complete implementation details for enforcing client-side data integrity on the ServiceNow **Incident** table using **UI Policies** and **Client Scripts**.

The objective of this project is to demonstrate how client-side controls dynamically enforce business rules on Incident records, ensuring required fields are populated, values are auto-set, and unauthorized modifications are blocked at the user interface level.

---

## Core Features & Functionalities
* **Dynamic Field Control:** Automatically locks the `Urgency` field as read-only whenever `Impact` is set to High (`1 - High`).
* **Automated Field Value Setting:** Uses an `onChange` client script to set `Urgency` to High (`1`) and displays an informational message when `Impact` changes to High.
* **Submit-Time Validation:** Uses an `onSubmit` client script to prevent saving an incident if `Assigned To` is missing while `Impact` is High[cite: 1].
* **List-Edit Protection:** Uses an `onCellEdit` client script to block direct updates to the `State` field from the list view, requiring users to open the form view[cite: 1].

---

## Implementation Summary

| Component Name | Type | Target Field | Purpose |
| :--- | :--- | :--- | :--- |
| **High Impact Control** | UI Policy | N/A | Evaluates when `Impact` is `1 - High` with `Reverse if false` enabled[cite: 1]. |
| **Urgency Read-Only Action** | UI Policy Action | `Urgency` | Sets the `Urgency` field to Read-Only when the UI Policy conditions are met[cite: 1]. |
| **Auto set urgency for high impact** | `onChange` Script | `Impact` | Auto-populates `Urgency` to `1` when `Impact` is updated to `1`[cite: 1]. |
| **Prevent save if Assigned To missing** | `onSubmit` Script | `Assigned To` | Prevents saving if `Assigned To` is empty on High impact incidents[cite: 1]. |
| **Prevent state change via list edit** | `onCellEdit` Script | `State` | Prevents inline editing of `State` from the list view[cite: 1]. |

---

## Technical Implementation Snippets

### 1. Auto-set Urgency (`onChange`)
```javascript
function onChange(control, oldValue, newValue, isLoading) {
    if (isLoading || newValue == '') {
        return;
    }
    if (newValue == '1') {
        g_form.setValue('urgency', '1');
        g_form.addInfoMessage('Urgency set to High for High impact incident.');
    }
}
