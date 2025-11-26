# FR#ISM-Feedback-Submission – Submit Interview Feedback

## FR#ISM-Feedback-Submission – Submit Interview Feedback

### Description
Panel members must submit feedback for each interview they conduct. Feedback is linked to the interview, candidate, and panel member, and is used for hiring decisions, reporting, and audit purposes.

### User Roles
- Panel Member (submit feedback)
- TA/Admin (review feedback)

---
### Preconditions and Postconditions
- [Preconditions]
	- Interview must be completed.
	- Panel member is assigned to the interview.
	- Feedback template is available for the interview type/role.
- [Postconditions]
	- Feedback is stored and linked to the interview, candidate, and panel member.
	- TA/Admin can review submitted feedback.
	- Audit fields are set.

### Module Name
- InterviewScheduleManagement
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`InterviewID` | Interview identifier | GUID | Must be valid and completed | Yes | None | "123e4567-e89b-12d3-a456-426614174000"
`CandidateName` | Candidate name | string | Display only | Yes | None | "John Doe"
`PanelMemberName` | Panel member name | string | Display only | Yes | None | "Jane Smith"
`InterviewDateTime` | Date and time of interview | datetime | Display only | Yes | None | "2025-11-26T10:00:00Z"
`Rating` | Overall rating | int | 1-5 stars | Yes | None | 4
`Decision` | Interview decision | string | Enum: Selected/Rejected/On Hold | Yes | None | "Selected"
`FeedbackComments` | Feedback comments | string | Min 10 chars | Yes | None | "Strong technical skills."
`Attachments` | Supporting files | file | Optional | No | None | "feedback.pdf"
`Source` | Application Source | string | Must be valid Application SourceID | Yes | None | "WebApp"
---

#### System-Level Business Rules
- FeedbackID is a system-generated GUID.
- CreatedDate and UpdatedDate must be set to current date and time.
- Only assigned panel members can submit feedback for their interviews.
- Feedback must be submitted before the review process can begin.
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
FEEDBACK_SUBMIT_SUCCESS | Success | Returns FeedbackID and success message | {"FeedbackID": "123e4567-e89b-12d3-a456-426614174001", "SuccessCode": "FEEDBACK_SUBMIT_SUCCESS", "SuccessMessage": "Feedback submitted successfully."} | No | Informational
FEEDBACK_SUBMIT_FAILURE | Failure | Returns error code and message | {"ErrorCode": "FEEDBACK_SUBMIT_FAILURE", "ErrorMessage": "Feedback submission failed."} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "ErrorMessage": "You are not authorized to perform this operation."} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "ErrorMessage": "Rating is required."} | Yes | Informational
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "ErrorMessage": "Feedback comments must be at least 10 characters."} | Yes | Informational
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "ErrorMessage": "Interview not found."} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "ErrorMessage": "Failed to submit feedback. Please try again later."} | Yes | Critical
---

### Security and Compliances
- [PII handling] Store only necessary PII. No plaintext sensitive data in logs.
- [Audit] Record creator, timestamp, source application, and key field changes.
- [Access Controls] Only assigned panel members can submit feedback for their interviews.

### Glossary
- [Feedback] Evaluation submitted by a panel member after an interview.
- [Panel Member] User assigned to conduct an interview.
- [Source] Originating application for the operation (e.g., WebApp, API, Admin).
