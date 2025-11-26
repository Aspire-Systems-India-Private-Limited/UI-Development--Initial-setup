# User Stories: Candidate Profile Management Screen

## Module: Candidate Profile Management
**Reference:** Figma_All_Screens.md - Section 9 (Candidate Profile Management Screen)  
**Related FR:** FR#CPM-1 to FR#CPM-4

---

## US-009.1: View Candidate Profiles List
**As a** Master Admin or TA Team Admin  
**I want to** view all candidate profiles  
**So that** I can see candidates in the recruitment pipeline

### Acceptance Criteria:
- [ ] Display candidates in a table with columns: Name, Email, Phone, Opportunity, Designation, Status, Actions
- [ ] Master Admin sees all candidates across all practices
- [ ] TA Team Admin sees candidates for their assigned practice opportunities
- [ ] Display candidate count at the top
- [ ] Show status badges: Pending (yellow), Scheduled (blue), Completed (green), Rejected (red)
- [ ] Default sorting by created date (newest first)
- [ ] Empty state message when no candidates exist

### UI Elements:
- Candidates table with sortable columns
- Candidate count badge
- Status indicator badges
- Action menu for each row
- "Add Candidate" button
- Empty state illustration

### Business Rules:
- Master Admin: View all candidates
- TA Team Admin: View candidates in assigned practice scope
- Practice Admin: View candidates for practice opportunities
- Display both active and inactive candidates with filter

### Related FR: FR#CPM-2 – Retrieve Candidate Profiles

---

## US-009.2: Search and Filter Candidates
**As a** Master Admin or TA Team Admin  
**I want to** search and filter candidates  
**So that** I can quickly find specific candidates

### Acceptance Criteria:
- [ ] Search box allows searching by name, email, or phone
- [ ] Search results update as user types (debounced)
- [ ] Filter by opportunity (dropdown)
- [ ] Filter by designation (dropdown)
- [ ] Filter by status (dropdown: All, Pending, Scheduled, Completed, Rejected)
- [ ] Filter by years of experience range (min, max)
- [ ] Filter by candidate source (Referred, LinkedIn, Naukri, etc.)
- [ ] Filter by assigned TA member (dropdown)
- [ ] Multiple filters can be applied simultaneously
- [ ] "Clear Filters" button resets all filters
- [ ] Display count of filtered results

### UI Elements:
- Search input field
- Opportunity filter dropdown
- Designation filter dropdown
- Status filter dropdown
- Experience range inputs (min, max)
- Candidate source filter dropdown
- TA member filter dropdown
- Clear Filters button
- Results count label

---

## US-009.3: Create New Candidate Profile
**As a** TA Team Admin  
**I want to** create a new candidate profile  
**So that** candidates can be scheduled for interviews

### Acceptance Criteria:
- [ ] "Add Candidate" button opens create candidate form
- [ ] Form displays all required fields with validation
- [ ] Hiring Opportunity dropdown (required, filtered by practice)
- [ ] First Name field (min 1, max 50 characters, required)
- [ ] Last Name field (min 1, max 50 characters, required)
- [ ] Email field (valid email format, max 250 characters, required, unique)
- [ ] Phone field (optional, valid format if provided)
- [ ] Designation Applied For dropdown (required, filtered by opportunity)
- [ ] Designation Presented For dropdown (optional, same filter as above)
- [ ] Years of Experience field (number, positive, required)
- [ ] Candidate Source dropdown (Referred, LinkedIn, Naukri, Direct, Other, required)
- [ ] Resume Document upload (PDF/DOC/DOCX, max 5MB, required)
- [ ] Mapped TA Team Member dropdown (required, defaults to current user)
- [ ] Source dropdown (Web, Mobile, API, Admin, required)
- [ ] "Create" button enabled when all required fields valid
- [ ] "Cancel" button closes form without saving
- [ ] Display validation errors inline
- [ ] Resume upload with progress indicator
- [ ] Success notification shows created candidate ID
- [ ] New candidate appears in list immediately

### UI Elements:
- "Add Candidate" button (primary action)
- Modal/page form with fields:
  - HiringOpportunityID (dropdown, required)
  - FirstName (text input, required)
  - LastName (text input, required)
  - EmailID (email input, required)
  - PhoneNumber (text input, optional)
  - DesignationAppliedFor (dropdown, required)
  - DesignationPresentedFor (dropdown, optional)
  - YearsOfExperience (number input, required)
  - CandidateSource (dropdown, required)
  - ResumeDocument (file upload, required)
  - MappedTATeamMemberID (dropdown, required)
  - Source (dropdown, required)
