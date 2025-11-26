## FR#CPM-1 – Create Candidate Profile by TA Team Admin

### Description
System allows creation of candidate profiles for interview process management.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can create candidate profiles for any practice
- [TA Team Admin] Can create candidate profiles for assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Valid Hiring Opportunity exists
    - User has TA Team Admin role
    - Required candidate information is available
    - Designation details are valid

- [Postconditions]
    - Candidate Profile is created with unique ID
    - Audit fields are set
    - CandidateProfileID is returned in response
    - Resume document is properly stored

### Module Name
- Candidate Profile Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`hiringOpportunityID` | Linked Hiring Opportunity | uuid | Must be valid and active opportunity | Yes | None | "12345678-1234-1234-1234-123456789012"
`firstName` | Candidate's First Name | string | Min 1 character, Max 50 characters | Yes | None | "John"
`lastName` | Candidate's Last Name | string | Min 1 character, Max 50 characters | Yes | None | "Doe"
`emailID` | Candidate's Email | string | Must be valid email format, Max 250 characters | Yes | None | "john.doe@example.com"
`designationAppliedFor` | Applied Designation | uuid | Must be valid designation | Yes | None | "12345678-1234-1234-1234-123456789012"
`designationPresentedFor` | Presented Designation | uuid | Must be valid designation | Yes | None | "12345678-1234-1234-1234-123456789012"
`yearsOfExperience` | Years of Experience | number | Must be positive number | Yes | None | 5.5
`candidateSource` | Source of Candidate | string | Must not be empty | Yes | None | "LinkedIn"
`resumeDocument` | Resume Reference | string | Must be valid document reference | Yes | None | "resume_12345.pdf"
`mappedTATeamMember` | Assigned TA Member | uuid | Must be valid team member ID | Yes | None | "12345678-1234-1234-1234-123456789012"
`isActive` | Is active | boolean | Must be true for new profiles | Yes | true | true
`modUser` | Modified by | string | Must be current user ID | Yes | None | "user123"
`source` | Application Source | integer | Must be valid source | Yes | None | 1
---

#### System-Level Business Rules
- `candidateProfileID` is system-generated UUID
- `createdDate` and `modifiedDate` must be UTC timestamps
- Resume document must be stored securely
- Email must be unique across active candidates
- Designations must be compatible with opportunity requirements
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
CANDIDATE_PROFILE_CREATE_SUCCESS | Success | Returns CandidateProfileID and message | {"candidateProfileID": "12345678-1234-1234-1234-123456789012", "message": "Candidate profile created successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error details | {"code": "VALIDATION_ERROR", "message": "Invalid email format"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to create candidate profiles"} | Yes | Error
DUPLICATE_ENTRY_ERROR | Failure | Returns duplicate error | {"code": "DUPLICATE_ENTRY_ERROR", "message": "Email already exists"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to create candidate profile"} | Yes | Critical

### Security and Compliances 
- [PII handling] Secure storage of candidate personal information
- [Document Security] Secure storage and access of resume documents
- [Audit] Track all profile modifications

### Glossary
- [Candidate Profile] Record containing candidate information and documents
- [Designation] Job level/position (SSE, ML, TL)
- [TA Team Member] HR team member responsible for candidate coordination