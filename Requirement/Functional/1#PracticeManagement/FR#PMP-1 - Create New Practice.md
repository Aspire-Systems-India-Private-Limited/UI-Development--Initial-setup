## FR#PMP-1 – Create New Practice

### Description
System should allow Master Admin to create new practices in the system. Each practice represents a business unit or department that can have its own members and administrators.

### User Roles
- Master Admin

### Personas and Permissions
- [Master Admin] Can create new practices. Not bound to any practice.
- Other roles cannot create practices.

### Preconditions and Postconditions
- [Preconditions]
    - User must be authenticated
    - User must have Master Admin role
    - Practice name must be unique in the system

- [Postconditions]
    - New practice is created in the system
    - Practice ID is generated
    - Audit fields are set
    - Success message is returned with PracticeID

### Module Name
- Practice Management

### Fields level Business Rules
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`PracticeName` | Name of the practice | string | Must be unique, Min 2 characters, Max 50 characters | Yes | None | ".NET"
`Description` | Description of the practice | string | Max 500 characters | No | None | "Microsoft .NET Development Practice"
`IsActive` | Practice status | boolean | Must be true for new practice | Yes | true | true
`UpdatedBy` | ID of user updating ceating practice | string | Must be current user ID | Yes | None | "user123"
`Source` | Application source | string | Must be valid Application SourceID | Yes | None | "WebApp"

### System-Level Business Rules
- `PracticeID` is a system-generated GUID
- `CreatedDate` and `ModifiedDate` must be set to current date and time
- `ModUser` must be set to current user ID
- Practice name must be unique across all practices
- Only Master Admin can create practices
- Initial status must be active (IsActive = true)
- All audit fields (BaseEntity) must be properly set

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
PRACTICE_CREATE_SUCCESS | Success | Returns PracticeID and success message | {"PracticeID": "12345678-1234-1234-1234-123456789012", "Message": "Practice created successfully"} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to create practices"} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "Message": "Practice name is required"} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "Message": "Practice name must be between 2 and 50 characters"} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "Message": "Source is required"} | Yes | Error
DUPLICATE_ENTRY_ERROR | Failure | Returns error code and message | {"ErrorCode": "DUPLICATE_ENTRY_ERROR", "Message": "Practice name already exists"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to create practice"} | Yes | Critical

### Security and Compliances
- [Access Control] Only Master Admin can create practices
- [Audit] Record creator, timestamp, source application
- [Validation] Enforce unique practice names
- [Logging] Log all practice creation attempts with user context
- [History] Maintain creation audit trail


### Glossary
- [Practice] An organizational unit representing a business division or department
- [Master Admin] System administrator with highest level permissions
- [Location] Physical location where the practice operates
- [Source] Originating application for the operation (e.g., WebApp, API, Admin)
- [Audit Trail] Record of practice creation with timestamp and user information