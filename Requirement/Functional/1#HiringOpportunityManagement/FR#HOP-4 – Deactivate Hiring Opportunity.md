## FR#HOP-4 – Deactivate Hiring Opportunity

### Description
System allows deactivation of hiring opportunities that are no longer needed.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can deactivate any hiring opportunity
- [TA Team Admin] Can deactivate opportunities within their assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - Hiring Opportunity exists and is active
    - User has deactivate permission
    - No active interview schedules linked
    - Valid deactivation reason provided

- [Postconditions]
    - Hiring Opportunity marked as inactive
    - Audit fields updated
    - Deactivation history recorded

### Module Name
- Hiring Opportunity Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`hiringOpportunityID` | Unique ID | uuid | Must exist | Yes | None | "12345678-1234-1234-1234-123456789012"
`reason` | Deactivation reason | string | Must not be empty | Yes | None | "Requirements fulfilled"
`statusID` | New status | integer | Must be valid final status | Yes | None | 3
`modUser` | Modified by | string | Must be current user | Yes | None | "user123"
---

#### System-Level Business Rules
- Check for linked active interviews
- Update status to closed/cancelled
- Maintain deactivation history
- Cannot reactivate once deactivated
- Archive after retention period
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
HIRING_OPPORTUNITY_DEACTIVATE_SUCCESS | Success | Returns success message | {"message": "Hiring opportunity deactivated successfully"} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Active interviews exist"} | Yes | Error
NOT_FOUND_ERROR | Failure | Returns not found error | {"code": "NOT_FOUND_ERROR", "message": "Hiring opportunity not found"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to deactivate opportunity"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to deactivate opportunity"} | Yes | Critical

### Security and Compliances 
- [Access Control] Practice-specific deactivation rights
- [Audit] Record deactivation details
- [Data Retention] Follow archival policies

### Glossary
- [Deactivation] Soft deletion of record
- [Final Status] Terminal state (Closed/Cancelled)
- [Retention Period] Time before archival