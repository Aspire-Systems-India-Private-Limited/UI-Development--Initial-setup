# User Stories: Interview Scheduling Screen

## Module: Interview Schedule Management
**Reference:** Figma_All_Screens.md - Section 10 (Interview Scheduling Screen)  
**Related FR:** FR#Interview Schedule Management

---

## US-010.1: View Interview Schedule List
**As a** TA Team Admin, Practice Admin, or Panel Member  
**I want to** view all scheduled interviews  
**So that** I can see upcoming and past interviews

### Acceptance Criteria:
- [ ] Display interviews in a table with columns: Candidate, Opportunity, Panel Member, Date/Time, Type, Level, Status, Actions
- [ ] TA Team Admin sees interviews for their practice scope
- [ ] Practice Admin sees interviews for their practice
- [ ] Panel Members see only their own interviews
- [ ] Master Admin sees all interviews
- [ ] Display interview count at the top
- [ ] Show status badges: Scheduled (blue), Completed (green), Cancelled (red), Rescheduled (yellow)
- [ ] Default sorting by scheduled date/time (upcoming first)
- [ ] Empty state message when no interviews exist

### UI Elements:
- Interview schedule table with sortable columns
- Interview count badge
- Status indicator badges
- Action menu for each row
- "Schedule Interview" button
- Calendar view toggle
- Empty state illustration

### Business Rules:
- Panel Members: View only assigned interviews
- TA Team Admin: View interviews for practice-scoped candidates
- Practice Admin: View interviews for practice panel members
- Master Admin: View all interviews

---

## US-010.2: View Interview Schedule - Calendar View
**As a** TA Team Admin or Panel Member  
**I want to** view interviews in a calendar format  
**So that** I can see schedule at a glance

### Acceptance Criteria:
- [ ] Calendar view displays interviews as events
- [ ] Each event shows: Candidate name, Panel member, Time
- [ ] Color coding by status: Scheduled, Completed, Cancelled
- [ ] Month, week, and day views available
- [ ] Click event to view interview details
- [ ] "Today" button navigates to current date
- [ ] View toggle to switch between Calendar and Table views
- [ ] Filter controls available

### UI Elements:
- Month/Week/Day calendar views
- Interview event cards
- Color-coded status indicators
- View toggle (Calendar/Table)
- Today button
- Filter panel

---

## US-010.3: Schedule New Interview
**As a** TA Team Admin  
**I want to** schedule an interview for a candidate  
**So that** interviews can be conducted

### Acceptance Criteria:
- [ ] "Schedule Interview" button opens scheduling form
- [ ] Title field (optional, auto-generated from candidate and opportunity)
- [ ] Candidate Profile dropdown (required, searchable)
- [ ] Hiring Opportunity dropdown (required, filtered by selected candidate)
- [ ] Interview Type dropdown (Technical, HR, Managerial, required)
- [ ] Designation Level dropdown (based on candidate and opportunity)
- [ ] Panel Member dropdown (required, filtered by qualification and availability)
  - Shows only panel members qualified for selected level
  - Shows availability indicators
- [ ] Availability Slot dropdown (required, populated after panel member selection)
  - Shows available slots for selected panel member
  - Displays date, start time, end time
- [ ] Scheduled Date (auto-filled from selected slot, read-only)
- [ ] Scheduled Time From (auto-filled from selected slot, read-only)
- [ ] Scheduled Time To (auto-filled from selected slot, read-only)
- [ ] Status automatically set to "Scheduled"
- [ ] Notes textarea (optional)
- [ ] Source dropdown (Web, Mobile, API, Admin, required)
- [ ] "Schedule" button enabled when all required fields valid
- [ ] "Cancel" button closes form without saving
- [ ] Display validation errors inline
- [ ] Success notification shows scheduled interview ID
- [ ] Confirmation email sent to candidate and panel member
- [ ] New interview appears in schedule list/calendar

### UI Elements:
- "Schedule Interview" button (primary action)
- Modal/page form with fields:
  - Title (text input, optional)
  - CandidateProfileID (dropdown, required, searchable)
  - HiringOpportunityID (dropdown, required)
  - InterviewTypeID (dropdown, required)
  - DesignationLevel (dropdown, required)
  - TechnicalPanelMemberID (dropdown with availability, required)
  - AvailabilityID (dropdown, required)
  - ScheduledDate (date display, read-only)
  - ScheduledTimeslotFrom (time display, read-only)
  - ScheduledTimeslotTo (time display, read-only)
  - StatusID (auto-set to "Scheduled")
  - Notes (textarea, optional)
  - Source (dropdown, required)
