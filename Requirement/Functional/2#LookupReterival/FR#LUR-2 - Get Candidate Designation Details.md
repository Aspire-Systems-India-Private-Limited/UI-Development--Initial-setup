## FR#LUR-2 – Get Candidate Designation Details

### Description
System should allow authorized users to retrieve detailed information about specific candidate designations used for categorizing interview candidates.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [All Roles] Can view candidate designation details as these are essential reference data
- [Master Admin] Can view all designations including inactive ones
- [Other Roles] Can view only active designations

### Preconditions and Postconditions
- [Preconditions]
    - Candidate designation must exist in the system
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Designation details are returned if authorized
    - Access attempt is logged

### Module Name
- Lookup Data Management

### Fields level Business Rules
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`CandidateDesignationID` | Unique identifier | guid | Must be valid existing ID | Yes | None | "12345678-1234-1234-1234-123456789012"

### Response Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`CandidateDesignationID` | Unique identifier | guid | "12345678-1234-1234-1234-123456789012"
`Name` | System name | string | "FullStackSSE"
`DisplayName` | Display name | string | "Full Stack Senior Software Engineer"
`IsActive` | Status | boolean | true
`CreatedDate` | Creation timestamp | datetime | "2025-11-05T10:00:00Z"
`ModifiedDate` | Last update timestamp | datetime | "2025-11-05T10:00:00Z"
`ModUser` | Last updater's ID | string | "user123"
`Source` | Application source | integer | 1 (Web)

### System-Level Business Rules
- All roles can access designation data
- Return not found for non-existent designations
- Cache frequently accessed designation data
- Handle both active and inactive designations
- All fields from BaseEntity must be included in response
- Response must follow GetCandidateDesignationResponse schema

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
CANDIDATE_DESIGNATION_GET_SUCCESS | Success | Returns designation details | {"successCode": "CANDIDATE_DESIGNATION_GET_SUCCESS", "successMessage": "Candidate designation details retrieved successfully", "designation": {...}} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to view designation details"} | Yes | Error
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "Message": "Candidate designation not found"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve designation details"} | Yes | Critical

### Security and Compliances
- [Access Control] Basic authentication required
- [Audit] Log all access attempts
- [Caching] Implement efficient caching strategy
- [Performance] Optimize for frequent access
- [Logging] Record unauthorized access attempts

### User Stories

1. **View Designation Details**
   ```
   As an authorized user
   I want to retrieve candidate designation details
   So that I can understand the designation's scope and level
   ```

2. **Access Cached Data**
   ```
   As an authorized user
   I want quick access to designation information
   So that I can maintain system performance
   ```

3. **Handle Missing Designations**
   ```
   As an authorized user
   I want to receive clear feedback for non-existent designations
   So that I can report or fix invalid references
   ```

4. **View Audit Information**
   ```
   As a Master Admin
   I want to see designation audit information
   So that I can track changes to reference data
   ```

### Glossary
- [Candidate Designation] Job role or position level for candidates (e.g., Full Stack SSE, Front End SSE)
- [Display Name] User-friendly name shown in UI and reports
- [System Name] Internal identifier used by the application
- [Source] Origin of the data (Web, Mobile, API, etc.)
- [Audit Information] Creation and modification details of designations