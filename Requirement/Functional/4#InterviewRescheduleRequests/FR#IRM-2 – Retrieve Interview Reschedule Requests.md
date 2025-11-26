## FR#IRM-2 – Retrieve Interview Reschedule Requests

### Description
System provides ability to retrieve and filter interview reschedule requests.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can view all reschedule requests across practices
- [TA Team Admin] Can view requests within assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - User has valid role with view permissions
    - Valid search/filter parameters provided

- [Postconditions]
    - Filtered list of requests returned
    - Total count included
    - Results filtered by permissions

### Module Name
- Interview Reschedule Request Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`pageNumber` | Page number | integer | Must be positive | Yes | 1 | 1
`pageSize` | Items per page | integer | Between 1 and 50 | Yes | 10 | 10
`startDate` | Filter start date | date | Valid date | No | None | "2025-11-10"
`endDate` | Filter end date | date | Valid date | No | None | "2025-11-17"
`requestStatus` | Status filter | integer | Valid status | No | None | 1
`interviewScheduleID` | Schedule filter | uuid | Must be valid | No | None | "12345678-1234-1234-1234-123456789012"
`sortBy` | Sort field | string | Valid field name | No | "modifiedDate" | "createdDate"
`sortDirection` | Sort direction | string | "asc" or "desc" | No | "desc" | "desc"
---

#### System-Level Business Rules
- Filter by role permissions
- Default sort by modified date
- Include only relevant requests
- Maximum page size enforced
- Date range validation
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
RESCHEDULE_REQUESTS_RETRIEVED | Success | Returns filtered requests | {"items": [...], "totalCount": 15, "pageNumber": 1} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid date range"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to view requests"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to retrieve requests"} | Yes | Critical

### Security and Compliances 
- [Access Control] Role-based filtering
- [Data Privacy] Limited data exposure
- [Audit] Log request access

### Glossary
- [Request Status] State of reschedule request
- [Date Range] Period for request filtering
- [Sort Order] Result ordering criteria