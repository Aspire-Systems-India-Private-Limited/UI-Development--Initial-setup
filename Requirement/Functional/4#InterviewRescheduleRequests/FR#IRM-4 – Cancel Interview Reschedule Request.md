## FR#IRM-4 – Cancel Interview Reschedule Request

### Description
System allows cancellation of pending interview reschedule requests.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can cancel any reschedule request
- [TA Team Admin] Can cancel requests within assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Reschedule Request exists and is active
    - Request not yet approved/rejected
    - Valid cancellation reason provided

- [Postconditions]
    - Request marked as cancelled
    - Notifications sent
    - History updated
    - Original schedule maintained

### Module Name
- Interview Reschedule Request Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`interviewRescheduleRequestID` | Request ID | uuid | Must exist | Yes | None | "12345678-1234-1234-1234-123456789012"
`reason` | Cancellation reason | string | Must not be empty | Yes | None | "No longer needed"
`requestStatus` | New status | integer | Must be Cancelled | Yes | None | 5
`modUser` | Modified by | string | Current user | Yes | None | "user123"
`notes` | Additional notes | string | Optional | No | None | "Original schedule retained"
---

#### System-Level Business Rules
- Only pending requests can be cancelled
- Original schedule remains unchanged
- Notify relevant parties
- Record cancellation history
- Clear proposed time slot
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
RESCHEDULE_REQUEST_CANCEL_SUCCESS | Success | Returns success message | {"message": "Reschedule request cancelled successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Cannot cancel processed request"} | Yes | Error
NOT_FOUND_ERROR | Failure | Returns not found error | {"code": "NOT_FOUND_ERROR", "message": "Request not found"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to cancel request"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to cancel request"} | Yes | Critical

### Security and Compliances 
- [Status Management] Proper status handling
- [Notifications] Cancellation alerts
- [Audit] Track cancellations

### Glossary
- [Cancellation] Termination of request
- [Original Schedule] Initial interview timing
- [Pending Request] Unapproved request