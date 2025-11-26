## FR#IRM-3 – Update Interview Reschedule Request

### Description
System allows modification of interview reschedule request details.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can update any reschedule request
- [TA Team Admin] Can update requests within assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Reschedule Request exists and is active
    - Request not yet approved/rejected
    - Valid update data provided
    - New schedule slot available

- [Postconditions]
    - Request details updated
    - Change history recorded
    - Notifications sent if needed

### Module Name
- Interview Reschedule Request Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`interviewRescheduleRequestID` | Request ID | uuid | Must exist | Yes | None | "12345678-1234-1234-1234-123456789012"
`newInterviewScheduleID` | New Schedule | uuid | Must be valid | Yes | None | "12345678-1234-1234-1234-123456789012"
`reason` | Reschedule reason | string | Must not be empty | Yes | None | "Updated panel availability"
`requestStatus` | Status | integer | Valid status | Yes | None | 1
`modUser` | Modified by | string | Current user | Yes | None | "user123"
---

#### System-Level Business Rules
- Cannot modify approved requests
- Validate new schedule availability
- Track request modifications
- Send notifications on status change
- Maintain change history
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
RESCHEDULE_REQUEST_UPDATE_SUCCESS | Success | Returns success message | {"message": "Reschedule request updated successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Cannot modify approved request"} | Yes | Error
NOT_FOUND_ERROR | Failure | Returns not found error | {"code": "NOT_FOUND_ERROR", "message": "Request not found"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to update request"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to update request"} | Yes | Critical

### Security and Compliances 
- [Status Control] Proper status transitions
- [Notifications] Status change alerts
- [Audit] Track all modifications

### Glossary
- [Request Status] Current state of request
- [New Schedule] Proposed interview time
- [Status Change] Request state transition