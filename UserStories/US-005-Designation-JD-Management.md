# User Stories: Designation & JD Management Screen

## Module: Designation & Job Description Management
**Reference:** Figma_All_Screens.md - Section 5 (Designation & JD Management Screen)

---

## US-005.1: View Designations and JDs with Tabs
**As a** Master Admin or Practice Admin  
**I want to** view designations and job descriptions in separate tabs  
**So that** I can manage them independently

### Acceptance Criteria:
- [ ] Screen displays two tabs: "Designations" and "Job Descriptions"
- [ ] Default active tab is "Designations"
- [ ] Clicking tab switches content without page reload
- [ ] Active tab is visually highlighted
- [ ] Tab content loads appropriate data

### UI Elements:
- Tab navigation (Designations | Job Descriptions)
- Active tab indicator
- Tab content area

---

## US-005.2: View Designation List
**As a** Master Admin or Practice Admin  
**I want to** view all designations in the system  
**So that** I can see available designation levels

### Acceptance Criteria:
- [ ] Display designations in a table with columns: Title, Practice, Level, Status, Actions
- [ ] Master Admin sees all designations across all practices
- [ ] Practice Admin sees designations for their practice only
- [ ] Display designation count
- [ ] Show active and inactive designations with status badges
- [ ] Default sorting by title (ascending)
- [ ] Empty state message when no designations exist

### UI Elements:
- Designations table with sortable columns
- Designation count badge
- Status indicator (active/inactive)
- Action menu for each row
- "Add Designation" button

### Business Rules:
- Designation levels: Junior, Mid-Level, Senior, Lead
- Each practice can have custom designations
- Designation titles can be: SSE, ML, TL, ASE, etc.

---

## US-005.3: Add New Designation
**As a** Master Admin or Practice Admin  
**I want to** create a new designation  
**So that** candidates and opportunities can be mapped to appropriate levels

### Acceptance Criteria:
- [ ] "Add Designation" button opens create designation form
- [ ] Form fields: Title (required), Practice (dropdown, required), Level (dropdown, optional), Description (textarea, optional)
- [ ] Title field validates minimum 2, maximum 50 characters
- [ ] Practice dropdown filtered by user permissions (Master Admin: all, Practice Admin: assigned practice)
- [ ] Level dropdown options: Junior, Mid-Level, Senior, Lead
- [ ] "Create" button enabled when required fields valid
- [ ] "Cancel" button closes form
- [ ] Success message displays created designation details
- [ ] New designation appears in list immediately

### UI Elements:
- "Add Designation" button (primary action)
- Modal form with fields:
  - Title (text input, required)
  - Practice (dropdown, required)
  - Level (dropdown, optional)
  - Description (textarea, optional)
- Create button (primary)
- Cancel button (secondary)
- Success notification

### Business Rules:
- Designation title must be unique within a practice
- Practice Admin can only create designations for their practice
- Master Admin can create designations for any practice
- System-generated DesignationID (GUID)

---

## US-005.4: Edit Designation
**As a** Master Admin or Practice Admin  
**I want to** edit designation details  
**So that** I can update designation information when needed

### Acceptance Criteria:
- [ ] "Edit" action opens edit form with pre-filled data
- [ ] Allow editing: Title, Level, Description
- [ ] Practice cannot be changed after creation (read-only)
- [ ] Title uniqueness validated within practice
- [ ] "Save" button updates designation
- [ ] Success message confirms update
- [ ] Updated designation reflected in list

### UI Elements:
- Edit form modal with pre-filled fields
- Practice field (read-only)
- Save and Cancel buttons
- Success notification

---

## US-005.5: Delete/Deactivate Designation
**As a** Master Admin or Practice Admin  
**I want to** deactivate a designation  
**So that** it's not available for new assignments

### Acceptance Criteria:
- [ ] "Delete" or "Deactivate" action available in row menu
- [ ] Confirmation dialog explains impact (cannot be used for new opportunities/candidates)
- [ ] Check for dependencies (existing opportunities or candidates)
- [ ] If dependencies exist, show warning and list of dependent items
- [ ] Upon confirmation, designation IsActive set to false
- [ ] Deactivated designation shown with "Inactive" badge
- [ ] Success message confirms deactivation