- Create button (primary)
- Cancel button (secondary)
- Inline validation messages
- File upload component with progress bar
- Success toast notification

### Business Rules:
- Email must be unique across all candidates
- Phone number must be unique if provided
- Resume document must be PDF, DOC, or DOCX format
- Maximum file size: 5MB
- TA Team Admin can only create candidates for opportunities in their practice
- Master Admin can create candidates for any opportunity
- System-generated CandidateProfileID (GUID)
- CreatedDate and ModifiedDate set to current timestamp
- ModUser set to current user ID
- Status defaults to "Pending"

### Related FR: FR#CPM-1 – Create Candidate Profile

---

## US-009.4: View Candidate Profile Details
**As a** Master Admin or TA Team Admin  
**I want to** view detailed information about a candidate  
**So that** I can see complete candidate information and progress

### Acceptance Criteria:
- [ ] Clicking candidate name or "View" action opens detail modal/page
- [ ] Display all candidate information: Name, Email, Phone, Opportunity, Designations, Experience, Source
- [ ] Show mapped TA team member details
- [ ] Display resume document with download option
- [ ] Show interview schedule history (past and upcoming)
- [ ] Display interview feedback summaries
- [ ] Show current status and status history
- [ ] Display audit information: Created Date, Modified Date
- [ ] "Edit", "Schedule Interview", and "Deactivate" buttons available (if permissions allow)
- [ ] "Download Resume" button for resume access
- [ ] "Close" button returns to candidate list

### UI Elements:
- Candidate detail modal/page
- Information sections: Personal Info, Opportunity & Designation, Experience & Source, Resume, Interview History, Feedback, Status History, Audit Info
- Action buttons: Edit, Schedule Interview, Deactivate, Download Resume, Close
- Interview history table
- Feedback cards
- Status timeline

---

## US-009.5: Edit Candidate Profile
**As a** TA Team Admin  
**I want to** edit candidate information  
**So that** I can update candidate details when needed

### Acceptance Criteria:
- [ ] "Edit" button in candidate row or detail view opens edit form
- [ ] Form pre-populated with existing candidate data
- [ ] Allow editing: FirstName, LastName, EmailID, PhoneNumber, DesignationAppliedFor, DesignationPresentedFor, YearsOfExperience, CandidateSource
- [ ] Hiring Opportunity cannot be changed (read-only)
- [ ] Resume can be replaced with new upload
- [ ] Email uniqueness validated (excluding current candidate)
- [ ] Phone uniqueness validated if changed
- [ ] "Save" button updates candidate
- [ ] "Cancel" button discards changes
- [ ] Audit fields updated automatically (ModifiedDate, ModUser)
- [ ] Success message confirms update
- [ ] Updated candidate reflected in list

### UI Elements:
- Edit form modal with pre-filled fields
- Read-only Hiring Opportunity field
- File upload component for resume replacement
- Save button (primary)
- Cancel button (secondary)
- Success notification

### Business Rules:
- Cannot change hiring opportunity after creation
- Email must remain unique
- Phone must remain unique if changed
- Resume replacement is optional (keeps existing if not replaced)
- Cannot edit if candidate has completed interviews (or specific restrictions)

### Related FR: FR#CPM-3 – Update Candidate Profile

---

## US-009.6: Download Candidate Resume
**As a** TA Team Admin or Panel Member  
**I want to** download candidate resume  
**So that** I can review candidate qualifications

### Acceptance Criteria:
- [ ] "Download Resume" button available in candidate detail view
- [ ] Clicking button downloads resume file
- [ ] File downloaded with original filename or standard naming (CandidateName_Resume.ext)
- [ ] Download works for all supported formats (PDF, DOC, DOCX)
- [ ] Success message confirms download
- [ ] Download logged for audit purposes

### UI Elements:
- Download Resume button with icon
- Download progress indicator
- Success notification

### Business Rules:
- Panel members can download resumes for candidates they're scheduled to interview
- TA and Admin roles can download any candidate resume
- Resume access logged for compliance

---

## US-009.7: Deactivate Candidate Profile
**As a** TA Team Admin  
**I want to** deactivate a candidate profile  
**So that** inactive candidates are not shown in active lists

