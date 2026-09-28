
# Phase 2: Requirement Analysis

## 1. Functional Requirements

### FR-1: Dynamic UI Control (High Impact)
* **Trigger:** When Impact is set to `1 - High`[cite: 1].
* **Behavior:** Automatically make the `Urgency` field read-only[cite: 1].
* **Reversal:** Revert back to original state if Impact is changed from High[cite: 1].

### FR-2: Auto-Populate Urgency
* **Trigger:** `onChange` event of the `Impact` field on the Incident form[cite: 1].
* **Behavior:** When Impact is changed to `1 - High`, set `Urgency` to `1 - High` and display an informational banner message to the user[cite: 1].

### FR-3: Form Submission Validation
* **Trigger:** `onSubmit` event on the Incident form[cite: 1].
* **Behavior:** Validate if `Impact` is `1 - High`. If `Assigned To` is empty, block submission and display an error box under `Assigned To`[cite: 1].

### FR-4: List Edit Restriction
* **Trigger:** `onCellEdit` event on the Incident table list view for the `State` field[cite: 1].
* **Behavior:** Prevent list-editing of the `State` field, prompt an alert to the user, and mandate state updates through the form view[cite: 1].

## 2. Technical Stack & Target Platform
* **Platform:** ServiceNow (San Diego / Tokyo / Utah / Washington / Xanadu)[cite: 1]
* **Target Table:** `Incident` (`incident`)[cite: 1]
* **Modules Required:** System UI → UI Policies, System UI → Client Scripts[cite: 1]
