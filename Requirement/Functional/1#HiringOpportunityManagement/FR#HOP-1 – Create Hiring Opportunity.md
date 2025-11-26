## FR#HOP-1 – Create Hiring Opportunity by Practice Admin and Master Admin

### Description
System can have hiring opportunities created to manage interview requirements. 

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can create hiring opportunities across all practices
- [TA Team Admin] Can create hiring opportunities within assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Practice exists and is active
    - User has valid role (Master Admin or Practice Admin)
    - Opportunity Category must be valid
    - Required fields must be properly populated

- [Postconditions]
    - Hiring Opportunity is created with a unique ID
    - Audit fields are set
    - HiringOpportunityID is returned in the response

### Module Name
- Hiring Opportunity Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`title` | Title for opportunity | string | Min 5 characters, Max 50 characters | Yes | None | "Senior .NET Developer Required"
`opportunityCategoryID` | Category of opportunity | uuid | Must be valid category (Forecast/ClientRequirements) | Yes | None | "12345678-1234-1234-1234-123456789012"
`practiceID` | Practice this opportunity belongs to | uuid | Must be valid practice ID | Yes | None | "12345678-1234-1234-1234-123456789012"
`jobDescription` | Detailed job description | string | Must not be empty | Yes | None | "We are looking for experienced .NET developers..."
`additionalNotes` | Additional notes about opportunity | string | Optional | No | None | "Immediate joiners preferred"
`plannedCandidatesCount` | Number of candidates required | integer | Min 0, Max 50 | Yes | None | 5
`statusID` | Status of the opportunity | integer | Must be valid status (Open, InProgress, Closed) | Yes | Open | 1
`isActive` | Is active | boolean | Must be true for new opportunities | Yes | true | true
`modUser` | Modified by | string | Must be current user ID | Yes | None | "user123"
`source` | Application Source | integer | Must be valid source (Web, Mobile, API, etc.) | Yes | None | 1
---

#### System-Level Business Rules
- `hiringOpportunityID` is a system-generated UUID
- `createdDate` and `modifiedDate` must be set to current UTC date and time
- `modUser` must be set to current user ID
- New opportunities must have `statusID` set to Open (1)
- `plannedCandidatesCount` must be realistic and within system limits
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
HIRING_OPPORTUNITY_CREATE_SUCCESS | Success | Returns HiringOpportunityID and success message | {"hiringOpportunityID": "12345678-1234-1234-1234-123456789012","message": "Hiring opportunity created successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error details | {"code": "VALIDATION_ERROR", "message": "Title length must be between 5 and 50 characters"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "You are not authorized to create hiring opportunities"} | Yes | Error
RESOURCE_NOT_FOUND_ERROR | Failure | Returns not found error for invalid references | {"code": "RESOURCE_NOT_FOUND_ERROR", "message": "Practice not found"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to create hiring opportunity"} | Yes | Critical

###  Security and Compliances 
- [Access Controls] Enforce practice-specific access for Practice Admins
- [Audit] Record creator, timestamp, source application
- [Validation] Ensure all required fields meet business rules

### Glossary
- [Hiring Opportunity] A record representing a hiring need for specific practice
- [Practice] Organizational unit that owns the hiring opportunity
- [Opportunity Category] Classification of opportunity (Forecast or Client Requirements)
- [Status] Current state of the hiring opportunity (Open, InProgress, Closed)