- Schedule button (primary)
- Cancel button (secondary)
- Inline validation messages
- Success toast notification

### Business Rules:
- Can only schedule for candidates with "Pending" or "Scheduled" status
- Panel member must be qualified for designation level
- Must use available (not blocked/unavailable) slots
- Selected slot becomes "Scheduled" and unavailable for other interviews
- System-generated InterviewScheduleID (GUID)
- CreatedDate and ModifiedDate set to current timestamp
- ModUser set to current user ID
- Notifications sent to candidate and panel member
- Calendar invites generated

### Related FR: FR#Interview Schedule Management - Create Interview Schedule

---

## US-010.4: View Interview Details
**As a** TA Team Admin, Practice Admin, or Panel Member  
**I want to** view detailed information about an interview  
**So that** I can see complete interview information

### Acceptance Criteria:
- [ ] Clicking interview row or calendar event opens detail modal/page
- [ ] Display all interview information: Title, Candidate, Opportunity, Panel Member, Interview Type, Level
- [ ] Show scheduled date and time details
- [ ] Display candidate information and resume download link
- [ ] Show panel member contact information
- [ ] Display interview notes
- [ ] Show interview status and status history
- [ ] Display audit information: Created Date, Modified Date
- [ ] "Edit", "Reschedule", "Cancel", and "Submit Feedback" buttons available (based on status and permissions)
- [ ] "Close" button returns to interview list

### UI Elements:
- Interview detail modal/page
- Information sections: Interview Info, Candidate Info, Panel Member Info, Schedule Details, Notes, Status History, Audit Info
- Action buttons: Edit, Reschedule, Cancel, Submit Feedback, Close
- Download Resume link
- Status timeline

---

## US-010.5: Edit Interview Details
**As a** TA Team Admin  
**I want to** edit interview information  
**So that** I can update interview details before it's conducted

### Acceptance Criteria:
- [ ] "Edit" button in interview detail view opens edit form
- [ ] Form pre-populated with existing interview data
- [ ] Allow editing: Title, InterviewTypeID, Notes
- [ ] Cannot edit: Candidate, Opportunity, Panel Member, Date/Time (use Reschedule instead)
- [ ] "Save" button updates interview
- [ ] "Cancel" button discards changes
- [ ] Audit fields updated automatically
- [ ] Success message confirms update
- [ ] Notification sent to affected parties if significant changes

### UI Elements:
- Edit form modal with pre-filled fields
- Read-only fields for locked data
- Save and Cancel buttons
- Success notification

### Business Rules:
- Can only edit interviews with "Scheduled" status
- Cannot edit completed or cancelled interviews
- To change date/time/panel member, use Reschedule function
- ModifiedDate and ModUser updated on save

---

## US-010.6: Reschedule Interview
**As a** TA Team Admin or Panel Member  
**I want to** reschedule an interview  
**So that** conflicts and changes can be accommodated

### Acceptance Criteria:
- [ ] "Reschedule" button in interview detail view opens reschedule form
- [ ] Display current interview details (read-only)
- [ ] Reschedule Reason dropdown (Panel Unavailable, Candidate Request, Technical Issue, Other, required)
- [ ] If "Other" selected, reason details textarea appears
- [ ] New Panel Member dropdown (optional, shows only qualified members with availability)
- [ ] New Availability Slot dropdown (required if panel member changes, or required for same member)
- [ ] New scheduled date/time auto-filled from selected slot
- [ ] "Reschedule" button creates reschedule request
- [ ] Confirmation dialog explains impact (notifications sent, previous slot freed)
- [ ] Upon confirmation, reschedule processed:
  - Original interview status changed to "Rescheduled"
  - New interview schedule created (linked to original)
  - Previous slot freed (becomes available again)
  - New slot marked as scheduled
  - Reschedule request record created
- [ ] Success message confirms rescheduling
- [ ] Notifications sent to candidate and panel members (old and new if changed)
- [ ] Updated interview appears in schedule

### UI Elements:
- Reschedule button
- Reschedule form modal
- Current interview details display
- Reason dropdown
- Reason details textarea
- New panel member dropdown (optional)
- New slot dropdown
- New schedule details display
- Reschedule button (primary)
- Cancel button (secondary)
- Confirmation dialog
- Success notification

