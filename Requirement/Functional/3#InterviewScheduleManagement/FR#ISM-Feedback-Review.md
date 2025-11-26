# FR#ISM-Feedback-Review – Review Interview Feedback

## FR#ISM-Feedback-Review – Review Interview Feedback

### Description
TA/Admin users review feedback submitted by panel members for completed interviews. This process is used for hiring decisions, audit, and compliance.

### User Roles
- TA/Admin (review feedback)
- Panel Member (view own feedback)

---
### Preconditions and Postconditions
- [Preconditions]
	- Feedback must be submitted by a panel member for a completed interview.
	- Reviewer must have appropriate permissions.
- [Postconditions]
	- Feedback is marked as reviewed.
	- Feedback is available for audit and reporting.
	- Audit fields are set.

### Module Name
- InterviewScheduleManagement
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`CandidateName` | Candidate name | string | Display only | Yes | None | "John Doe"
`PanelMemberName` | Panel member name | string | Display only | Yes | None | "Jane Smith"
`InterviewDateTime` | Date and time of interview | datetime | Display only | Yes | None | "2025-11-26T10:00:00Z"
`Rating` | Overall rating | int | 1-5 stars | Yes | None | 4
`Decision` | Interview decision | string | Enum: Selected/Rejected/On Hold | Yes | None | "Selected"
`FeedbackComments` | Feedback comments | string | Min 10 chars | Yes | None | "Strong technical skills."
`Attachments` | Supporting files | file | Optional | No | None | "feedback.pdf"
`Status` | Review status | string | Enum: Reviewed/Not Reviewed | Yes | "Not Reviewed" | "Reviewed"
`Source` | Application Source | string | Must be valid Application SourceID | Yes | None | "WebApp"
---

#### System-Level Business Rules
- Only authorized users can mark feedback as reviewed.
- All review actions are logged with user, timestamp, and source.
- Feedback review status must be updated atomically.
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
FEEDBACK_REVIEW_SUCCESS | Success | Returns FeedbackID and success message | {"FeedbackID": "123e4567-e89b-12d3-a456-426614174001", "SuccessCode": "FEEDBACK_REVIEW_SUCCESS", "SuccessMessage": "Feedback marked as reviewed."} | No | Informational
FEEDBACK_REVIEW_FAILURE | Failure | Returns error code and message | {"ErrorCode": "FEEDBACK_REVIEW_FAILURE", "ErrorMessage": "Feedback review failed."} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "ErrorMessage": "You are not authorized to perform this operation."} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "ErrorMessage": "Status is required."} | Yes | Informational
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "ErrorMessage": "Feedback not found."} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "ErrorMessage": "Failed to review feedback. Please try again later."} | Yes | Critical
---

### Security and Compliances
- [PII handling] Store only necessary PII. No plaintext sensitive data in logs.
- [Audit] Record reviewer, timestamp, source application, and key field changes.
- [Access Controls] Only authorized users can review and mark feedback as reviewed.

### Glossary
- [Feedback] Evaluation submitted by a panel member after an interview.
- [Panel Member] User assigned to conduct an interview.
- [Source] Originating application for the operation (e.g., WebApp, API, Admin).
