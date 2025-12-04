# User Stories: Opportunity Management Screen

## Module: Hiring Opportunity Management
**Reference:** Figma_All_Screens.md - Section 8 (Opportunity Management Screen)  
**Related FR:** FR#HOP-1 to FR#HOP-4

---

## US-008.1: View Hiring Opportunities List
**As a** Master Admin or TA Team Admin  
**I want to** view all hiring opportunities  
**So that** I can see current recruitment needs

### Acceptance Criteria:
- [ ] Display opportunities in a table with columns: Title, Designation, JD, Practice, Status, Candidate Count, Actions
- [ ] Master Admin sees all opportunities across all practices
- [ ] TA Team Admin sees opportunities for their assigned practice
- [ ] Practice Admin sees opportunities for their practice
- [ ] Display opportunity count at the top
- [ ] Show status badges: Open (green), In Progress (blue), Closed (gray)
- [ ] Default sorting by created date (newest first)
- [ ] Empty state message when no opportunities exist

### UI Elements:
- Opportunities table with sortable columns
- Opportunity count badge
- Status indicator badges
- Action menu for each row
- "Add Opportunity" button
- Empty state illustration

### Business Rules:
- Master Admin: View all opportunities
- TA Team Admin: View opportunities in assigned practice
- Practice Admin: View opportunities in their practice
- Display both active and closed opportunities with filter

### Related FR: FR#HOP-2 – Retrieve Hiring Opportunities

---

## US-008.2: Search and Filter Opportunities
**As a** Master Admin, TA Team Admin, or Practice Admin  
**I want to** search and filter opportunities  
**So that** I can quickly find specific opportunities

### Acceptance Criteria:
- [ ] Search box allows searching by title, designation, or JD
- [ ] Search results update as user types (debounced)
- [ ] Filter by practice (dropdown) - for Master Admin
- [ ] Filter by designation (dropdown)
- [ ] Filter by status (dropdown: All, Open, In Progress, Closed)
- [ ] Filter by opportunity category (Forecast, Client Requirements)
- [ ] Multiple filters can be applied simultaneously
- [ ] "Clear Filters" button resets all filters
- [ ] Display count of filtered results

### UI Elements:
- Search input field
- Practice filter dropdown (Master Admin only)
- Designation filter dropdown
- Status filter dropdown
- Category filter dropdown
- Clear Filters button
- Results count label

---

## US-008.3: Create New Hiring Opportunity
**As a** Master Admin or TA Team Admin  
**I want to** create a new hiring opportunity  
**So that** recruitment activities can begin

### Acceptance Criteria:
- [ ] "Add Opportunity" button opens create opportunity form
- [ ] Form displays all required fields with validation
- [ ] Title field (min 5, max 50 characters, required)
- [ ] Opportunity Category dropdown (Forecast, Client Requirements, required)
- [ ] Practice dropdown (required, filtered by user permissions)
- [ ] Designation dropdown (required, filtered by selected practice)
- [ ] Job Description dropdown (required, filtered by designation)
- [ ] Job Description field auto-populated when JD selected
- [ ] Additional Notes textarea (optional)
- [ ] Planned Candidates Count field (number, min 0, max 50, required)
- [ ] Source dropdown (Web, Mobile, API, Admin, required)
- [ ] Status automatically set to "Open" for new opportunities
- [ ] "Create" button enabled when all required fields valid
- [ ] "Cancel" button closes form without saving
- [ ] Display validation errors inline
- [ ] Success notification shows created opportunity ID
- [ ] New opportunity appears in list immediately

### UI Elements:
- "Add Opportunity" button (primary action)
- Modal/page form with fields:
  - Title (text input, required)
  - OpportunityCategoryID (dropdown, required)
  - PracticeID (dropdown, required)
  - Designation (dropdown, required)
  - JobDescriptionID (dropdown, required)
  - JobDescription (display/textarea, auto-filled)
  - AdditionalNotes (textarea, optional)
  - PlannedCandidatesCount (number input, required)
  - Source (dropdown, required)
- Create button (primary)
- Cancel button (secondary)
- Inline validation messages
- Success toast notification

### Business Rules:
- Master Admin can create opportunities for any practice
- TA Team Admin can create opportunities for their assigned practice
- Title must be descriptive and unique within practice (optional uniqueness)
- Status defaults to "Open" (StatusID = 1)
- IsActive defaults to true
- System-generated HiringOpportunityID (GUID)
- CreatedDate and ModifiedDate set to current timestamp
- ModUser set to current user ID

### Related FR: FR#HOP-1 – Create Hiring Opportunity

---

## US-008.4: View Opportunity Details
**As a** Master Admin, TA Team Admin, or Practice Admin  
**I want to** view detailed information about an opportunity  
**So that** I can see complete opportunity information and progress

### Acceptance Criteria:
- [ ] Clicking opportunity title or "View" action opens detail modal/page
- [ ] Display all opportunity information: Title, Category, Practice, Designation, JD, Status
- [ ] Show job description full text
- [ ] Display additional notes
- [ ] Show planned vs. actual candidate count
- [ ] Display list of candidates associated with opportunity
- [ ] Show interview statistics (scheduled, completed, pending)
- [ ] Display audit information: Created Date, Modified Date, Created By
- [ ] "Edit" and "Close" buttons available (if permissions allow)
- [ ] "Close" button returns to opportunity list