### UI Elements:
- Delete/Deactivate button
- Confirmation dialog with dependency check
- Warning message for dependencies
- Success notification

### Business Rules:
- Cannot delete designation with active dependencies
- Deactivation is soft delete (IsActive = false)
- Deactivated designations not shown in dropdowns for new items

---

## US-005.6: Search and Filter Designations
**As a** Master Admin or Practice Admin  
**I want to** search and filter designations  
**So that** I can quickly find specific designations

### Acceptance Criteria:
- [ ] Search box for designation title
- [ ] Filter by practice (Master Admin only)
- [ ] Filter by level (Junior, Mid-Level, Senior, Lead)
- [ ] Filter by status (Active, Inactive, All)
- [ ] Clear filters button
- [ ] Results count display

### UI Elements:
- Search input
- Practice filter dropdown
- Level filter dropdown
- Status filter dropdown
- Clear filters button

---

## US-005.7: View Job Description List
**As a** Master Admin or Practice Admin  
**I want to** view all job descriptions  
**So that** I can see available JDs for opportunities

### Acceptance Criteria:
- [ ] Display JDs in a table with columns: Title, Designation, Practice, Status, Actions
- [ ] Master Admin sees all JDs across all practices
- [ ] Practice Admin sees JDs for their practice only
- [ ] Display JD count
- [ ] Show active and inactive JDs with status badges
- [ ] Default sorting by title (ascending)
- [ ] Empty state message when no JDs exist

### UI Elements:
- JD table with sortable columns
- JD count badge
- Status indicator
- Action menu for each row
- "Add JD" button

---

## US-005.8: Add New Job Description
**As a** Master Admin or Practice Admin  
**I want to** create a new job description  
**So that** hiring opportunities have detailed requirement information

### Acceptance Criteria:
- [ ] "Add JD" button opens create JD form
- [ ] Form fields: Title (required), Designation (dropdown, required), Description (textarea, required), Requirements (dynamic list, required)
- [ ] Title field validates minimum 5, maximum 100 characters
- [ ] Designation dropdown filtered by practice (shows designations of selected practice)
- [ ] Practice dropdown (required) - determines available designations
- [ ] Description field is rich text editor (supports formatting)
- [ ] Requirements section allows adding multiple requirement items
- [ ] "Add Requirement" button adds new requirement input field
- [ ] Each requirement can be removed individually
- [ ] Minimum 1 requirement mandatory
- [ ] "Create" button enabled when all required fields valid
- [ ] Success message displays created JD details

### UI Elements:
- "Add JD" button (primary action)
- Modal/page form with fields:
  - Title (text input, required)
  - Practice (dropdown, required)
  - Designation (dropdown, required, filtered by practice)
  - Description (rich text editor, required)
  - Requirements (dynamic list):
    - Requirement text input
    - Add Requirement button
    - Remove button for each requirement
- Create button (primary)
- Cancel button (secondary)
- Success notification

### Business Rules:
- JD title must be unique within a practice
- Description should detail job responsibilities and expectations
- Requirements can include skills, experience, education, etc.
- Practice determines which designations are available
- System-generated JobDescriptionID (GUID)

---

## US-005.9: Edit Job Description
**As a** Master Admin or Practice Admin  
**I want to** edit job description details  
**So that** I can update JD information as requirements change

### Acceptance Criteria:
- [ ] "Edit" action opens edit form with pre-filled data
- [ ] Allow editing: Title, Description, Requirements
- [ ] Designation and Practice cannot be changed (read-only)
- [ ] Requirements list shows existing items with ability to add/remove
- [ ] Title uniqueness validated within practice
- [ ] "Save" button updates JD
- [ ] Success message confirms update
- [ ] Updated JD reflected in list

