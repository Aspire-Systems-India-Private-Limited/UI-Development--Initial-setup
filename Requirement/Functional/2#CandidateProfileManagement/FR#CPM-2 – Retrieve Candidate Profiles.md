## FR#CPM-2 – Retrieve Candidate Profiles

### Description
System provides ability to search and retrieve candidate profiles with filtering options.

### User Roles
- Master Admin
- TA Team Admin
---
### Personas and Permissions
- [Master Admin] Can view all candidate profiles across practices
- [TA Team Admin] Can view profiles within their assigned practices

---
### Preconditions and Postconditions
- [Preconditions]
    - User has valid role with view permissions
    - Valid search/filter parameters provided

- [Postconditions]
    - Filtered list of candidate profiles returned
    - Personal information properly masked
    - Access logged for audit

### Module Name
- Candidate Profile Management
---
### Fields level Business Rules
FieldName| Description | Type | Validation | Required | Default Value | Example
-----|-----|---------------|--------|--------|--------|--------
`pageNumber` | Page number | integer | Must be positive | Yes | 1 | 1
`pageSize` | Items per page | integer | Between 1 and 50 | Yes | 10 | 10
`searchTerm` | Search text | string | Optional | No | None | "John"
`hiringOpportunityID` | Filter by opportunity | uuid | Must be valid | No | None | "12345678-1234-1234-1234-123456789012"
`designationID` | Filter by designation | uuid | Must be valid | No | None | "12345678-1234-1234-1234-123456789012"
`experienceFrom` | Min experience | number | Must be positive | No | None | 2
`experienceTo` | Max experience | number | Must be positive | No | None | 5
`sortBy` | Sort field | string | Valid field name | No | "modifiedDate" | "firstName"
`sortDirection` | Sort direction | string | "asc" or "desc" | No | "desc" | "asc"
---

#### System-Level Business Rules
- Mask sensitive personal information
- Filter by practice automatically
- Include only active profiles by default
- Maximum page size enforced
- Sort by modified date by default
---

#### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|-------------------|-------------------|-------------------
CANDIDATE_PROFILES_RETRIEVED | Success | Returns filtered profiles | {"items": [...], "totalCount": 50, "pageNumber": 1} | No | Informational
VALIDATION_ERROR | Failure | Returns validation error | {"code": "VALIDATION_ERROR", "message": "Invalid experience range"} | Yes | Error
UNAUTHORIZED_ERROR | Failure | Returns unauthorized error | {"code": "UNAUTHORIZED_ERROR", "message": "Not authorized to view profiles"} | Yes | Error
SYSTEM_ERROR | Failure | Returns system error | {"code": "SYSTEM_ERROR", "message": "Failed to retrieve profiles"} | Yes | Critical

### Security and Compliances 
- [PII Protection] Mask sensitive data
- [Access Control] Practice-based filtering
- [Audit] Log all profile access

### Glossary
- [Search Term] Text to match against profile fields
- [Experience Range] Min/max years of experience
- [Designation] Job level/position