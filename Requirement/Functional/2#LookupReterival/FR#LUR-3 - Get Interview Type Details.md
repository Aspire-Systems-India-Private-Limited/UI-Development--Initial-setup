## FR#LUR-3 – Get Interview Type Details

### Description
System should allow authorized users to retrieve detailed information about specific interview types used for categorizing different interview formats.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [All Roles] Can view interview type details as these are essential reference data
- [Master Admin] Can view all types including inactive ones
- [Other Roles] Can view only active types

### Preconditions and Postconditions
- [Preconditions]
    - Interview type must exist in the system
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Interview type details are returned if authorized
    - Access attempt is logged

### Module Name
- Lookup Data Management

### Fields level Business Rules
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`InterviewTypeID` | Unique identifier | guid | Must be valid existing ID | Yes | None | "12345678-1234-1234-1234-123456789012"

### Response Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`InterviewTypeID` | Unique identifier | guid | "12345678-1234-1234-1234-123456789012"
`Name` | System name | string | "WeekDaysScheduled"
`DisplayName` | Display name | string | "Weekday - Scheduled Interview"
`IsActive` | Status | boolean | true
`CreatedDate` | Creation timestamp | datetime | "2025-11-05T10:00:00Z"
`ModifiedDate` | Last update timestamp | datetime | "2025-11-05T10:00:00Z"
`ModUser` | Last updater's ID | string | "user123"
`Source` | Application source | integer | 1 (Web)

### System-Level Business Rules
- All roles can access interview type data
- Return not found for non-existent types
- Cache frequently accessed type data
- Handle both active and inactive types
- All fields from BaseEntity must be included in response
- Response must follow GetInterviewTypeResponse schema

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
INTERVIEW_TYPE_GET_SUCCESS | Success | Returns type details | {"successCode": "INTERVIEW_TYPE_GET_SUCCESS", "successMessage": "Interview type details retrieved successfully", "type": {...}} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to view interview type details"} | Yes | Error
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "Message": "Interview type not found"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve interview type details"} | Yes | Critical

### Security and Compliances
- [Access Control] Basic authentication required
- [Audit] Log all access attempts
- [Caching] Implement efficient caching strategy
- [Performance] Optimize for frequent access
- [Logging] Record unauthorized access attempts

### User Stories

1. **View Interview Type Details**
   ```
   As an authorized user
   I want to retrieve interview type details
   So that I can understand the interview format and scheduling requirements
   ```

2. **Access Cached Data**
   ```
   As an authorized user
   I want quick access to interview type information
   So that I can maintain system performance
   ```

3. **Handle Missing Types**
   ```
   As an authorized user
   I want to receive clear feedback for non-existent interview types
   So that I can report or fix invalid references
   ```

4. **View Audit Information**
   ```
   As a Master Admin
   I want to see interview type audit information
   So that I can track changes to reference data
   ```

### Glossary
- [Interview Type] Format of interview (e.g., WeekDay-Scheduled, WeekDay-Walkin, Weekend-Scheduled)
- [Display Name] User-friendly name shown in UI and reports
- [System Name] Internal identifier used by the application
- [Source] Origin of the data (Web, Mobile, API, etc.)
- [Audit Information] Creation and modification details of interview types