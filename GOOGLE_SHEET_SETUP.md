# Google Sheet Lead Capture Setup Guide (1-Minute Setup)

Follow these simple steps to save website leads automatically into your Google Sheet:

---

### Step 1: Create a Google Sheet
1. Open [Google Sheets](https://sheets.new) and create a new spreadsheet.
2. In the first row (**Row 1**), write these exact column headers:
   - **A1**: `Timestamp`
   - **B1**: `Name`
   - **C1**: `Phone`
   - **D1**: `Email`
   - **E1**: `City`
   - **F1**: `Mode`

---

### Step 2: Add the Google Apps Script
1. In your Google Sheet, click **Extensions** → **Apps Script**.
2. Delete any code in the editor and paste the following:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var p = e.parameter;
  
  sheet.appendRow([
    p.Timestamp || new Date().toLocaleString('en-IN', { timeZone: 'Asia/Kolkata' }),
    p.Name || '',
    p.Phone || '',
    p.Email || '',
    p.City || '',
    p.Mode || 'Offline Classroom (Pune)'
  ]);
  
  return ContentService.createTextOutput(JSON.stringify({ 'result': 'success' }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. Click the **Save** icon (disk icon) or press `Ctrl + S`.

---

### Step 3: Deploy as Web App
1. Click the blue **Deploy** button (top right) → **New deployment**.
2. Click the gear icon ⚙️ next to "Select type" and choose **Web app**.
3. Configure the settings:
   - **Description**: `Chaitanya Lead Form`
   - **Execute as**: `Me`
   - **Who has access**: `Anyone` *(Crucial so the website can submit leads)*
4. Click **Deploy**.
5. Copy the **Web App URL** (it looks like `https://script.google.com/macros/s/.../exec`).

---

### Step 4: Paste URL in `index.html`
1. Open `index.html`.
2. Locate line `~2308`:
   ```javascript
   const GOOGLE_SHEET_URL = 'PASTE_YOUR_COPIED_URL_HERE';
   ```
3. Save `index.html`.

That's it! Every time someone submits the enquiry form:
- The lead is saved directly in your Google Sheet.
- An instant WhatsApp chat window opens with the lead's details pre-filled.
