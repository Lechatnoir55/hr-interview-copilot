# Demo Script

## Demo Objective

Use a fictional candidate to demonstrate how HR Interview Assistant completes the end-to-end flow of "live lookup, time selection, user confirmation, meeting creation, email notification, and status update".

## Pre-Demo Preparation

- Use a test SharePoint List and fictional candidates
- Verify the Availability Workflow returns test times correctly
- Verify the Teams Workflow uses test email addresses
- Hide or redact the tenant, environment, site URL, and connection information in the browser
- Prepare screenshots of the overview, topics, Workflow runs, and the updated SharePoint record

## Opening Narration

> This is an enterprise HR interview assistant built with Microsoft Copilot Studio. The point of this project is not ordinary Q&A — it is chaining natural-language interaction with live SharePoint data, the interviewer's calendar, Teams meetings, and Outlook notifications. I also added data-truthfulness constraints and user confirmation before any write operation.

## Demo Steps

### 1. Show the welcome entry point

Input:

```text
Start
```

Narration:

> The agent offers three business entry points. Booking a single candidate by ID is already configured; batch booking and data analysis are reserved for the next phase.

### 2. Enter the booking flow

Input:

```text
Book by ID lookup
```

Expected: the agent requests the candidate ID.

### 3. Enter a test ID

Input:

```text
20260724-0002
```

Narration:

> The agent will not answer candidate questions on its own. Once an ID is entered, it must call the Availability Workflow, return the candidate information from SharePoint, and query the interviewer's bookable times.

### 4. Show the query results

Show:

- CandidateName
- Position
- Status
- CandidateEmail
- InterviewEmail
- AvailableSlot

Narration:

> If the candidate does not exist, the status does not permit booking, or no time slot is available, the agent branches to the corresponding exception path and does not create a meeting.

### 5. Select a time

Input:

```text
Select the 2nd option
```

Expected: the agent displays the booking summary.

### 6. Emphasize the confirmation mechanism

Narration:

> Creating a meeting is a write operation. The agent must first show the candidate, position, time, and email addresses, then obtain explicit user confirmation. Without confirmation, the Teams Workflow is not called.

Input:

```text
Confirm booking
```

### 7. Show the execution result

Narration:

> The Teams Workflow is responsible for creating the meeting, sending the Outlook invitation, and updating SharePoint. The agent only tells the user the booking succeeded after the Workflow returns success.

Show:

- Workflow run result
- Teams meeting
- Test invitation email
- `InterviewTimeSlot` and `Status = Scheduled` in SharePoint

## Closing Summary

> This demo shows how I break an HR business process down into the agent's topics, workflows, data constraints, user confirmation, and error handling. The next phase can add batch booking, feedback collection, and recruitment progress analysis, and further strengthen permissions, auditing, and exception compensation.

## 60-Second Project Pitch

> I built an HR interview assistant with Microsoft Copilot Studio and connected SharePoint, Teams, and Outlook through Power Automate. After HR enters an InterviewID or CandidateID, the agent queries the candidate's status and the interviewer's bookable times in real time. Only after the user selects a time and confirms does the system create the Teams meeting, send the invitation, and update SharePoint. To reduce the risk of generative AI, I required all personal information and business status to come from Workflows, and allowed the agent to declare a successful booking only after a Workflow returns success. This project mainly demonstrates my ability to turn business requirements into a controlled agent flow and a Microsoft 365 automation solution.
