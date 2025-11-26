## FR#HOP-2 – Retrieve Hiring Opportunities with Pagination

### Description
System provides ability to retrieve hiring opportunities with pagination support.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can view all hiring opportunities across practices
- [TA Team Admin] Can view opportunities for their assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - User has valid role with view permissions
    - Valid pagination parameters provided

- [Postconditions]
    - Paginated list of hiring opportunities returned
    - Total count of records included
    - Filtered by practice for relevant roles

### Module Name
- Hiring Opportunity Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`pageNumber` | Page number | integer | Must be positive number | Yes | 1 | 1
`pageSize` | Items per page | integer | Must be between 1 and 50 | Yes | 10 | 10
`sortBy` | Sort field | string | Must be valid field name | No | "modifiedDate" | "title"
`sortDirection` | Sort direction | string | Must be "asc" or "desc" | No | "desc" | "asc"
`practiceID` | Filter by practice | uuid | Must be valid practice | No | None | "12345678-1234-1234-1234-123456789012"
`statusID` | Filter by status | integer | Must be valid status | No | None | 1

---

#### System-Level Business Rules
- Default sorting by modified date descending
- Inactive records not included by default
- Practice-specific filtering applied automatically based on user role
- Maximum page size enforced
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
HIRING_OPPORTUNITIES_RETRIEVED | Success | Returns paginated opportunities | {"items": [...], "totalCount": 100, "pageNumber": 1, "pageSize": 10} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid page number"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to view opportunities"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to retrieve opportunities"} | Yes | Critical

### Security and Compliances 
- [Access Control] Practice-specific data access
- [Pagination] Prevent excessive data retrieval
- [Audit] Log access to sensitive data

### Glossary
- [Pagination] Division of results into pages
- [Sort Direction] Order of results (ascending/descending)
- [Filter] Criteria to narrow down results