# Phase 6: Project Testing

## Test Execution Matrix

| Test ID | Test Scenario | Steps Executed | Expected Result | Pass/Fail |
| :---: | :--- | :--- | :--- | :---: |
| **TC-01** | Mandatory Field Enforcement | 1. Open Incident form.<br>2. Set `Impact = High`.<br>3. Leave `Assigned To` empty.<br>4. Click Submit[cite: 1]. | Form submit is blocked. Error box appears on `Assigned To`[cite: 1]. | **PASS** |
| **TC-02** | Successful Form Submit | 1. Set `Impact = High`.<br>2. Populate `Assigned To`.<br>3. Click Submit[cite: 1]. | Record saves successfully. Urgency auto-sets to High & becomes read-only[cite: 1]. | **PASS** |
| **TC-03** | Reverse Condition Check | 1. Open record where `Impact = High`.<br>2. Change `Impact` to `Medium`.<br>3. Verify behavior[cite: 1]. | `Urgency` field becomes editable and `Assigned To` requirement releases[cite: 1]. | **PASS** |
| **TC-04** | List View Edit Blocking | 1. Navigate to Incident list view.<br>2. Double click `State` column to edit[cite: 1]. | Alert box pops up blocking edit. Cell reverts to original value[cite: 1]. | **PASS** |
| **TC-05** | Form View State Update | 1. Open Incident record.<br>2. Change `State` on form view.<br>3. Click Update[cite: 1]. | Record updates successfully without restriction[cite: 1]. | **PASS** |

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/6ced8bdf-c15c-4eb3-88da-d2212d0d7ff3" />
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/7584f3e4-3026-4409-9399-d51bd18ae569" />
