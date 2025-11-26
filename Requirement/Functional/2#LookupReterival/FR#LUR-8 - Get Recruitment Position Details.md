## FR#LUR-8 – Get Recruitment Position Details

### Description
System should allow authorized users to retrieve detailed information about recruitment positions used for categorizing job roles in the interview process.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [All Roles] Can view recruitment position details as these are essential reference data
- [Master Admin] Can view all positions including inactive ones
- [Other Roles] Can view only active positions

### Preconditions and Postconditions
- [Preconditions]
    - Recruitment position must exist in the system
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Recruitment position details are returned if authorized
    - Access attempt is logged

### Module Name
- Lookup Data Management

### Fields level Business Rules
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`RecruitmentPositionID` | Unique identifier | guid | Must be valid existing ID | Yes | None | "12345678-1234-1234-1234-123456789012"

### Response Fields
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
- All roles can access recruitment position data
- Return not found for non-existent positions
- Cache frequently accessed position data
- Handle both active and inactive positions
- All fields from BaseEntity must be included in response
- Response must follow GetRecruitmentPositionResponse schema

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
RECRUITMENT_POSITION_GET_SUCCESS | Success | Returns position details | {"successCode": "RECRUITMENT_POSITION_GET_SUCCESS", "successMessage": "Recruitment position details retrieved successfully", "position": {...}} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to view recruitment position details"} | Yes | Error
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "Message": "Recruitment position not found"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve recruitment position details"} | Yes | Critical

### Security and Compliances
- [Access Control] Basic authentication required
- [Audit] Log all access attempts
- [Caching] Implement efficient caching strategy
- [Performance] Optimize for frequent access
- [Logging] Record unauthorized access attempts

### User Stories

1. **View Recruitment Position Details**
   ```
   As an authorized user
   I want to retrieve recruitment position details
   So that I can understand and categorize job roles
   ```

2. **Access Cached Data**
   ```
   As an authorized user
   I want quick access to recruitment position information
   So that I can maintain system performance
   ```

3. **Handle Missing Positions**
   ```
   As an authorized user
   I want to receive clear feedback for non-existent recruitment positions
   So that I can report or fix invalid references
   ```

4. **View Audit Information**
   ```
   As a Master Admin
   I want to see recruitment position audit information
   So that I can track changes to reference data
   ```

### Glossary
- [Recruitment Position] Job role or position being recruited for (e.g., Software Engineer, Senior Developer, Technical Lead)
- [Display Name] User-friendly name shown in UI and reports
- [System Name] Internal identifier used by the application
- [Source] Origin of the data (Web, Mobile, API, etc.)
- [Audit Information] Creation and modification details of recruitment positions