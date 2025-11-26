## FR#ISM-2 – Retrieve Interview Schedules

### Description
System provides ability to retrieve and filter interview schedules.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can view all interview schedules across practices
- [TA Team Admin] Can view schedules within assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - User has valid role with view permissions
    - Valid search/filter parameters provided

- [Postconditions]
    - Filtered list of schedules returned
    - Total count included
    - Results filtered by permissions

### Module Name
- Interview Schedule Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`pageNumber` | Page number | integer | Must be positive | Yes | 1 | 1
`pageSize` | Items per page | integer | Between 1 and 50 | Yes | 10 | 10
`startDate` | Filter start date | date | Valid date | No | None | "2025-11-10"
`endDate` | Filter end date | date | Valid date | No | None | "2025-11-17"
`technicalPanelMemberID` | Panel member filter | uuid | Must be valid | No | None | "12345678-1234-1234-1234-123456789012"
`hiringOpportunityID` | Opportunity filter | uuid | Must be valid | No | None | "12345678-1234-1234-1234-123456789012"
`interviewTypeID` | Type filter | uuid | Must be valid | No | None | "12345678-1234-1234-1234-123456789012"
`statusID` | Status filter | integer | Must be valid | No | None | 1
`sortBy` | Sort field | string | Valid field name | No | "scheduledDate" | "title"
`sortDirection` | Sort direction | string | "asc" or "desc" | No | "asc" | "desc"
---

#### System-Level Business Rules
- Filter by role permissions
- Default sort by scheduled date
- Include only relevant schedules
- Maximum page size enforced
- Date range validation
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
INTERVIEW_SCHEDULES_RETRIEVED | Success | Returns filtered schedules | {"items": [...], "totalCount": 25, "pageNumber": 1} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid date range"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to view schedules"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to retrieve schedules"} | Yes | Critical

### Security and Compliances 
- [Access Control] Role-based filtering
- [Data Privacy] Limited data exposure
- [Audit] Log schedule access

### Glossary
- [Date Range] Period for schedule filtering
- [Interview Type] Category of interview
- [Panel Member] Technical interviewer