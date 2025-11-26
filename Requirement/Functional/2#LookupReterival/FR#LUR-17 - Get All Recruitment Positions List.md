## FR#LUR-17 – Get All Recruitment Positions List

### Description
System should allow authorized users to retrieve a paginated list of all recruitment positions with filtering options for active/inactive status.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [All Roles] Can view list of recruitment positions
- [Master Admin] Can view both active and inactive positions
- [Other Roles] Can view only active positions

### Preconditions and Postconditions
- [Preconditions]
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Filtered list of recruitment positions is returned
    - Access attempt is logged

### Module Name
- Lookup Data Management

### Request Parameters
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`PageNumber` | Page number for pagination | integer | Must be > 0 | No | 1 | 1
`PageSize` | Items per page | integer | Must be > 0 and ≤ 100 | No | 20 | 20
`IsActive` | Filter by active status | boolean | None | No | true | true
`SearchTerm` | Search by name | string | Max length 50 | No | null | "Engineer"

### Response Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`Items` | Array of recruitment positions | array | [{ ... }]
`TotalCount` | Total number of matching records | integer | 50
`PageNumber` | Current page number | integer | 1
`PageSize` | Items per page | integer | 20
`TotalPages` | Total number of pages | integer | 3
`HasNextPage` | More pages available | boolean | true
`HasPreviousPage` | Previous pages available | boolean | false

### Item Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`RecruitmentPositionID` | Unique identifier | guid | "12345678-1234-1234-1234-123456789012"
`Name` | System name | string | "SoftwareEngineer"
`DisplayName` | Display name | string | "Software Engineer"
`IsActive` | Status | boolean | true
`CreatedDate` | Creation timestamp | datetime | "2025-11-05T10:00:00Z"
`ModifiedDate` | Last update timestamp | datetime | "2025-11-05T10:00:00Z"
`ModUser` | Last updater's ID | string | "user123"
`Source` | Application source | integer | 1 (Web)

### System-Level Business Rules
- Return empty list if no positions match filters
- Implement server-side pagination
- Cache frequently accessed lists
- Sort by DisplayName by default
- Filter inactive items for non-admin users
- All fields from BaseEntity must be included in response
- Response must follow GetRecruitmentPositionListResponse schema

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
RECRUITMENT_POSITION_LIST_SUCCESS | Success | Returns paginated list | {"successCode": "RECRUITMENT_POSITION_LIST_SUCCESS", "successMessage": "Recruitment positions retrieved successfully", "data": {...}} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to view recruitment positions"} | Yes | Error
INVALID_PARAMETERS | Failure | Returns validation errors | {"ErrorCode": "INVALID_PARAMETERS", "Message": "Invalid page number"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve recruitment positions"} | Yes | Critical

### Security and Compliances
- [Access Control] Basic authentication required
- [Audit] Log all access attempts
- [Caching] Cache list results for 5 minutes
- [Performance] Implement efficient pagination
- [Rate Limiting] Apply standard API rate limits

### User Stories

1. **View All Recruitment Positions**
   ```
   As an authorized user
   I want to retrieve a list of recruitment positions
   So that I can view and select from available options
   ```

2. **Filter Active Positions**
   ```
   As a regular user
   I want to see only active recruitment positions
   So that I can make valid selections
   ```

3. **Search Positions**
   ```
   As an authorized user
   I want to search recruitment positions by name
   So that I can quickly find specific positions
   ```

4. **Navigate Pages**
   ```
   As an authorized user
   I want to navigate through pages of recruitment positions
   So that I can view all available options
   ```

### Glossary
- [Recruitment Position] Job role or position being recruited for (e.g., Software Engineer, Tech Lead)
- [Pagination] Division of results into pages for efficient data retrieval
- [Search Term] Text to filter positions by name
- [Active Status] Whether a recruitment position is currently in use