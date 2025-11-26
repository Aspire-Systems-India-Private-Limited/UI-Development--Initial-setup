## FR#LUR-1 – Get Opportunity Category Details

### Description
System should allow authorized users to retrieve detailed information about specific opportunity categories used for categorizing hiring opportunities.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [All Roles] Can view opportunity category details as these are essential reference data
- [Master Admin] Can view all categories including inactive ones
- [Other Roles] Can view only active categories

### Preconditions and Postconditions
- [Preconditions]
    - Opportunity category must exist in the system
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Category details are returned if authorized
    - Access attempt is logged

### Module Name
- Lookup Data Management

### Fields level Business Rules
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`OpportunityCategoryID` | Unique identifier | guid | Must be valid existing ID | Yes | None | "12345678-1234-1234-1234-123456789012"

### Response Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`OpportunityCategoryID` | Unique identifier | guid | "12345678-1234-1234-1234-123456789012"
`Name` | System name | string | "Forecast"
`DisplayName` | Display name | string | "Forecast Hiring"
`IsActive` | Status | boolean | true
`CreatedDate` | Creation timestamp | datetime | "2025-11-05T10:00:00Z"
`ModifiedDate` | Last update timestamp | datetime | "2025-11-05T10:00:00Z"
`ModUser` | Last updater's ID | string | "user123"
`Source` | Application source | integer | 1 (Web)

### System-Level Business Rules
- All roles can access opportunity category data
- Return not found for non-existent categories
- Cache frequently accessed category data
- Handle both active and inactive categories
- All fields from BaseEntity must be included in response
- Response must follow GetOpportunityCategoryResponse schema

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
OPPORTUNITY_CATEGORY_GET_SUCCESS | Success | Returns category details | {"successCode": "OPPORTUNITY_CATEGORY_GET_SUCCESS", "successMessage": "Opportunity category details retrieved successfully", "category": {...}} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to view category details"} | Yes | Error
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "Message": "Opportunity category not found"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve category details"} | Yes | Critical

### Security and Compliances
- [Access Control] Basic authentication required
- [Audit] Log all access attempts
- [Caching] Implement efficient caching strategy
- [Performance] Optimize for frequent access
- [Logging] Record unauthorized access attempts

### User Stories

1. **View Category Details**
   ```
   As an authorized user
   I want to retrieve opportunity category details
   So that I can understand the category's purpose and usage
   ```

2. **Access Cached Data**
   ```
   As an authorized user
   I want quick access to category information
   So that I can maintain system performance
   ```

3. **Handle Missing Categories**
   ```
   As an authorized user
   I want to receive clear feedback for non-existent categories
   So that I can report or fix invalid references
   ```

4. **View Audit Information**
   ```
   As a Master Admin
   I want to see category audit information
   So that I can track changes to reference data
   ```

### Glossary
- [Opportunity Category] Classification of hiring opportunities (e.g., Forecast, On-demand, Client Request)
- [Display Name] User-friendly name shown in UI and reports
- [System Name] Internal identifier used by the application
- [Source] Origin of the data (Web, Mobile, API, etc.)
- [Audit Information] Creation and modification details of categories