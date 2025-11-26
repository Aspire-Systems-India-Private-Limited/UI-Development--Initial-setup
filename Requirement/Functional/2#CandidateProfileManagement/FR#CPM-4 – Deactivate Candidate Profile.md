## FR#CPM-4 – Deactivate Candidate Profile

### Description
System allows deactivation of candidate profiles when no longer under consideration.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can deactivate any candidate profile
- [TA Team Admin] Can deactivate profiles within their assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Candidate Profile exists and is active
    - No pending interviews scheduled
    - Valid deactivation reason provided

- [Postconditions]
    - Profile marked as inactive
    - Audit fields updated
    - Related documents archived
    - Deactivation history recorded

### Module Name
- Candidate Profile Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`candidateProfileID` | Profile ID | uuid | Must exist | Yes | None | "12345678-1234-1234-1234-123456789012"
`reason` | Deactivation reason | string | Must not be empty | Yes | None | "Candidate withdrew"
`modUser` | Modified by | string | Must be current user | Yes | None | "user123"
`notes` | Additional notes | string | Optional | No | None | "Candidate found another opportunity"
---

#### System-Level Business Rules
- Check for pending interviews
- Archive related documents
- Maintain deactivation history
- Cannot reactivate automatically
- Follow data retention policy
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
CANDIDATE_PROFILE_DEACTIVATE_SUCCESS | Success | Returns success message | {"message": "Profile deactivated successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Pending interviews exist"} | Yes | Error
NOT_FOUND_ERROR | Failure | Returns not found error | {"code": "NOT_FOUND_ERROR", "message": "Profile not found"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to deactivate profile"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to deactivate profile"} | Yes | Critical

### Security and Compliances 
- [PII Handling] Proper data archival
- [Document Retention] Follow retention policies
- [Audit] Record deactivation details

### Glossary
- [Deactivation] Soft deletion of profile
- [Document Archival] Secure storage of documents
- [Retention Policy] Data storage duration rules