### Business Rules:
- Can reschedule interviews with "Scheduled" status
- Cannot reschedule completed or cancelled interviews
- Reschedule reason is mandatory
- Original slot becomes available again
- New slot must be available
- If panel member changes, new member must be qualified for level
- Reschedule history maintained
- InterviewRescheduleRequest record created for tracking
- Candidate and panel members notified
- Calendar invites updated

### Related FR: FR#Interview Reschedule Requests

---

## US-010.7: Cancel Interview
**As a** TA Team Admin or Panel Member  
**I want to** cancel an interview  
**So that** cancelled interviews are properly recorded

### Acceptance Criteria:
- [ ] "Cancel" button in interview detail view opens cancellation confirmation
- [ ] Cancellation reason dropdown (Candidate Withdrew, Panel Unavailable, Position Filled, Other, required)
- [ ] If "Other" selected, reason details textarea appears
- [ ] Confirmation dialog warns about cancellation
- [ ] Upon confirmation:
  - Interview status changed to "Cancelled"
  - Scheduled slot freed (becomes available again)
  - Cancellation reason and date recorded
  - Candidate status updated if applicable
- [ ] Success message confirms cancellation
- [ ] Notifications sent to candidate and panel member
- [ ] Cancelled interview appears with "Cancelled" badge

### UI Elements:
- Cancel button
- Cancellation confirmation dialog
- Reason dropdown
- Reason details textarea
- Confirm and Cancel buttons
- Success notification

### Business Rules:
- Can only cancel interviews with "Scheduled" status
- Cannot cancel completed interviews
- Cancellation reason is mandatory
- Slot becomes available for other interviews
- Cancellation recorded in audit trail
- Candidate and panel member notified
- Calendar invites cancelled
- Candidate status may change based on cancellation context

---

## US-010.8: Mark Interview as Completed
**As a** TA Team Admin or Panel Member  
**I want to** mark an interview as completed  
**So that** interview progress is tracked

### Acceptance Criteria:
- [ ] "Mark as Completed" button available for scheduled interviews (on or after scheduled date)
- [ ] Clicking button displays confirmation
- [ ] Upon confirmation, interview status changed to "Completed"
- [ ] Completion timestamp recorded
- [ ] Success message confirms completion
- [ ] Panel member prompted to submit feedback
- [ ] Candidate status updated if all interviews completed

### UI Elements:
- Mark as Completed button
- Confirmation dialog
- Success notification
- Feedback submission prompt

### Business Rules:
- Can only mark as completed on or after scheduled date
- Cannot mark as completed if already completed or cancelled
- Completion triggers feedback reminder
- Slot remains in "used" state
- Candidate status may advance if all rounds completed

---

## US-010.9: Search and Filter Interviews
**As a** TA Team Admin, Practice Admin, or Panel Member  
**I want to** search and filter interviews  
**So that** I can find specific interviews quickly

### Acceptance Criteria:
- [ ] Search box allows searching by candidate name, panel member name
- [ ] Search results update as user types (debounced)
- [ ] Filter by candidate (dropdown, searchable)
- [ ] Filter by panel member (dropdown)
- [ ] Filter by opportunity (dropdown)
- [ ] Filter by interview type (Technical, HR, Managerial)
- [ ] Filter by status (Scheduled, Completed, Cancelled, Rescheduled)
- [ ] Filter by date range (start date, end date)
- [ ] Multiple filters can be applied simultaneously
- [ ] "Clear Filters" button resets all filters
- [ ] Display count of filtered results

### UI Elements:
- Search input field
- Candidate filter dropdown
- Panel member filter dropdown
- Opportunity filter dropdown
- Interview type filter dropdown
- Status filter dropdown
- Date range pickers
- Clear Filters button
- Results count label

---

## US-010.10: View Upcoming Interviews
**As a** Panel Member  
**I want to** see my upcoming interviews  
**So that** I can prepare for them

### Acceptance Criteria:
- [ ] "My Upcoming Interviews" view shows only logged-in panel member's scheduled interviews
- [ ] Display interviews for next 7 days by default
- [ ] Show interview cards with: Candidate name, Date/Time, Designation, Interview Type
- [ ] Click card to view full details
- [ ] "Download Resume" quick action on card
- [ ] Countdown timer for interviews within 24 hours
- [ ] "View All" link to see full schedule

