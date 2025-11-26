## FR#LUR-13 – Get All Schedule Types List

### Description
System should allow authorized users to retrieve a paginated list of all schedule types with filtering options for active/inactive status.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [All Roles] Can view list of schedule types
- [Master Admin] Can view both active and inactive types
- [Other Roles] Can view only active types

### Preconditions and Postconditions
- [Preconditions]
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Filtered list of schedule types is returned
    - Access attempt is logged

### Module Name
- Lookup Data Management

### Request Parameters
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`PageNumber` | Page number for pagination | integer | Must be > 0 | No | 1 | 1
`PageSize` | Items per page | integer | Must be > 0 and ≤ 100 | No | 20 | 20
`IsActive` | Filter by active status | boolean | None | No | true | true
`SearchTerm` | Search by name | string | Max length 50 | No | null | "WeekDay"

### Response Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`Items` | Array of schedule types | array | [{ ... }]
`TotalCount` | Total number of matching records | integer | 50
`PageNumber` | Current page number | integer | 1
`PageSize` | Items per page | integer | 20
`TotalPages` | Total number of pages | integer | 3
`HasNextPage` | More pages available | boolean | true
`HasPreviousPage` | Previous pages available | boolean | false

### Item Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`ScheduleTypeID` | Unique identifier | guid | "12345678-1234-1234-1234-123456789012"
`Name` | System name | string | "WeekDaySchedule"
`DisplayName` | Display name | string | "Weekday Schedule"
`IsActive` | Status | boolean | true
`CreatedDate` | Creation timestamp | datetime | "2025-11-05T10:00:00Z"
`ModifiedDate` | Last update timestamp | datetime | "2025-11-05T10:00:00Z"
`ModUser` | Last updater's ID | string | "user123"
`Source` | Application source | integer | 1 (Web)

### System-Level Business Rules
- Return empty list if no types match filters
- Implement server-side pagination
- Cache frequently accessed lists
- Sort by DisplayName by default
- Filter inactive items for non-admin users
- All fields from BaseEntity must be included in response
- Response must follow GetScheduleTypeListResponse schema

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
SCHEDULE_TYPE_LIST_SUCCESS | Success | Returns paginated list | {"successCode": "SCHEDULE_TYPE_LIST_SUCCESS", "successMessage": "Schedule types retrieved successfully", "data": {...}} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to view schedule types"} | Yes | Error
INVALID_PARAMETERS | Failure | Returns validation errors | {"ErrorCode": "INVALID_PARAMETERS", "Message": "Invalid page number"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve schedule types"} | Yes | Critical

### Security and Compliances
- [Access Control] Basic authentication required
- [Audit] Log all access attempts
- [Caching] Cache list results for 5 minutes
- [Performance] Implement efficient pagination
- [Rate Limiting] Apply standard API rate limits

### User Stories

1. **View All Schedule Types**
   ```
   As an authorized user
   I want to retrieve a list of schedule types
   So that I can view and select from available options
   ```

2. **Filter Active Types**
   ```
   As a regular user
   I want to see only active schedule types
   So that I can make valid selections
   ```

3. **Search Types**
   ```
   As an authorized user
   I want to search schedule types by name
   So that I can quickly find specific types
   ```

4. **Navigate Pages**
   ```
   As an authorized user
   I want to navigate through pages of schedule types
   So that I can view all available options
   ```

### Glossary
- [Schedule Type] Format of scheduling (e.g., WeekDay, Weekend, Holiday)
- [Pagination] Division of results into pages for efficient data retrieval
- [Search Term] Text to filter types by name
- [Active Status] Whether a schedule type is currently in use