# Phase 5: Project Development

## Step 1: Create UI Policy & Action
1. Navigate to **System UI** → **UI Policies** and click **New**[cite: 1].
2. Set **Name** to `High Impact Control`, **Table** to `Incident`, **Active** to `true`[cite: 1].
3. Set Condition: `Impact is 1 - High`[cite: 1].
4. Set **Reverse if false** to `true` and click **Submit**[cite: 1].
5. Under **UI Policy Actions** related list, click **New**[cite: 1]:
   * **Field name:** `Urgency`[cite: 1]
   * **Read-only:** `true`[cite: 1]
   * Click **Submit**[cite: 1].

---

## Step 2: Create onChange Client Script
* **Navigation:** **System UI** → **Client Scripts** → **New**[cite: 1]
* **Name:** `Auto set urgency for high impact`[cite: 1]
* **Table:** `Incident [incident]` | **Type:** `onChange` | **Field name:** `Impact` | **Active:** `true`[cite: 1]

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