### UI Elements:
- Opportunity detail modal/page
- Information sections: Basic Info, Job Description, Candidates, Interview Statistics, Audit Info
- Action buttons: Edit, Close Opportunity, View History, Close
- Candidates table with status
- Statistics cards

---

## US-008.5: Edit Hiring Opportunity
**As a** Master Admin or TA Team Admin  
**I want to** edit opportunity information  
**So that** I can update opportunity details as requirements change

### Acceptance Criteria:
- [ ] "Edit" button in opportunity row or detail view opens edit form
- [ ] Form pre-populated with existing opportunity data
- [ ] Allow editing: Title, Designation, JobDescriptionID, AdditionalNotes, PlannedCandidatesCount, Status
- [ ] Practice and Category cannot be changed (read-only)
- [ ] Title validation applies as in create
- [ ] Status dropdown: Open, In Progress, Closed
- [ ] Changing status to "Closed" requires confirmation
- [ ] "Save" button updates opportunity
- [ ] "Cancel" button discards changes
- [ ] Audit fields updated automatically (ModifiedDate, ModUser)
- [ ] Success message confirms update
- [ ] Updated opportunity reflected in list

### UI Elements:
- Edit form modal with pre-filled fields
- Read-only Practice and Category fields
- Status dropdown
- Confirmation dialog for status change
- Save button (primary)
- Cancel button (secondary)
- Success notification

### Business Rules:
- Cannot change practice or category after creation
- Closing opportunity requires all interviews to be completed or cancelled
- Status change from Open to Closed records closure details
- ModifiedDate and ModUser updated on save

### Related FR: FR#HOP-3 – Update Hiring Opportunity

---

## US-008.6: Close Hiring Opportunity
**As a** Master Admin or TA Team Admin  
**I want to** close a hiring opportunity  
**So that** completed recruitment activities are properly recorded

### Acceptance Criteria:
- [ ] "Close Opportunity" action available for Open/In Progress opportunities
- [ ] Clicking "Close" opens closure confirmation dialog
- [ ] Dialog requires closure reason (dropdown: Fulfilled, Cancelled, On Hold, Other)
- [ ] If "Other" selected, text field for reason details appears
- [ ] Check for pending interviews (scheduled but not completed)
- [ ] If pending interviews exist, show warning and list
- [ ] User must confirm closure despite warnings or cancel pending interviews first
- [ ] Upon confirmation, opportunity status set to "Closed"
- [ ] Closure details recorded: ClosedDate, ClosedBy, ClosureReason
- [ ] Success message confirms closure
- [ ] Closed opportunity shown with "Closed" badge in list
- [ ] Closed opportunities not editable (read-only)

### UI Elements:
- Close Opportunity button
- Closure confirmation dialog
- Closure reason dropdown
- Reason details textarea (for "Other")
- Warning message for pending interviews
- Confirm and Cancel buttons
- Success notification

### Business Rules:
- Only Open or In Progress opportunities can be closed
- Closure reason is mandatory
- Pending interviews should be resolved before closure (or force close with warning)
- Closure is recorded in audit trail
- Closed opportunities cannot be reopened (or require special permission)
- Candidates remain associated but cannot schedule new interviews

---

## US-008.7: Deactivate Hiring Opportunity
**As a** Master Admin or TA Team Admin  
**I want to** deactivate a hiring opportunity  
**So that** it's removed from active lists but retained for records

### Acceptance Criteria:
- [ ] "Deactivate" action available in opportunity menu
- [ ] Clicking "Deactivate" displays confirmation dialog
- [ ] Deactivation reason required (textarea)
- [ ] Check for active candidates and interviews
- [ ] Warning displayed if active dependencies exist
- [ ] Upon confirmation, opportunity IsActive set to false
- [ ] Deactivation details recorded: DeactivationReason, DeactivatedDate, DeactivatedBy
- [ ] Deactivation history entry created
- [ ] Success message confirms deactivation
- [ ] Deactivated opportunity shown with "Inactive" badge
- [ ] Deactivated opportunities not shown in dropdowns

### UI Elements:
- Deactivate button
- Confirmation dialog with reason field
- Warning message for dependencies
- Success notification

### Business Rules:
- Deactivation reason is mandatory
- Deactivation is soft delete (IsActive = false)
- Deactivation history recorded in HiringOpportunityDeactivationHistory table
- Deactivated opportunities still viewable with filter
- Cannot create new candidates for deactivated opportunities
- Cannot schedule new interviews for deactivated opportunities

### Related FR: FR#HOP-4 – Deactivate Hiring Opportunity

---

## US-008.8: Reactivate Hiring Opportunity
**As a** Master Admin  
**I want to** reactivate a previously deactivated opportunity  
**So that** it can be used for recruitment again

