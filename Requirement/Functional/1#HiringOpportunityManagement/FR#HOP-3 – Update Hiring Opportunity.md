## FR#HOP-3 – Update Hiring Opportunity Details

### Description
System allows modification of existing hiring opportunity details.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can update any hiring opportunity
- [TA Team Admin] Can update opportunities within their assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Hiring Opportunity exists and is active
    - User has update permission for the practice
    - Valid update data provided

- [Postconditions]
    - Hiring Opportunity details updated
    - Audit fields updated
    - Change history recorded

### Module Name
- Hiring Opportunity Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`hiringOpportunityID` | Unique ID | uuid | Must exist | Yes | None | "12345678-1234-1234-1234-123456789012"
`title` | Title for opportunity | string | Min 5 characters, Max 50 characters | Yes | None | "Senior .NET Developer Required"
`opportunityCategoryID` | Category | uuid | Must be valid category | Yes | None | "12345678-1234-1234-1234-123456789012"
`jobDescription` | Job description | string | Must not be empty | Yes | None | "Updated job description..."
`additionalNotes` | Additional notes | string | Optional | No | None | "Updated requirements"
`plannedCandidatesCount` | Required candidates | integer | Min 0, Max 50 | Yes | None | 5
`statusID` | Status | integer | Must be valid status | Yes | None | 1
`modUser` | Modified by | string | Must be current user | Yes | None | "user123"
---

#### System-Level Business Rules
- Cannot change practice assignment
- Status transitions must be valid
- Original creation date preserved
- Modified date updated automatically
- Maintain change history
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
HIRING_OPPORTUNITY_UPDATE_SUCCESS | Success | Returns success message | {"message": "Hiring opportunity updated successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid status transition"} | Yes | Error
NOT_FOUND_ERROR | Failure | Returns not found error | {"code": "NOT_FOUND_ERROR", "message": "Hiring opportunity not found"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to update opportunity"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to update opportunity"} | Yes | Critical

### Security and Compliances 
- [Access Control] Practice-specific update permissions
- [Audit] Track all modifications
- [History] Maintain change history

### Glossary
- [Status Transition] Valid movement between status states
- [Change History] Record of modifications
- [Practice Assignment] Organizational ownership