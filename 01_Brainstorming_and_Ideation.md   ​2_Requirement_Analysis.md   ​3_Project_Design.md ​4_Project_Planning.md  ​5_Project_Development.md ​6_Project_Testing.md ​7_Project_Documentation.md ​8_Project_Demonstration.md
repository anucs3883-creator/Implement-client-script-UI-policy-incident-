# Implement Client Script & UI Policy (Incident)

## Phase 1: Project Overview & Objectives 
* **Problem Statement:** Manual data entry on Incident records often leads to incomplete, inconsistent, or inaccurate data submission, impacting reporting accuracy, SLA compliance, and overall service quality.
* **Objective:** Demonstrate how ServiceNow client-side controls (UI Policies and Client Scripts) enforce data integrity by dynamically controlling field visibility, mandatory status, auto-populating values, and validating submissions.
* **Skills Covered:** Incident Management, UI Policy, UI Policy Actions, Client Scripts, and Form Validation.

---

## Phase 2: Task 1 – Create UI Policy on Incident
1. **Navigate:** Go to **System UI** → **UI Policies** and click **New**.
2. **Details:** Set **Name** to `High Impact Control`, **Table** to `Incident`, and **Active** to `true`.
3. **Condition:** Add condition where **Impact** `is` `1 - High`.
4. **Settings:** Set **Reverse if false** to `true` to automatically revert changes when conditions evaluate to false.
5. **Submit:** Review configuration and click **Submit** to save the UI Policy.

---

## Phase 3: Task 2 – Create UI Policy Action (Urgency Field)
1. **Open UI Policy Action:** Access the **UI Policy Actions** related list under `High Impact Control` and click **New**.
2. **Configure Action:**
   * **Field name:** Select `Urgency`.
   * **Read-only:** Set to `true`.
   * **Visible:** Leave unchanged.
3. **Save:** Click **Submit** to link the action to the UI Policy.

---

## Phase 4: Task 3 – Create onChange Client Script
1. **Navigate:** Go to **System UI** → **Client Scripts** and click **New**.
2. **Details:** Set **Name** to `Auto set urgency for high impact`, **Table** to `Incident`, **Type** to `onChange`, **Field name** to `Impact`, and **Active** to `true`[cite: 1].
3. **Script Execution:**
   ```javascript
   function onChange(control, oldValue, newValue, isLoading) {
       if (isLoading || newValue == '') {
           return;
       }
       if (newValue == '1') {
           g_form.setValue('urgency', '1');
           g_form.addInfoMessage('Urgency set to High for High impact incident.');
       }
   }# Implement Client Script & UI Policy (Incident)

## Phase 1: Project Overview & Objectives
* **Problem Statement:** Manual data entry on Incident records often leads to incomplete, inconsistent, or inaccurate data submission, impacting reporting accuracy, SLA compliance, and overall service quality.
* **Objective:** Demonstrate how ServiceNow client-side controls (UI Policies and Client Scripts) enforce data integrity by dynamically controlling field visibility, mandatory status, auto-populating values, and validating submissions.
* **Skills Covered:** Incident Management, UI Policy, UI Policy Actions, Client Scripts, and Form Validation.

---

## Phase 2: Task 1 – Create UI Policy on Incident
1. **Navigate:** Go to **System UI** → **UI Policies** and click **New**.
2. **Details:** Set **Name** to `High Impact Control`, **Table** to `Incident`, and **Active** to `true`.
3. **Condition:** Add condition where **Impact** `is` `1 - High`.
4. **Settings:** Set **Reverse if false** to `true` to automatically revert changes when conditions evaluate to false.
5. **Submit:** Review configuration and click **Submit** to save the UI Policy.

---

## Phase 3: Task 2 – Create UI Policy Action (Urgency Field)
1. **Open UI Policy Action:** Access the **UI Policy Actions** related list under `High Impact Control` and click **New**.
2. **Configure Action:**
   * **Field name:** Select `Urgency`.
   * **Read-only:** Set to `true`.
   * **Visible:** Leave unchanged.
3. **Save:** Click **Submit** to link the action to the UI Policy.

---

## Phase 4: Task 3 – Create onChange Client Script
1. **Navigate:** Go to **System UI** → **Client Scripts** and click **New**.
2. **Details:** Set **Name** to `Auto set urgency for high impact`, **Table** to `Incident`, **Type** to `onChange`, **Field name** to `Impact`, and **Active** to `true`[cite: 1].
3. **Script Execution:**
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
