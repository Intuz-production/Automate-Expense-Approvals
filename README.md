*Intuz — Your automation partner, one workflow at a time.*

<p align="center">
  <picture>
    <img alt="Banner Image" src="https://github.com/user-attachments/assets/210f97fc-0fce-404a-b647-7dfe1302cd37" />
  </picture>
</p>

[Intuz](https://www.intuz.com) helps organizations orchestrate AI, automation, and enterprise systems through scalable workflows. Our repository showcases proven implementations across healthcare, operations, customer support, document processing, sales, and back-office functions, enabling teams to accelerate automation initiatives without starting from scratch.

[N8N Creator](https://n8n.io/creators/intuz/) · [AI Automation Agency](https://www.intuz.com/company/) · [Generative AI Development Company](https://www.intuz.com/generative-ai-development/) · [For Custom Workflow Automation](https://www.intuz.com/get-started/)

# Approve Slack expense receipts and post invoices to Xero with Textract and OpenAI

## Quick overview

This workflow captures expense receipt images shared in Slack, extracts key fields with AWS Textract, categorizes the spend with OpenAI, requests manager approval in Slack, then creates an authorised ACCPAY invoice in Xero with the receipt attached and logs the outcome to Google Sheets.

## How it works

1. Triggers when a file is shared in Slack and downloads the shared file.
2. Filters events to receipt image uploads and sends the image to AWS Textract AnalyzeExpense to extract vendor, total, date, and currency.
3. Uses OpenAI to assign a single expense category from a fixed list and normalizes the extracted fields while checking Textract confidence thresholds.
4. If the extraction is low confidence, sends a Slack message asking the uploader to resend a clearer photo.
5. If the extraction is confident, posts a Slack approval request that pauses until a manager approves or rejects.
6. On approval, maps the category to a Xero account code, creates an authorised Xero ACCPAY invoice (routing via one of two Xero API requests), reattaches the original receipt image as an invoice attachment, and appends an “approved” entry to Google Sheets.
7. On rejection, notifies the original Slack user and appends a “rejected” entry to Google Sheets.

## Setup

1. Connect Slack OAuth credentials with permission to receive file_share events, download files, send messages, and use interactive approvals, then set the trigger and approval channel/user to match where receipts and approvals happen.
2. Add AWS credentials with permission for Textract AnalyzeExpense and ensure the Slack-downloaded file is provided as binary data to Textract.
3. Add an OpenAI API credential for the chat categorization request.
4. Connect Xero via OAuth2, confirm the Xero Tenant ID header is set for your organisation, and adjust the invoice details (e.g., due date policy, tax type, and Contact naming) if needed.
5. Connect Google Sheets credentials and update the spreadsheet and sheet (tab) used for the ExpenseAudit lookup/log so it matches your document structure, then adjust the category-to-account-code mapping if your chart of accounts differs.

## Requirements

- Slack bot (files + messaging) and an approval channel
- AWS IAM with Textract AnalyzeExpense
- OpenAI API credential
- Xero OAuth connected to org INTUZ (tenant already configured)
- Google Sheet n8n poc → tab ExpenseAudit
- Workflow published (draft ≠ live)

## FAQ

**What triggers this workflow?**  
The workflow triggers when a file is shared in Slack.

**How does the workflow handle low confidence expense extraction?**  
If the extraction confidence is low, the workflow sends a Slack message asking the uploader to resend a clearer photo.

**What happens after a manager approves an expense?**  
On approval, the workflow creates an authorised ACCPAY invoice in Xero with the receipt attached and logs the approval in Google Sheets.

## Related n8n templates from Intuz

- [Google and Facebook sign in using firebase authentication](https://github.com/Intuz-production/Firebase-authenticaiton-android)
- [CalendarView](https://github.com/Intuz-production/CalendarView)
- [CustomLoaderView SwiftUI](https://github.com/Intuz-production/CustomLoaderView-SwiftUI)

[See all of Intuz's free n8n templates](https://www.intuz.com/n8n-workflow-automation-templates/)

## Connect with us

Intuz is a USA-based AI & workflow automation company with 16+ years of experience building custom AI-enabled workflow automations for SMBs and Enterprises, specializing in agentic AI, LLM integrations, and CRM/ERP sync across Healthcare, FinTech, eCommerce, Manufacturing, and Real Estate.

* **Website:** [https://www.intuz.com](https://www.intuz.com)
* **Email:** [getstarted@intuz.com](mailto:getstarted@intuz.com)
* **LinkedIn:** https://www.linkedin.com/company/intuz/
* **Get Started:** https://n8n.partnerlinks.io/intuz

## For Custom Workflow Automation

[Click here - Get Started](https://www.intuz.com/get-started/)
