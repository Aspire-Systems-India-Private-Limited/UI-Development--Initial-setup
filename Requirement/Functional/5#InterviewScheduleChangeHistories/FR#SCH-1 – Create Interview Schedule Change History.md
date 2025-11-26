## FR#SCH-1 – Create Interview Schedule Change History

### Description
System maintains a history of all interview schedule changes for audit and tracking purposes.

### User Roles
- Master Admin
- TA Team Admin
- System (Automated)
---
### Personas and Permissions
- [Master Admin] Can trigger history record creation for any schedule
- [TA Team Admin] Can trigger history record creation within assigned practices
- [System] Automatically creates history records for all schedule changes

---
### Preconditions and Postconditions
- [Preconditions]
    - Interview Schedule change occurs
    - Valid reschedule request exists
    - All required information available

- [Postconditions]
    - Change History record created
    - Audit fields are set
    - RescheduleHistoryID returned

### Module Name
- Interview Schedule Change History Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`interviewScheduleID` | Changed Schedule | uuid | Must be valid schedule | Yes | None | "12345678-1234-1234-1234-123456789012"
`previousInterviewScheduleID` | Previous Schedule | uuid | Must be valid schedule | Yes | None | "12345678-1234-1234-1234-123456789012"
`newInterviewScheduleID` | New Schedule | uuid | Must be valid schedule | Yes | None | "12345678-1234-1234-1234-123456789012"
`interviewRescheduleRequestID` | Reschedule Request | uuid | Must be valid request | Yes | None | "12345678-1234-1234-1234-123456789012"
`interviewScheduleType` | Schedule Type | integer | Must be valid type (New/Reschedule) | Yes | None | 1
`reason` | Change Reason | string | Must not be empty | Yes | None | "Panel member unavailable"
`requestStatus` | Request Status | integer | Must be valid status | Yes | None | 1
`isActive` | Is active | boolean | Must be true for new records | Yes | true | true
`modUser` | Modified by | string | Must be current user ID | Yes | None | "user123"
`source` | Application Source | integer | Must be valid source | Yes | None | 1
---

#### System-Level Business Rules
- `rescheduleHistoryID` is system-generated UUID
- History record created for every schedule change
- Complete change details must be captured
- Linked to original reschedule request
- Track both successful and failed changes
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
CHANGE_HISTORY_CREATE_SUCCESS | Success | Returns HistoryID and message | {"historyID": "12345678-1234-1234-1234-123456789012", "message": "Change history recorded successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid schedule reference"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to record change history"} | Yes | Critical

### Security and Compliances 
- [Audit Trail] Complete history of all changes
- [Data Integrity] No modification of history records
- [Retention] Meet data retention requirements

### Glossary
- [Schedule Change History] Record of interview schedule modifications
- [Schedule Type] Whether new schedule or reschedule
- [Previous Schedule] Original schedule before change
- [New Schedule] Modified schedule after change