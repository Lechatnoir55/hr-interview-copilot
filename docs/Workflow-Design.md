# Workflow Design

## Workflow 1: Query the interviewer's Available Timeslot

### Objective

Look up the candidate by InterviewID or CandidateID, and return the interviewer's bookable times when the candidate is eligible.

### Inputs

- `InterviewID` or `CandidateID`, based on the actual input names used by the current Workflow

### Outputs

- `IsFound`
- `AvailableSlot`
- `CandidateName`
- `Position`
- `Status`
- `InterviewEmail`
- `CandidateEmail`

### Suggested Steps

1. Receive the candidate ID.
2. Validate that the ID is not empty.
3. Query the SharePoint InterviewCandidate List.
4. If there is no matching record, return `IsFound = No`.
5. If a record is found, return the candidate's basic information and status.
6. If the status permits booking, query the interviewer's available times.
7. Return a structured AvailableSlot.
8. Catch exceptions and return an identifiable error result.

### Example Response

```json
{
  "IsFound": "Yes",
  "CandidateName": "Demo Candidate",
  "Position": "Solution Consultant",
  "Status": "Applied",
  "CandidateEmail": "candidate@example.com",
  "InterviewEmail": "interviewer@example.com",
  "AvailableSlot": [
    "2026-09-24T10:00:00+08:00",
    "2026-09-24T14:00:00+08:00"
  ]
}
```

> The data above is for demonstration only and must not be used in place of real Workflow return values.

## Workflow 2: Teams

### Objective

After explicit user confirmation, create the Microsoft Teams interview meeting, send the Outlook invitation, and update the SharePoint candidate record.

### Inputs

- `InterviewID` or `CandidateID`
- `SelectedStartTime`
- `CandidateName`
- `CandidateEmail`
- `InterviewerEmail` or `InterviewEmail`
- `Position`

### Suggested Steps

1. Validate that the candidate ID, time, and email addresses are not empty.
2. Re-check the candidate record to avoid using stale context.
3. Create the Teams meeting.
4. Send the interview invitation email.
5. Write `InterviewTimeSlot` to SharePoint.
6. Update `Status` to `Scheduled`.
7. Return the result of each step.

### Suggested Response Structure

```json
{
  "Success": "Yes",
  "MeetingCreated": true,
  "EmailSent": true,
  "SharePointUpdated": true,
  "Message": "Booking completed"
}
```

## Consistency and Compensation

Meeting creation, email delivery, and the SharePoint update are multiple steps. The Workflow should return the status of each step separately so that a partial failure is not reported as an overall success.

Examples:

- Meeting created successfully but the SharePoint update failed: remind HR to check the record manually.
- Meeting creation failed: do not go on to declare the booking successful.
- Email delivery failed: return an explicit status so that HR can resend the notification.

## Input/Output Mapping Checklist

- Variable names in the Topic match the Workflow input names
- `SelectedStartTime` uses a date-time format the Workflow can parse
- The mapping between `InterviewEmail` and `InterviewerEmail` is unambiguous
- The return type of `AvailableSlot` is fixed
- The value ranges of `IsFound` and `Success` are fixed — for example `Yes/No` or Boolean — and not mixed
