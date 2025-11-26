## FR#PMP-3 – Get Practice Details

### Description
System should allow authorized users to retrieve detailed information about a specific practice.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [Master Admin] Can view details of any practice
- [Practice Admin] Can view details of their assigned practice only
- [Tech Team Panel Member] Can view details of their assigned practice only
- [TA Team Admin] Can view details of their assigned practice only

### Preconditions and Postconditions
- [Preconditions]
    - Practice must exist in the system
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Practice details are returned if authorized
    - Access attempt is logged

### Module Name
- Practice Management

### Fields level Business Rules
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`PracticeID` | Unique identifier | guid | Must be valid existing PracticeID | Yes | None | "12345678-1234-1234-1234-123456789012"

### Response Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`PracticeID` | Unique identifier | guid | "12345678-1234-1234-1234-123456789012"
`PracticeName` | Name of the practice | string | ".NET"
`Description` | Description of the practice | string | "Microsoft .NET Development Practice"
`Location` | Primary location of practice | string | "Chennai"
`IsActive` | Practice status | boolean | true
`CreatedDate` | Creation timestamp | datetime | "2025-11-05T10:00:00Z"
`ModifiedDate` | Last update timestamp | datetime | "2025-11-05T10:00:00Z"
`ModUser` | Last updater's ID | string | "user123"
`Source` | Application source | string | "WebApp"

### System-Level Business Rules
- Master Admin can view any practice
- Other roles can only view their assigned practice
- Must handle both active and inactive practices
- Return not found for non-existent practices
- Return forbidden for unauthorized access attempts
- All fields from BaseEntity must be included in response

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
PRACTICE_DETAILS_SUCCESS | Success | Returns practice details | {"PracticeID": "guid", "PracticeName": ".NET", ...} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to view this practice"} | Yes | Error
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "Message": "Practice not found"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve practice details"} | Yes | Critical

### Security and Compliances
- [Access Control] Enforce role-based access control
- [Audit] Log all access attempts
- [PII] Mask sensitive information if present
- [Data Privacy] Ensure practice data is only visible to authorized users
- [Logging] Record all unauthorized access attempts


### Glossary
- [Practice] An organizational unit representing a business division or department
- [Master Admin] System administrator with highest level permissions
- [Practice Admin] Administrator for a specific practice
- [Source] Originating application for the operation
- [Audit Information] Creation and modification details of the practice