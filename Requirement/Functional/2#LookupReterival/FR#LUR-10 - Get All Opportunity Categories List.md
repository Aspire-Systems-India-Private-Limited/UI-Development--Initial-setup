## FR#LUR-10 – Get All Opportunity Categories List

### Description
System should allow authorized users to retrieve a paginated list of all opportunity categories with filtering options for active/inactive status.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [All Roles] Can view list of opportunity categories
- [Master Admin] Can view both active and inactive categories
- [Other Roles] Can view only active categories

### Preconditions and Postconditions
- [Preconditions]
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Filtered list of opportunity categories is returned
    - Access attempt is logged

### Module Name
- Lookup Data Management

### Request Parameters
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`PageNumber` | Page number for pagination | integer | Must be > 0 | No | 1 | 1
`PageSize` | Items per page | integer | Must be > 0 and ≤ 100 | No | 20 | 20
`IsActive` | Filter by active status | boolean | None | No | true | true
`SearchTerm` | Search by name | string | Max length 50 | No | null | "Developer"

### Response Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`Items` | Array of opportunity categories | array | [{ ... }]
`TotalCount` | Total number of matching records | integer | 50
`PageNumber` | Current page number | integer | 1
`PageSize` | Items per page | integer | 20
`TotalPages` | Total number of pages | integer | 3
`HasNextPage` | More pages available | boolean | true
`HasPreviousPage` | Previous pages available | boolean | false

### Item Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`OpportunityCategoryID` | Unique identifier | guid | "12345678-1234-1234-1234-123456789012"
`Name` | System name | string | "DotNetDeveloper"
`DisplayName` | Display name | string | ".NET Developer"
`IsActive` | Status | boolean | true
`CreatedDate` | Creation timestamp | datetime | "2025-11-05T10:00:00Z"
`ModifiedDate` | Last update timestamp | datetime | "2025-11-05T10:00:00Z"
`ModUser` | Last updater's ID | string | "user123"
`Source` | Application source | integer | 1 (Web)

### System-Level Business Rules
- Return empty list if no categories match filters
- Implement server-side pagination
- Cache frequently accessed lists
- Sort by DisplayName by default
- Filter inactive items for non-admin users
- All fields from BaseEntity must be included in response
- Response must follow GetOpportunityCategoryListResponse schema

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
OPPORTUNITY_CATEGORY_LIST_SUCCESS | Success | Returns paginated list | {"successCode": "OPPORTUNITY_CATEGORY_LIST_SUCCESS", "successMessage": "Opportunity categories retrieved successfully", "data": {...}} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to view opportunity categories"} | Yes | Error
INVALID_PARAMETERS | Failure | Returns validation errors | {"ErrorCode": "INVALID_PARAMETERS", "Message": "Invalid page number"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve opportunity categories"} | Yes | Critical

### Security and Compliances
- [Access Control] Basic authentication required
- [Audit] Log all access attempts
- [Caching] Cache list results for 5 minutes
- [Performance] Implement efficient pagination
- [Rate Limiting] Apply standard API rate limits

### User Stories

1. **View All Categories**
   ```
   As an authorized user
   I want to retrieve a list of opportunity categories
   So that I can view and select from available options
   ```

2. **Filter Active Categories**
   ```
   As a regular user
   I want to see only active opportunity categories
   So that I can make valid selections
   ```

3. **Search Categories**
   ```
   As an authorized user
   I want to search opportunity categories by name
   So that I can quickly find specific categories
   ```

4. **Navigate Pages**
   ```
   As an authorized user
   I want to navigate through pages of categories
   So that I can view all available options
   ```

### Glossary
- [Opportunity Category] Classification of job opportunities (e.g., .NET Developer, Java Developer)
- [Pagination] Division of results into pages for efficient data retrieval
- [Search Term] Text to filter categories by name
- [Active Status] Whether a category is currently in use