### UI Elements:
- Upcoming Interviews section/widget
- Interview cards with key info
- Countdown timer
- Quick action buttons
- View All link

---

## US-010.11: View Interview History
**As a** TA Team Admin or Panel Member  
**I want to** view past interviews  
**So that** I can review interview history

### Acceptance Criteria:
- [ ] "Interview History" view shows completed and cancelled interviews
- [ ] Filter by date range
- [ ] Filter by status (Completed, Cancelled)
- [ ] Display feedback status for completed interviews
- [ ] Click interview to view details including feedback

### UI Elements:
- Interview History tab/section
- Date range filter
- Status filter
- Interview table with feedback indicator

---

## US-010.12: Send Interview Reminders
**As a** TA Team Admin  
**I want to** send reminders about upcoming interviews  
**So that** participants are reminded

### Acceptance Criteria:
- [ ] "Send Reminder" action available for scheduled interviews
- [ ] Reminder sent to candidate and/or panel member (selectable)
- [ ] Email and in-app notification sent
- [ ] Reminder includes interview details and joining information
- [ ] Success message confirms reminder sent
- [ ] Reminder history recorded

### UI Elements:
- Send Reminder button/action
- Recipient selection (checkboxes for candidate, panel member)
- Send button
- Success notification

### Business Rules:
- Automated reminders: 24 hours and 2 hours before interview
- Manual reminders can be sent anytime
- Reminders include all interview details

---

## US-010.13: Bulk Reschedule/Cancel
**As a** TA Team Admin  
**I want to** reschedule or cancel multiple interviews at once  
**So that** I can handle mass changes efficiently

### Acceptance Criteria:
- [ ] Checkbox selection in interview table
- [ ] "Bulk Actions" dropdown appears when interviews selected
- [ ] Bulk actions: Reschedule, Cancel
- [ ] Bulk reschedule opens form for common reason and action
- [ ] Bulk cancel requires reason
- [ ] Confirmation dialog shows count and list of affected interviews
- [ ] Success message shows count of processed interviews
- [ ] Notifications sent to all affected parties

### UI Elements:
- Selection checkboxes
- Bulk Actions dropdown
- Bulk action form/dialog
- Confirmation dialog with list
- Success notification

---

## US-010.14: Sort Interviews List
**As a** system user  
**I want to** sort interviews by different columns  
**So that** I can organize interviews meaningfully

### Acceptance Criteria:
- [ ] Sortable columns: Date/Time, Candidate, Panel Member, Status, Interview Type
- [ ] Click column header to sort
- [ ] Sort indicator displayed
- [ ] Default sort: Scheduled Date/Time (upcoming first)

### UI Elements:
- Sort indicators in column headers

---

## US-010.15: Pagination for Interviews List
**As a** system user  
**I want to** navigate through pages of interviews  
**So that** I can view large lists efficiently

### Acceptance Criteria:
- [ ] Display 20 interviews per page by default
- [ ] Page size selector: 10, 20, 50
- [ ] Page navigation controls
- [ ] Display current page and total pages

### UI Elements:
- Pagination controls at bottom of table

---

## US-010.17: View Interview Timeline
**As a** TA Team Admin  
**I want to** see a timeline view of interview schedules  
**So that** I can understand interview progression for candidates

### Acceptance Criteria:
- [ ] Timeline view shows interview rounds in chronological order
- [ ] Display for selected candidate or opportunity
- [ ] Show interview status, date, panel member, feedback status for each round
- [ ] Visual timeline with milestones
- [ ] Click milestone to view interview details

### UI Elements:
- Timeline visualization
- Interview milestones with status
- Detail view on click

---

## Technical Notes:
- Use full-featured calendar component for calendar view
- Implement cascading dropdowns with real-time availability checking
- Integrate with email service for notifications and calendar invites
- Implement conflict detection to prevent double-booking
- Use optimistic UI updates for better UX
- Log all scheduling actions for audit
- Consider video conferencing integration (Zoom, Teams) for virtual interviews
- Implement reminder job scheduler for automated reminders
- Handle time zone conversions if needed

## Related Functional Requirements:
- FR#Interview Schedule Management - Create, Update, Retrieve, Delete Schedules
- FR#Interview Reschedule Requests
- FR#Availability Management (slot availability)
- FR#Feedback Management (post-interview)

## Priority: P0 (Critical)
## Estimated Story Points: 21