### Acceptance Criteria:
- [ ] "Reactivate" button available for inactive opportunities (Master Admin only)
- [ ] Clicking "Reactivate" displays confirmation dialog
- [ ] Reactivation reason optional
- [ ] Upon confirmation, opportunity IsActive set to true
- [ ] Status set to "Open"
- [ ] Reactivated opportunity appears as active in list
- [ ] Success message confirms reactivation
- [ ] Opportunity becomes available for candidate and interview operations

### UI Elements:
- Reactivate button (Master Admin only)
- Confirmation dialog
- Success notification

---

## US-008.9: View Associated Candidates
**As a** Master Admin, TA Team Admin, or Practice Admin  
**I want to** view candidates associated with an opportunity  
**So that** I can track recruitment progress

### Acceptance Criteria:
- [ ] "View Candidates" action or tab in opportunity detail view
- [ ] Display candidates in a table: Name, Email, Designation, Status, Interview Status, Actions
- [ ] Candidate count displayed
- [ ] Click candidate to view profile
- [ ] "Add Candidate" button to associate new candidate with opportunity
- [ ] Filter candidates by status (Pending, Scheduled, Completed, Rejected)
- [ ] Sort by name, status, interview status

### UI Elements:
- Candidates tab/section in opportunity detail
- Candidates table
- Add Candidate button
- Status filter dropdown
- View Profile link

---

## US-008.10: View Interview Statistics
**As a** Master Admin, TA Team Admin, or Practice Admin  
**I want to** see interview statistics for an opportunity  
**So that** I can monitor recruitment progress

### Acceptance Criteria:
- [ ] Statistics section in opportunity detail view
- [ ] Display metrics:
  - Total candidates
  - Interviews scheduled
  - Interviews completed
  - Interviews pending
  - Candidates selected
  - Candidates rejected
  - Average time to complete interviews
- [ ] Visual representations (charts/graphs) for key metrics
- [ ] Date range filter for statistics

### UI Elements:
- Statistics section with cards
- Charts/graphs for visual representation
- Date range filter

---

## US-008.11: Sort Opportunities List
**As a** system user  
**I want to** sort opportunities by different columns  
**So that** I can organize opportunities meaningfully

### Acceptance Criteria:
- [ ] Sortable columns: Title, Designation, Practice, Status, Candidate Count, Created Date
- [ ] Click column header to sort ascending, click again for descending
- [ ] Sort indicator displayed in active column
- [ ] Default sort: Created Date (newest first)
- [ ] Sort persists during pagination

### UI Elements:
- Sort indicators in column headers
- Sort direction arrows

---

## US-008.12: Pagination for Opportunities List
**As a** system user  
**I want to** navigate through pages of opportunities  
**So that** I can view large lists efficiently

### Acceptance Criteria:
- [ ] Display 20 opportunities per page by default
- [ ] Page size selector: 10, 20, 50
- [ ] Page navigation: First, Previous, Next, Last
- [ ] Display current page and total pages
- [ ] Display total opportunity count
- [ ] Pagination controls disabled appropriately

### UI Elements:
- Pagination controls at bottom of table
- Page size dropdown
- Page navigation buttons
- Page and count display

---

## US-008.14: View Opportunity Deactivation History
**As a** Master Admin or TA Team Admin  
**I want to** view deactivation history for an opportunity  
**So that** I can understand why and when it was deactivated

### Acceptance Criteria:
- [ ] "View History" button in opportunity detail view
- [ ] Opens deactivation history modal/page
- [ ] Display history entries: Date, Deactivated By, Reason, Previous Status, New Status
- [ ] Sort by date (newest first)
- [ ] If multiple deactivations, show all entries

### UI Elements:
- View History button
- History modal/page
- History table with timeline view
- Close button

---

## US-008.15: Opportunity Dashboard Widget
**As a** TA Team Admin or Practice Admin  
**I want to** see opportunity summary on my dashboard  
**So that** I can quickly understand current recruitment status

### Acceptance Criteria:
- [ ] Dashboard widget shows opportunity stats:
  - Open opportunities count
  - In Progress opportunities count
  - Total candidates
  - Interviews scheduled this week
- [ ] Click widget to navigate to opportunities list
- [ ] Widget updates in real-time or on refresh

### UI Elements:
- Opportunity summary widget on dashboard
- Stat cards with counts
- Navigation link to full opportunities list

---

## Technical Notes:
- Implement cascading dropdowns for Practice → Designation → JD selection
- Cache designation and JD lookups for dropdown population
- Validate opportunity title uniqueness at server-side
- Log all opportunity management actions for audit
- Implement status transition validations (Open → In Progress → Closed)
- Consider workflow approvals for opportunity creation (future enhancement)
- Track opportunity lifecycle metrics for analytics

## Related Functional Requirements:
- FR#HOP-1 – Create Hiring Opportunity
- FR#HOP-2 – Retrieve Hiring Opportunities
- FR#HOP-3 – Update Hiring Opportunity
- FR#HOP-4 – Deactivate Hiring Opportunity
- FR#Opportunity Deactivation History

## Priority: P0 (Critical)
## Estimated Story Points: 13