### Acceptance Criteria:
- [ ] "Deactivate" action available in candidate menu
- [ ] Clicking "Deactivate" displays confirmation dialog
- [ ] Deactivation reason required (dropdown: Candidate Withdrew, Rejected, Position Filled, Other)
- [ ] If "Other" selected, text field for reason details appears
- [ ] Check for scheduled interviews (not yet completed)
- [ ] If scheduled interviews exist, show warning and list
- [ ] User must confirm deactivation
- [ ] Upon confirmation, candidate IsActive set to false
- [ ] Deactivation details recorded
- [ ] Success message confirms deactivation
- [ ] Deactivated candidate shown with "Inactive" badge
- [ ] Deactivated candidates not shown in dropdowns

### UI Elements:
- Deactivate button
- Confirmation dialog with reason field
- Warning message for scheduled interviews
- Success notification

### Business Rules:
- Deactivation reason is mandatory
- Deactivation is soft delete (IsActive = false)
- Cannot schedule new interviews for deactivated candidates
- Existing scheduled interviews remain (must be cancelled separately if needed)
- Deactivated candidates still viewable with filter

### Related FR: FR#CPM-4 – Deactivate Candidate Profile

---

## US-009.8: Reactivate Candidate Profile
**As a** Master Admin or TA Team Admin  
**I want to** reactivate a previously deactivated candidate  
**So that** they can be considered for interviews again

### Acceptance Criteria:
- [ ] "Reactivate" button available for inactive candidates
- [ ] Clicking "Reactivate" displays confirmation dialog
- [ ] Reactivation reason optional
- [ ] Upon confirmation, candidate IsActive set to true
- [ ] Status set to "Pending"
- [ ] Reactivated candidate appears as active in list
- [ ] Success message confirms reactivation

### UI Elements:
- Reactivate button (for inactive candidates)
- Confirmation dialog
- Success notification

---

## US-009.9: Update Candidate Status
**As a** TA Team Admin  
**I want to** update candidate status manually  
**So that** recruitment progress is accurately reflected

### Acceptance Criteria:
- [ ] "Update Status" action in candidate menu
- [ ] Status dropdown: Pending, Scheduled, Completed, Selected, Rejected, On Hold
- [ ] Reason field for status change (optional for some statuses, required for others)
- [ ] Status change triggers appropriate notifications
- [ ] Status history recorded
- [ ] Success message confirms status update

### UI Elements:
- Update Status button/action
- Status selection modal
- Status dropdown
- Reason textarea
- Save and Cancel buttons
- Success notification

### Business Rules:
- Status transitions follow workflow rules (e.g., Pending → Scheduled → Completed)
- Some status changes require interviews to be completed
- Status change notifications sent to relevant stakeholders
- Status history maintained for audit

---

## US-009.10: View Interview Schedule for Candidate
**As a** TA Team Admin  
**I want to** see all interviews scheduled for a candidate  
**So that** I can track interview progress

### Acceptance Criteria:
- [ ] "Interview Schedule" tab/section in candidate detail view
- [ ] Display interviews in a table: Date/Time, Panel Member, Interview Type, Level, Status, Feedback Status
- [ ] Show upcoming and past interviews
- [ ] Filter by status (Scheduled, Completed, Cancelled, Rescheduled)
- [ ] Click interview to view details
- [ ] "Schedule New Interview" button available
- [ ] Color coding for interview status

### UI Elements:
- Interview Schedule tab/section
- Interviews table
- Status filter
- Schedule New Interview button
- View Details link

---

## US-009.11: Schedule Interview from Candidate Profile
**As a** TA Team Admin  
**I want to** schedule an interview directly from candidate profile  
**So that** I can quickly schedule interviews

### Acceptance Criteria:
- [ ] "Schedule Interview" button in candidate detail view
- [ ] Opens interview scheduling form with candidate pre-selected
- [ ] Form includes all scheduling fields (covered in Interview Scheduling user stories)
- [ ] Save schedules interview and returns to candidate profile
- [ ] Success message confirms scheduling
- [ ] Interview appears in candidate's interview schedule

### UI Elements:
- Schedule Interview button
- Interview scheduling form modal
- Success notification

---

## US-009.12: View Candidate Feedback Summary
**As a** TA Team Admin or Practice Admin  
**I want to** view feedback summaries for a candidate  
**So that** I can evaluate candidate performance

