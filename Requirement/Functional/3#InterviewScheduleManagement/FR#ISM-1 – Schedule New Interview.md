## FR#ISM-1 – Schedule New Interview by TA Team Admin

### Description
System allows scheduling of interviews for candidates with technical panel members.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can schedule interviews across all practices
- [TA Team Admin] Can schedule interviews within assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Valid Candidate Profile exists
    - Technical Panel Member is available
    - Interview slot is available
    - Hiring Opportunity is active

- [Postconditions]
    - Interview Schedule is created
    - Calendar invites are sent
    - Audit fields are set
    - InterviewScheduleID is returned

### Module Name
- Interview Schedule Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`title` | Interview Title | string | Must not be empty | Yes | None | "Technical Interview - John Doe"
`notes` | Interview Notes | string | Optional | No | None | "Please review candidate's project experience"
`technicalPanelMemberID` | Technical Panel Member | uuid | Must be valid and available member | Yes | None | "12345678-1234-1234-1234-123456789012"
`candidateProfileID` | Candidate Profile | uuid | Must be valid profile | Yes | None | "12345678-1234-1234-1234-123456789012"
`hiringOpportunityID` | Hiring Opportunity | uuid | Must be valid opportunity | Yes | None | "12345678-1234-1234-1234-123456789012"
`interviewTypeID` | Interview Type | uuid | Must be valid type (Weekday/Weekend/Walkin) | Yes | None | "12345678-1234-1234-1234-123456789012"
`availabilityID` | Availability Slot | uuid | Must be valid and open slot | Yes | None | "12345678-1234-1234-1234-123456789012"
`scheduledDate` | Interview Date | date | Must be future date | Yes | None | "2025-11-15"
`scheduledTimeslotFrom` | Start Time | time | Must be valid time | Yes | None | "10:00:00"
`scheduledTimeslotTo` | End Time | time | Must be after start time | Yes | None | "11:00:00"
`statusID` | Schedule Status | integer | Must be valid status | Yes | None | 1
`isActive` | Is active | boolean | Must be true for new schedules | Yes | true | true
`modUser` | Modified by | string | Must be current user ID | Yes | None | "user123"
`source` | Application Source | integer | Must be valid source | Yes | None | 1
---

#### System-Level Business Rules
- `interviewScheduleID` is system-generated UUID
- Time slot must be available for panel member
- No overlapping interviews for same panel member
- Calendar invites must be sent to all participants
- Status transitions must follow defined workflow
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
INTERVIEW_SCHEDULE_CREATE_SUCCESS | Success | Returns InterviewScheduleID and message | {"interviewScheduleID": "12345678-1234-1234-1234-123456789012", "message": "Interview scheduled successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid interview time slot"} | Yes | Error
CONFLICT_ERROR | Failure | Returns conflict error | {"code": "CONFLICT_ERROR", "message": "Panel member not available"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to schedule interviews"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to schedule interview"} | Yes | Critical

### Security and Compliances 
- [Calendar Integration] Secure calendar invite handling
- [Notification] Proper notification to all participants
- [Audit] Track all schedule changes and notifications

### Glossary
- [Interview Schedule] Record of planned interview with details
- [Technical Panel Member] Interviewer conducting technical evaluation
- [Interview Type] Category of interview (Weekday/Weekend/Walkin)
- [Availability] Time slot when panel member is available