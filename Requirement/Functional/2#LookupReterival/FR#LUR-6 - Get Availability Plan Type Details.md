## FR#LUR-6 – Get Availability Plan Type Details

### Description
System should allow authorized users to retrieve detailed information about availability plan types used for categorizing different scheduling availability configurations.

### User Roles
- Master Admin
- Practice Admin
- Tech Team Panel Member
- TA Team Admin

### Personas and Permissions
- [All Roles] Can view availability plan type details as these are essential reference data
- [Master Admin] Can view all types including inactive ones
- [Other Roles] Can view only active types

### Preconditions and Postconditions
- [Preconditions]
    - Availability plan type must exist in the system
    - User must be authenticated
    - User must have appropriate permissions

- [Postconditions]
    - Availability plan type details are returned if authorized
    - Access attempt is logged

### Module Name
- Lookup Data Management

### Fields level Business Rules
FieldName | Description | Type | Validation | Required | Default Value | Example
----------|-------------|------|------------|----------|---------------|----------
`AvailabilityPlanTypeID` | Unique identifier | guid | Must be valid existing ID | Yes | None | "12345678-1234-1234-1234-123456789012"

### Response Fields
FieldName | Description | Type | Example
----------|-------------|------|----------
`AvailabilityPlanTypeID` | Unique identifier | guid | "12345678-1234-1234-1234-123456789012"
`Name` | System name | string | "WeeklyRecurring"
`DisplayName` | Display name | string | "Weekly Recurring Plan"
`IsActive` | Status | boolean | true
`CreatedDate` | Creation timestamp | datetime | "2025-11-05T10:00:00Z"
`ModifiedDate` | Last update timestamp | datetime | "2025-11-05T10:00:00Z"
`ModUser` | Last updater's ID | string | "user123"
`Source` | Application source | integer | 1 (Web)

### System-Level Business Rules
- All roles can access availability plan type data
- Return not found for non-existent types
- Cache frequently accessed type data
- Handle both active and inactive types
- All fields from BaseEntity must be included in response
- Response must follow GetAvailabilityPlanTypeResponse schema

### API Level Business Rules
Result Name | ResultType | Response and ActionsValidation | Example | Should be logged | Response Category
------------|------------|--------------------------------|---------|------------------|------------------
AVAILABILITY_PLAN_TYPE_GET_SUCCESS | Success | Returns type details | {"successCode": "AVAILABILITY_PLAN_TYPE_GET_SUCCESS", "successMessage": "Availability plan type details retrieved successfully", "type": {...}} | No | Informational
UNAUTHORIZED_ERROR | Failure | Returns error code and message | {"ErrorCode": "UNAUTHORIZED_ERROR", "Message": "You are not authorized to view availability plan type details"} | Yes | Error
RESOURCE_NOT_FOUND_ERROR | Failure | Returns error code and message | {"ErrorCode": "RESOURCE_NOT_FOUND_ERROR", "Message": "Availability plan type not found"} | Yes | Error
SYSTEM_ERROR | Failure | Returns error code and message | {"ErrorCode": "SYSTEM_ERROR", "Message": "Failed to retrieve availability plan type details"} | Yes | Critical

### Security and Compliances
- [Access Control] Basic authentication required
- [Audit] Log all access attempts
- [Caching] Implement efficient caching strategy
- [Performance] Optimize for frequent access
- [Logging] Record unauthorized access attempts

### User Stories

1. **View Availability Plan Type Details**
   ```
   As an authorized user
   I want to retrieve availability plan type details
   So that I can understand the scheduling configuration options
   ```

2. **Access Cached Data**
   ```
   As an authorized user
   I want quick access to availability plan type information
   So that I can maintain system performance
   ```

3. **Handle Missing Types**
   ```
   As an authorized user
   I want to receive clear feedback for non-existent availability plan types
   So that I can report or fix invalid references
   ```

4. **View Audit Information**
   ```
   As a Master Admin
   I want to see availability plan type audit information
   So that I can track changes to reference data
   ```

### Glossary
- [Availability Plan Type] Configuration type for availability schedules (e.g., Weekly Recurring, Monthly Recurring, One-time)
- [Display Name] User-friendly name shown in UI and reports
- [System Name] Internal identifier used by the application
- [Source] Origin of the data (Web, Mobile, API, etc.)
- [Audit Information] Creation and modification details of availability plan types