### Acceptance Criteria:
- [ ] "Feedback" tab/section in candidate detail view
- [ ] Display feedback from all completed interviews
- [ ] Show feedback summary: Interview Date, Panel Member, Rating, Decision, Comments
- [ ] Click feedback to view full details
- [ ] Overall rating/decision summary displayed
- [ ] Filter feedback by interview round or panel member

### UI Elements:
- Feedback tab/section
- Feedback cards/table
- Overall rating summary
- View Full Feedback link

---

## US-009.13: Sort Candidates List
**As a** system user  
**I want to** sort candidates by different columns  
**So that** I can organize candidates meaningfully

### Acceptance Criteria:
- [ ] Sortable columns: Name, Email, Opportunity, Designation, Status, Experience, Created Date
- [ ] Click column header to sort ascending, click again for descending
- [ ] Sort indicator displayed
- [ ] Default sort: Created Date (newest first)
- [ ] Sort persists during pagination

### UI Elements:
- Sort indicators in column headers

---

## US-009.14: Pagination for Candidates List
**As a** system user  
**I want to** navigate through pages of candidates  
**So that** I can view large lists efficiently

### Acceptance Criteria:
- [ ] Display 20 candidates per page by default
- [ ] Page size selector: 10, 20, 50
- [ ] Page navigation controls
- [ ] Display current page and total pages
- [ ] Display total candidate count

### UI Elements:
- Pagination controls at bottom of table
- Page size dropdown

---

## US-009.15: Export Candidates List
**As a** TA Team Admin  
**I want to** export candidate information  
**So that** I can use data for reporting and analysis

### Acceptance Criteria:
- [ ] "Export" button available above candidate table
- [ ] Export format options: CSV, Excel
- [ ] Exported file includes: Name, Email, Phone, Opportunity, Designation, Status, Experience, Source, Created Date
- [ ] Export respects current filters/search
- [ ] File name format: Candidates_YYYYMMDD_HHMMSS
- [ ] Download starts automatically

### UI Elements:
- Export button with format dropdown
- Success notification

---

## US-009.16: Bulk Import Candidates
**As a** TA Team Admin  
**I want to** import multiple candidates from a file  
**So that** I can efficiently add many candidates at once

### Acceptance Criteria:
- [ ] "Import Candidates" button opens import modal
- [ ] Download template option (CSV/Excel template)
- [ ] File upload component (CSV or Excel)
- [ ] File validation (format, required columns)
- [ ] Preview imported data before confirmation
- [ ] Error reporting for invalid rows
- [ ] "Import" button processes file
- [ ] Success message shows count of imported candidates
- [ ] Error summary for failed imports

### UI Elements:
- Import Candidates button
- Import modal with file upload
- Download Template link
- Data preview table
- Import button (primary)
- Error report display
- Success notification

### Business Rules:
- Template includes all required fields
- Email and phone uniqueness validated
- Invalid rows skipped with error report
- Resumes must be uploaded separately after import
- Maximum import size: 100 candidates per file

---

## US-009.17: Send Communication to Candidate
**As a** TA Team Admin  
**I want to** send emails to candidates  
**So that** I can communicate interview schedules and updates

### Acceptance Criteria:
- [ ] "Send Email" action in candidate menu
- [ ] Opens email composition modal
- [ ] Email templates available (Interview Invitation, Rejection, etc.)
- [ ] Recipient pre-filled with candidate email
- [ ] Subject and body editable
- [ ] "Send" button sends email
- [ ] Email history recorded
- [ ] Success message confirms email sent

### UI Elements:
- Send Email button
- Email composition modal
- Template selector
- Subject and body fields
- Send button
- Success notification

---

## Technical Notes:
- Implement secure file upload with virus scanning
- Store resume documents in secure storage (cloud storage)
- Generate signed URLs for resume downloads
- Validate email uniqueness at server-side
- Log all candidate management actions for audit
- Implement GDPR-compliant data handling for candidate PII
- Consider candidate portal for self-service (future enhancement)
- Integrate with email service for automated notifications

## Related Functional Requirements:
- FR#CPM-1 – Create Candidate Profile
- FR#CPM-2 – Retrieve Candidate Profiles
- FR#CPM-3 – Update Candidate Profile
- FR#CPM-4 – Deactivate Candidate Profile

## Priority: P0 (Critical)
## Estimated Story Points: 13
