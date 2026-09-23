# Security and Privacy

## 1. Redaction Requirements for the Public Repository

A public GitHub repository must not contain:

- Real candidate names, personal email addresses, phone numbers, resumes, feedback, or interview results
- Real interviewer email addresses or calendar information
- SharePoint Site URL, Tenant ID, Environment ID
- Power Automate connections, access tokens, connection strings, or API keys
- Workflow run history containing real personal information
- Unreviewed solution export packages

Before taking screenshots:

- Use a test environment and fictional data
- Redact the browser address bar and environment identifiers
- Redact email addresses, candidate IDs, and connection names
- Check image metadata and file names

## 2. Principle of Least Privilege

A production solution should grant only the access required to do the job:

- The agent reads only the necessary candidate fields
- The Workflow updates only the necessary status and time fields
- Only authorized HR users can perform bookings
- Non-HR users should not be able to batch-query personal information

## 3. User Confirmation

Creating meetings, sending email, and updating SharePoint are write operations. The agent must:

1. Display the booking summary
2. Obtain explicit confirmation
3. Call the Workflow
4. Describe the execution status based on the actual return value

## 4. Logging and Auditing

Recommended fields to record:

- Operation timestamp
- Candidate record identifier
- Operation type
- Execution result
- Workflow Run ID
- Error reason

The public portfolio only describes the audit design; it does not upload real run logs containing personal data.

## 5. Data Retention

Before a real enterprise deployment, retention and deletion rules for candidate data, conversation records, interview feedback, and Workflow logs must be defined according to company policy. This portfolio does not replace an organization's legal, privacy, or compliance review.

## 6. Demo Data Rules

All demo data must:

- Be clearly labeled as fictional or test data
- Use an example domain, such as `example.com`
- Not correspond to any real individual
- Not contain credentials that could be used to access real systems
