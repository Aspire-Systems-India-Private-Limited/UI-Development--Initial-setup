## FR#ISM-4 – Cancel Interview Schedule

### Description
System allows cancellation of scheduled interviews when needed.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can cancel any interview schedule
- [TA Team Admin] Can cancel schedules within assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Interview Schedule exists and is active
    - Valid cancellation reason provided
    - Schedule is not already completed

- [Postconditions]
    - Schedule marked as cancelled
    - Calendar invites cancelled
    - Notifications sent
    - Cancellation history recorded

### Module Name
- Interview Schedule Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`interviewScheduleID` | Schedule ID | uuid | Must exist | Yes | None | "12345678-1234-1234-1234-123456789012"
`reason` | Cancellation reason | string | Must not be empty | Yes | None | "Candidate unavailable"
`notes` | Additional notes | string | Optional | No | None | "Candidate found another opportunity"
`statusID` | New status | integer | Must be Cancelled (5) | Yes | None | 5
`modUser` | Modified by | string | Current user | Yes | None | "user123"
---

#### System-Level Business Rules
- Only future schedules can be cancelled
- Cancel calendar invitations
- Notify all participants
- Record cancellation history
- Free up panel member time slot
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
INTERVIEW_SCHEDULE_CANCEL_SUCCESS | Success | Returns success message | {"message": "Interview cancelled successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Cannot cancel past interview"} | Yes | Error
NOT_FOUND_ERROR | Failure | Returns not found error | {"code": "NOT_FOUND_ERROR", "message": "Schedule not found"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to cancel schedule"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to cancel schedule"} | Yes | Critical

### Security and Compliances 
- [Calendar Integration] Proper cancellation
- [Notifications] Timely alerts to all parties
- [Audit] Track cancellation details

### Glossary
- [Cancellation] Termination of scheduled interview
- [Calendar Cleanup] Remove calendar entries
- [Time Slot Release] Free up reserved time