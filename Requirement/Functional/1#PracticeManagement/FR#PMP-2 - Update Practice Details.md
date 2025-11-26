## FR#PMP-2 – Update Practice Details

### Description
System should allow Master Admin to update existing practice details while maintaining data integrity and audit trail.

### User Roles
- Master Admin

### Personas and Permissions
- [Master Admin] Can update any practice details. Not bound to any practice.
- Other roles cannot update practice details.

### Preconditions and Postconditions
- [Preconditions]
    - Practice must exist in the system
    - Practice must be active
    - User must be authenticated as Master Admin
    - Updated practice name (if changed) must be unique

- [Postconditions]
    - Practice details are updated
    - Audit fields are updated
    - Success message is returned
    - Update history is recorded

### Module Name
- Practice Management

### Fields level Business Rules
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`PracticeID` | Unique identifier | guid | Must be valid existing PracticeID | Yes | None | "12345678-1234-1234-1234-123456789012"
`PracticeName` | Name of the practice | string | Must be unique if changed, Min 2 characters, Max 50 characters | Yes | Existing Value | ".NET"
`Description` | Description of the practice | string | Max 500 characters | No | Existing Value | "Microsoft .NET Development Practice"
`IsActive` | Practice status | boolean | Must be true or false | Yes | Existing Value | true
`UpdatedBy` | ID of user updating practice | string | Must be current user ID | Yes | None | "user123"
`Source` | Application source | string | Must be valid Application SourceID | Yes | None | "WebApp"

### System-Level Business Rules
- Cannot modify `PracticeID`
- `ModifiedDate` must be set to current date and time
- `ModUser` must be set to current user ID
- Practice name must remain unique across all practices if changed
- Only Master Admin can update practices
- Cannot update a deactivated practice
- All audit fields (BaseEntity) must be properly updated

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
PRACTICE_UPDATE_SUCCESS | Success | Returns success message | {"Message": "Practice updated successfully"} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to update practices"} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "Message": "Practice name is required"} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "Message": "Practice name must be between 2 and 50 characters"} | Yes | Error
DUPLICATE_ENTRY_ERROR | Failure | Returns error code and message | {"ErrorCode": "DUPLICATE_ENTRY_ERROR", "Message": "Practice name already exists"} | Yes | Error
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "Message": "Practice not found"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to update practice"} | Yes | Critical

### Security and Compliances
- [Access Control] Only Master Admin can update practices
- [Audit] Record updater, timestamp, source application
- [Validation] Enforce unique practice names
- [Logging] Log all practice update attempts
- [History] Maintain update history for auditing



### Glossary
- [Practice] An organizational unit representing a business division or department
- [Master Admin] System administrator with highest level permissions
- [Location] Physical location where the practice operates
- [Source] Originating application for the operation
- [Audit Trail] Record of all changes made to practice details