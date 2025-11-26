## FR#IRM-1 – Create Interview Reschedule Request by TA Team Admin

### Description
System allows creation of interview reschedule requests when changes are needed to existing schedules.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can create reschedule requests for any interview
- [TA Team Admin] Can create reschedule requests within assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Original Interview Schedule exists
    - Valid reason for rescheduling
    - New time slot is available
    - All required participants available

- [Postconditions]
    - Reschedule Request is created
    - Notification sent to approver
    - Audit fields are set
    - InterviewRescheduleRequestID returned

### Module Name
- Interview Reschedule Request Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`interviewScheduleID` | Original Schedule | uuid | Must be valid schedule | Yes | None | "12345678-1234-1234-1234-123456789012"
`previousInterviewScheduleID` | Previous Schedule | uuid | Must be valid schedule | Yes | None | "12345678-1234-1234-1234-123456789012"
`newInterviewScheduleID` | New Schedule | uuid | Must be valid schedule | Yes | None | "12345678-1234-1234-1234-123456789012"
`reason` | Reschedule Reason | string | Must not be empty | Yes | None | "Panel member unavailable"
`requestStatus` | Request Status | integer | Must be valid status | Yes | 1 | 1
`isActive` | Is active | boolean | Must be true for new requests | Yes | true | true
`modUser` | Modified by | string | Must be current user ID | Yes | None | "user123"
`source` | Application Source | integer | Must be valid source | Yes | None | 1
---

#### System-Level Business Rules
- `interviewRescheduleRequestID` is system-generated UUID
- Original schedule must be in valid state for rescheduling
- New schedule must not conflict with existing schedules
- Request must be approved before taking effect
- Notifications must be sent to all affected parties
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
RESCHEDULE_REQUEST_CREATE_SUCCESS | Success | Returns RescheduleRequestID and message | {"rescheduleRequestID": "12345678-1234-1234-1234-123456789012", "message": "Reschedule request created successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid reschedule reason"} | Yes | Error
CONFLICT_ERROR | Failure | Returns conflict error | {"code": "CONFLICT_ERROR", "message": "New schedule conflicts with existing interview"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to create reschedule requests"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to create reschedule request"} | Yes | Critical

### Security and Compliances 
- [Workflow] Proper approval process must be followed
- [Notification] All affected parties must be notified
- [Audit] Track all request states and approvals

### Glossary
- [Reschedule Request] Formal request to change interview schedule
- [Previous Schedule] Original interview schedule being changed
- [New Schedule] Proposed new interview schedule
- [Request Status] Current state of the reschedule request