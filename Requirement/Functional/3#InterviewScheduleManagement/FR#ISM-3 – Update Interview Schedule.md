## FR#ISM-3 – Update Interview Schedule

### Description
System allows modification of existing interview schedule details.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can update any interview schedule
- [TA Team Admin] Can update schedules within assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Interview Schedule exists and is active
    - No conflicts with new time slot
    - Valid update data provided
    - Panel member available

- [Postconditions]
    - Schedule details updated
    - Calendar invites updated
    - Notifications sent
    - Change history recorded

### Module Name
- Interview Schedule Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`interviewScheduleID` | Schedule ID | uuid | Must exist | Yes | None | "12345678-1234-1234-1234-123456789012"
`title` | Interview title | string | Must not be empty | Yes | None | "Technical Interview - Updated"
`notes` | Schedule notes | string | Optional | No | None | "Updated requirements discussion"
`technicalPanelMemberID` | Panel member | uuid | Must be valid and available | Yes | None | "12345678-1234-1234-1234-123456789012"
`interviewTypeID` | Interview type | uuid | Must be valid | Yes | None | "12345678-1234-1234-1234-123456789012"
`scheduledDate` | Interview date | date | Must be future date | Yes | None | "2025-11-15"
`scheduledTimeslotFrom` | Start time | time | Valid time | Yes | None | "10:00:00"
`scheduledTimeslotTo` | End time | time | After start time | Yes | None | "11:00:00"
`statusID` | Status | integer | Valid status | Yes | None | 1
`modUser` | Modified by | string | Current user | Yes | None | "user123"
---

#### System-Level Business Rules
- Validate time slot availability
- Update calendar invitations
- Notify affected parties
- Record schedule changes
- Check panel member availability
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
INTERVIEW_SCHEDULE_UPDATE_SUCCESS | Success | Returns success message | {"message": "Schedule updated successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid time slot"} | Yes | Error
CONFLICT_ERROR | Failure | Returns conflict error | {"code": "CONFLICT_ERROR", "message": "Panel member unavailable"} | Yes | Error
NOT_FOUND_ERROR | Failure | Returns not found error | {"code": "NOT_FOUND_ERROR", "message": "Schedule not found"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to update schedule"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to update schedule"} | Yes | Critical

### Security and Compliances 
- [Calendar Integration] Secure calendar updates
- [Notifications] Proper notification handling
- [Audit] Track all modifications

### Glossary
- [Time Slot] Interview time period
- [Calendar Invite] Meeting invitation
- [Panel Availability] Interviewer's free time