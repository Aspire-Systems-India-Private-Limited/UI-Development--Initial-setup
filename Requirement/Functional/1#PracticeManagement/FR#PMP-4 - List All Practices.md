## FR#PMP-4 – List All Practices

### Description
System should allow authorized users to retrieve a paginated list of all practices with filtering and sorting capabilities.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [Master Admin] Can view all practices with full details
- [Practice Admin] Can view list of all practices with limited details
- [Tech Team Panel Member] Can view list of all practices with limited details
- [TA Team Admin] Can view list of all practices with limited details

### Preconditions and Postconditions
- [Preconditions]
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Filtered and paginated practice list is returned
    - Access attempt is logged

### Module Name
- Practice Management

### Request Parameters
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`PageNumber` | Page number for pagination | integer | Must be > 0 | No | 1 | 1
`PageSize` | Items per page | integer | Must be > 0 and ≤ 100 | No | 10 | 20
`SearchTerm` | Search text | string | Max 50 characters | No | None | ".NET"
`SortBy` | Field to sort by | string | Must be valid field name | No | "PracticeName" | "Location"
`SortOrder` | Sort direction | string | "ASC" or "DESC" | No | "ASC" | "DESC"
`IsActive` | Filter by active status | boolean | true/false | No | None | true

### Response Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`Practices` | Array of practice items | array | [{"PracticeID": "guid", "PracticeName": ".NET", ...}]
`TotalCount` | Total number of practices | integer | 100
`PageNumber` | Current page number | integer | 1
`PageSize` | Items per page | integer | 20
`TotalPages` | Total number of pages | integer | 5

### Practice Item Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`PracticeID` | Unique identifier | guid | "12345678-1234-1234-1234-123456789012"
`PracticeName` | Name of the practice | string | ".NET"
`Location` | Primary location | string | "Chennai"
`IsActive` | Practice status | boolean | true
`ModifiedDate` | Last update timestamp | datetime | "2025-11-05T10:00:00Z"

### System-Level Business Rules
- Implement pagination to handle large datasets
- Sort by PracticeName by default
- Filter out inactive practices unless specifically requested
- Master Admin sees all fields, other roles see limited fields
- Cache results for improved performance
- Validate sort field names against allowed list
- Handle empty result sets appropriately

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
PRACTICE_LIST_SUCCESS | Success | Returns paginated practice list | {"Practices": [...], "TotalCount": 100, ...} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "Not authorized to list practices"} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "Message": "Invalid page size"} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "Message": "Invalid sort field"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve practices"} | Yes | Critical

### Security and Compliances
- [Access Control] Enforce role-based field visibility
- [Audit] Log access to practice list
- [Performance] Implement caching for frequent requests
- [Pagination] Prevent large data dumps
- [Data Privacy] Filter sensitive information based on role

### Glossary
- [Practice] An organizational unit representing a business division or department
- [Pagination] Division of large data sets into manageable pages
- [Sort Order] Direction of sorting (ascending or descending)
- [Search Term] Text to filter practices by name or location
- [Cache] Temporary storage of frequently accessed data