### UI Elements:
- Edit form with pre-filled fields
- Read-only Designation and Practice fields
- Dynamic requirements list
- Save and Cancel buttons
- Success notification

---

## US-005.10: View Job Description Details
**As a** Master Admin or Practice Admin  
**I want to** view complete job description details  
**So that** I can review full JD content

### Acceptance Criteria:
- [ ] Clicking JD title or "View" action opens detail modal/page
- [ ] Display all JD information: Title, Designation, Practice, Description, Requirements list
- [ ] Show audit information: Created Date, Modified Date
- [ ] Display associated opportunities using this JD
- [ ] "Edit" and "Delete" buttons available (if permissions allow)
- [ ] "Close" button returns to JD list

### UI Elements:
- JD detail modal/page
- Information sections: Basic Info, Description, Requirements, Associated Opportunities, Audit Info
- Action buttons: Edit, Delete, Close

---

## US-005.11: Delete/Deactivate Job Description
**As a** Master Admin or Practice Admin  
**I want to** deactivate a job description  
**So that** it's not available for new opportunities

### Acceptance Criteria:
- [ ] "Delete" or "Deactivate" action available
- [ ] Confirmation dialog explains impact
- [ ] Check for active opportunities using this JD
- [ ] If active opportunities exist, show warning and list
- [ ] If no active dependencies, allow deactivation
- [ ] Upon confirmation, JD IsActive set to false
- [ ] Deactivated JD shown with "Inactive" badge
- [ ] Success message confirms deactivation

### UI Elements:
- Delete/Deactivate button
- Confirmation dialog with dependency check
- Warning message for dependencies
- Success notification

### Business Rules:
- Cannot deactivate JD with active hiring opportunities
- Can deactivate if opportunities are closed/completed
- Deactivation is soft delete (IsActive = false)

---

## US-005.12: Search and Filter Job Descriptions
**As a** Master Admin or Practice Admin  
**I want to** search and filter job descriptions  
**So that** I can quickly find specific JDs

### Acceptance Criteria:
- [ ] Search box for JD title or keywords in description
- [ ] Filter by practice (Master Admin only)
- [ ] Filter by designation
- [ ] Filter by status (Active, Inactive, All)
- [ ] Clear filters button
- [ ] Results count display

### UI Elements:
- Search input
- Practice filter dropdown
- Designation filter dropdown
- Status filter dropdown
- Clear filters button

---

## US-005.13: Copy/Duplicate Job Description
**As a** Master Admin or Practice Admin  
**I want to** duplicate an existing job description  
**So that** I can create similar JDs quickly

### Acceptance Criteria:
- [ ] "Duplicate" action available in JD row menu
- [ ] Clicking duplicate opens create form pre-filled with source JD data
- [ ] Title automatically appended with " (Copy)"
- [ ] All fields editable
- [ ] User must save to create duplicate
- [ ] Success message confirms creation

### UI Elements:
- Duplicate button/action
- Create form with pre-filled data
- Modified title field
- Create and Cancel buttons

---

## US-005.14: Sort and Pagination
**As a** Master Admin or Practice Admin  
**I want to** sort and paginate designation and JD lists  
**So that** I can navigate large lists efficiently

### Acceptance Criteria:
- [ ] Sortable columns for both designations and JDs
- [ ] Pagination controls at bottom of tables
- [ ] Page size options: 10, 20, 50
- [ ] Default: 20 items per page
- [ ] Total count display

### UI Elements:
- Sort indicators in column headers
- Pagination controls
- Page size dropdown

---

## Technical Notes:
- Use rich text editor (e.g., Quill, TinyMCE) for JD description
- Implement real-time validation for title uniqueness
- Cache designation and practice lists for dropdown population
- Log all designation and JD management actions
- Implement responsive table design with horizontal scroll on mobile
- Support bulk import of designations and JDs (future enhancement)

## Related Functional Requirements:
- FR#Designation Management
- FR#Job Description Management
- FR#LUR (Lookup Retrieval for designation-related lookups)

## Priority: P1 (High)
## Estimated Story Points: 13
