## FR#CPM-3 – Update Candidate Profile

### Description
System allows modification of existing candidate profile information.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can update any candidate profile
- [TA Team Admin] Can update profiles within their assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Candidate Profile exists and is active
    - User has update permission
    - Valid update data provided

- [Postconditions]
    - Profile information updated
    - Audit fields updated
    - Change history recorded

### Module Name
- Candidate Profile Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`candidateProfileID` | Profile ID | uuid | Must exist | Yes | None | "12345678-1234-1234-1234-123456789012"
`firstName` | First Name | string | Min 1, Max 50 chars | Yes | None | "John"
`lastName` | Last Name | string | Min 1, Max 50 chars | Yes | None | "Doe"
`emailID` | Email | string | Valid email, Max 250 | Yes | None | "john.doe@example.com"
`designationPresentedFor` | Presented Designation | uuid | Must be valid | Yes | None | "12345678-1234-1234-1234-123456789012"
`yearsOfExperience` | Experience | number | Must be positive | Yes | None | 5.5
`resumeDocument` | Resume | string | Valid document ref | No | None | "resume_12345.pdf"
`modUser` | Modified by | string | Must be current user | Yes | None | "user123"
---

#### System-Level Business Rules
- Maintain email uniqueness
- Track document version history
- Update modified date automatically
- Record all field changes
- Validate designation changes
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
CANDIDATE_PROFILE_UPDATE_SUCCESS | Success | Returns success message | {"message": "Profile updated successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid email format"} | Yes | Error
NOT_FOUND_ERROR | Failure | Returns not found error | {"code": "NOT_FOUND_ERROR", "message": "Profile not found"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to update profile"} | Yes | Error
DUPLICATE_ERROR | Failure | Returns duplicate error | {"code": "DUPLICATE_ERROR", "message": "Email already exists"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to update profile"} | Yes | Critical

### Security and Compliances 
- [PII Protection] Secure handling of personal data
- [Document Security] Secure document updates
- [Audit] Track all modifications

### Glossary
- [Document Reference] Link to stored resume
- [Version History] Track of document changes
- [Field Change] Modified field tracking