# Business Scenario

## 1. Scenario Overview

When arranging interviews, HR needs to look up candidate information, confirm the interviewer's availability, create Teams meetings, send notifications, and write the results back to the candidate record. Handling this manually easily leads to duplicate lookups, missed notifications, out-of-sync statuses, and mistakes.

HR Interview Assistant provides a single natural-language entry point, but it does not rely on model memory to answer questions about candidate data. Anything involving candidates, interview times, email addresses, statuses, and results must be retrieved from the SharePoint List or the corresponding Workflow.

## 2. Target Users

- Recruiters
- HR operations staff
- Business users authorized to help schedule interviews

## 3. Core User Stories

### User Story A: Schedule an interview by ID

As an HR user, I want to enter an InterviewID or CandidateID and look up the candidate plus the interviewer's bookable times, so that I can choose a suitable time and create the interview meeting.

**Acceptance criteria:**

1. If no ID has been entered, the agent must first ask for the ID.
2. Once an ID is entered, the agent must call the query Workflow.
3. If the candidate does not exist, no speculative information is displayed.
4. Only statuses that permit booking allow the flow to continue.
5. After the user selects a time, the agent must display the booking summary.
6. No meeting may be created without explicit user confirmation.
7. Booking success may only be reported after the Teams Workflow returns success.

### User Story B: Query unbooked candidates

As an HR user, I want to see candidates whose interviews have not yet been scheduled, so that I can continue scheduling them.

**Current status:** The batch query Workflow is not yet enabled. The agent should guide the user to enter a single CandidateID or InterviewID and must not fabricate a list.

### User Story C: Analyze recruitment progress

As an HR user, I want to see the total number of candidates, booked, unbooked, and completed counts, different results, and the position distribution, so that I can understand recruitment progress.

**Current status:** The analysis Workflow is not yet enabled. The agent may only describe the recommended metrics and must not generate fake numbers.

## 4. Business Rules

- The SharePoint InterviewCandidate List is the single source of truth for candidate data.
- Whenever personal information or business status is involved, a Topic or Workflow must be called.
- Statuses such as `Completed`, `Rejected`, and `Cancelled` must not proceed with booking.
- Whether statuses such as `Applied`, `Pending`, and `Pass` permit booking should match the company's actual process.
- Meeting creation must only happen after explicit user confirmation.
- The results of creating a meeting, sending email, and updating SharePoint must come from Workflow return values.

## 5. Success Criteria

- The agent does not fabricate personal information or business results.
- A user can complete an end-to-end booking for a single candidate.
- Every write operation has an explicit confirmation step.
- Error messages are clear and guide the user back into the flow.
- Public demonstration materials contain no real personal data or connection credentials.
