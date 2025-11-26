# Interview Reschedule Request Screen

## Purpose
Request and manage interview rescheduling.

## Fields
- InterviewRescheduleRequestID (system-generated)
- InterviewScheduleID (dropdown, required)
- PreviousInterviewScheduleID (dropdown, auto)
- NewInterviewScheduleID (dropdown, required)
- Reason (textarea, required)
- RequestStatus (dropdown, required)
- IsActive (checkbox, required)
- CreatedDate (auto)
- ModifiedDate (auto)
- ModUser (auto)
- Source (dropdown, required)

## Actions
- Create Request
- Approve/Reject Request

## Layout Suggestion
RequestID | Interview | Previous | New | Reason | Status | Actions
[Create Request]
