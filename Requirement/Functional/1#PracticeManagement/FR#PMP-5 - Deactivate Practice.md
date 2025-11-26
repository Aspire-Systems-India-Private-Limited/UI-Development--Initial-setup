## FR#PMP-5 – Deactivate Practice

### Description
System should allow Master Admin to deactivate a practice while maintaining data integrity and handling associated members.

### User Roles
- Master Admin

### Personas and Permissions
- [Master Admin] Can deactivate any active practice. Not bound to any practice.
- Other roles cannot deactivate practices.

### Preconditions and Postconditions
- [Preconditions]
    - Practice must exist and be active
    - User must be authenticated as Master Admin
    - Practice must not have any active members
    - All associated resources must be properly handled

- [Postconditions]
    - Practice is marked as inactive
    - Audit fields are updated
    - Success message is returned
    - Associated resources are properly handled
    - Deactivation history is recorded

### Module Name
- Practice Management

### Fields level Business Rules
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`PracticeID` | Unique identifier | guid | Must be valid existing PracticeID | Yes | None | "12345678-1234-1234-1234-123456789012"
`Reason` | Deactivation reason | string | Max 500 characters | Yes | None | "Practice merged with .NET Core practice"
`UpdatedBy` | ID of user deactivating | string | Must be current user ID | Yes | None | "user123"
`Source` | Application source | string | Must be valid Application SourceID | Yes | None | "WebApp"

### System-Level Business Rules
- Cannot deactivate already inactive practice
- Must verify no active members exist
- Must update practice status to inactive
- Must record deactivation reason
- Must update ModifiedDate and ModUser
- Should handle associated resources (archive/reassign)
- Must maintain deactivation audit trail

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
PRACTICE_DEACTIVATE_SUCCESS | Success | Returns success message | {"Message": "Practice deactivated successfully"} | Yes | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "Not authorized to deactivate practices"} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "Message": "Deactivation reason required"} | Yes | Error
VALIDATION_ERROR | Failure | Returns error code and message | {"ErrorCode": "VALIDATION_ERROR", "Message": "Reason must not exceed 500 characters"} | Yes | Error
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "Message": "Practice not found"} | Yes | Error
ACTIVE_MEMBERS_ERROR | Failure | Returns error code and message | {"ErrorCode": "ACTIVE_MEMBERS_ERROR", "Message": "Practice has active members"} | Yes | Error
INVALID_STATE_ERROR | Failure | Returns error code and message | {"ErrorCode": "INVALID_STATE_ERROR", "Message": "Practice is already inactive"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to deactivate practice"} | Yes | Critical

### Security and Compliances
- [Access Control] Only Master Admin can deactivate practices
- [Audit] Log deactivation with reason and timestamp
- [Data Integrity] Ensure proper handling of associated data
- [Validation] Verify no active dependencies exist
- [History] Maintain deactivation history
- [Logging] Record all deactivation attempts

### User Stories

1. **Deactivate Practice**
   ```
   As a Master Admin
   I want to deactivate a practice
   So that it's no longer available for new assignments
   ```

2. **Provide Deactivation Reason**
   ```
   As a Master Admin
   I want to provide a reason for practice deactivation
   So that there's a record of why the practice was deactivated
   ```

3. **Check Active Members**
   ```
   As a Master Admin
   I want to be notified if a practice has active members
   So that I can handle member reassignment before deactivation
   ```

4. **Handle Resources**
   ```
   As a Master Admin
   I want the system to properly handle associated resources
   So that no data is orphaned after practice deactivation
   ```

5. **View Deactivation History**
   ```
   As a Master Admin
   I want to see the deactivation history of practices
   So that I can track organizational changes
   ```

### Glossary
- [Practice] An organizational unit representing a business division or department
- [Active Members] Users currently assigned to the practice
- [Associated Resources] Data, assets, or configurations linked to the practice
- [Deactivation] Process of making a practice inactive while preserving historical data
- [Audit Trail] Record of practice deactivation with reason and user information