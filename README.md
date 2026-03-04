# Holi Email Bot – n8n Workflow

Automated sender of personalized Holi greeting emails using n8n, Google Sheets (contact list), and Gmail (OAuth2).

**Security warning**  
This workflow JSON contains **no credentials, no sheet IDs, no personal data**. You must configure your own Google Sheets and Gmail credentials after importing.

## What it does
- Triggers annually on March 4 at 18:00 IST (6 PM) via cron: `0 18 4 3 *`
- Reads rows from a Google Sheet (expected columns: Email, Name, Message)
- Sends one personalized email per row via Gmail
- Intended for one-time use per year → deactivate after execution to prevent repeats

**Note on date**  
Workflow uses March 4 every year (matches Holi 2026 in most calendars). Actual Holi date can vary slightly by region/Panchang—confirm locally.

## Requirements
- n8n (self-hosted or cloud)
- Google account with:
  - Sheets API enabled
  - Gmail API enabled
- Google Sheet with columns:
  - Email (required)
  - Name (optional)
  - Message (optional)

## How to use
1. Download: [holi-email-bot.json](./holi-email-bot.json) (or the name you used)
2. In n8n: Workflows → Import from File → upload the JSON
3. Set workflow timezone: Settings → Timezone → Asia/Kolkata
4. Create credentials:
   - Google Sheets OAuth2
   - Gmail OAuth2
5. Configure nodes:
   - Google Sheets: paste your Document ID, select correct Sheet name, set range if needed
   - Gmail: set From Email, adjust Subject/Message if desired (expressions like `{{ $json.Name }}` are already set)
6. Test: Execute Workflow manually (should send emails if sheet has data)
7. When ready: Save → Publish → Activate
8. After it runs on March 4 → deactivate or delete the workflow

## Workflow structure
Schedule Trigger (cron: 0 18 4 3 *)
→ Google Sheets (Read rows)
→ Gmail (Send one email per row)


## Important
- Keep your contact list small and personal. Bulk emailing friends can trigger Google's spam filters or policy violation.
- If no rows in sheet → no emails sent.
- Test thoroughly before the real date.

## License
MIT

## Disclaimer
Use at your own risk. No support provided. Wrong credentials/range = no emails. Duplicate sends = angry friends.
