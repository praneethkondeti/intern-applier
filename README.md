# Intern Applier

This project is an n8n workflow that automatically reads new rows from a Google Sheet, generates an internship application email using Google Gemini, and sends it through Gmail.

## Workflow overview

The workflow does the following:

1. Watches a Google Sheet for new updates.
2. Reads values from the row, including:
   - Full Name
   - Email
   - Position Applied
   - Details
   - Experience (Years)
   - Skills
3. Sends those values into a LangChain LLM prompt.
4. Uses a structured output parser to generate a valid email object with:
   - to
   - subject
   - body
5. Sends the email using Gmail.

## Source file

- Workflow file: [Intern applier (2).json](Intern%20applier%20%282%29.json)

## Google Sheet configuration

The workflow is connected to this spreadsheet:

- Spreadsheet ID: 1oULDcENAeFZfKnsnWn8wF4kAsru6uzgrb5r6RvUdKrI
- Sheet name: Sheet1
- Sheet link: https://docs.google.com/spreadsheets/d/1oULDcENAeFZfKnsnWn8wF4kAsru6uzgrb5r6RvUdKrI/edit#gid=0

This sheet is used as the trigger source for new application entries.

## Authentication details

The JSON contains credential references, not the actual secret tokens. In n8n, the real OAuth credentials are stored securely in the n8n instance and linked through these records.

### 1. Google Sheets trigger authentication

- Credential type: Google Sheets OAuth2
- Credential ID: xd0PGMuJyvpzzAsp
- Credential name: Google Sheets Trigger account 901

### 2. Google Gemini authentication

- Credential type: Google Gemini / PaLM API
- Credential ID: NNKzhKmGyLdlFA6g
- Credential name: Google Gemini(PaLM) Api account 3059

### 3. Gmail authentication

- Credential type: Gmail OAuth2
- Credential ID: fx7Pw9C1TmTm7f4t
- Credential name: Gmail account 1135

> Important: The actual access tokens, refresh tokens, and client secrets are not present in this JSON. Those are stored in the n8n credential store for your environment.

## How the prompt works

The workflow builds a prompt using row data such as:

- Name
- Email
- Internship role
- Details
- Experience
- Skills

Then it asks the LLM to generate a polished internship email in a ready-to-send format, using the greeting:

- Dear Hiring Manager

The email is then sent to the candidate's target email address, derived from the sheet row.

## Important notes

- This is an n8n workflow, so it must be imported into an n8n instance.
- The workflow is currently set as inactive in the JSON: active: false.
- The actual credentials must be reconnected in the target n8n environment if this workflow is imported elsewhere.
- The workflow depends on valid Google Sheets, Google Gemini, and Gmail credential permissions.

## Requirements for running

To run this workflow in another environment, make sure:

- n8n is installed and running
- The Google Sheets credential is authorized for the spreadsheet
- The Gemini API credential is valid
- The Gmail OAuth account is authorized to send emails
- The spreadsheet columns match the field names used by the prompt

## Suggested fields in the sheet

Make sure the Google Sheet contains columns like:

- Full Name
- Email
- Position Applied
- Details
- Experience (Years)
- Skills

## Summary

This workflow is a simple AI-powered internship application automation system that turns spreadsheet data into personalized emails and sends them automatically.
