# User Stories: Interview Reschedule Request Screen

## Module: Interview Reschedule Request Management
**Reference:** Figma_All_Screens.md - Section 12 (Interview Reschedule Request Screen)  
**Related FR:** FR#Interview Reschedule Requests

---

## US-012.1: View Reschedule Request List
**As a** TA Team Admin or Practice Admin  
**I want to** view all interview reschedule requests  
**So that** I can manage rescheduling efficiently

### Acceptance Criteria:
- [ ] Display reschedule requests in a table with columns: Request ID, Interview (Candidate), Panel Member, Previous Date/Time, New Date/Time, Reason, Request Status, Actions
- [ ] TA Team Admin sees requests for practice-scoped interviews
- [ ] Practice Admin sees requests for practice panel members
- [ ] Master Admin sees all requests
- [ ] Display request count at the top
- [ ] Show status badges: Pending (yellow), Approved (green), Rejected (red)
- [ ] Default sorting by request date (newest first)
- [ ] Empty state message when no requests exist

### UI Elements:
- Reschedule requests table with sortable columns
- Request count badge
- Status indicator badges
- Action menu for each row
- Filter controls
- Empty state illustration

### Business Rules:
- TA Team Admin: View requests for candidates in practice scope
- Practice Admin: View requests for practice panel members
- Master Admin: View all requests
- Display both active and resolved requests with filter

---

## US-012.2: Create Reschedule Request (Panel Member Initiated)
**As a** Panel Member  
**I want to** request to reschedule an interview  
**So that** conflicts can be resolved

### Acceptance Criteria:
- [ ] "Request Reschedule" button available for scheduled interviews in panel member's schedule
- [ ] Opens reschedule request form
- [ ] Display current interview details (read-only): Candidate, Date/Time, Designation, Type
- [ ] Reschedule Reason dropdown (Panel Unavailable, Technical Issue, Personal Emergency, Other, required)
- [ ] If "Other" selected, reason details textarea appears (required)
- [ ] Proposed New Date/Time section:
  - Option 1: Select from my available slots (dropdown)
  - Option 2: Suggest new date/time (date and time pickers)
  - Option 3: Request TA to reschedule (no specific time provided)
- [ ] Additional notes textarea (optional)
- [ ] "Submit Request" button creates reschedule request
- [ ] Request sent to TA Team Admin for approval
- [ ] Success message confirms request submission
- [ ] Notification sent to TA Team Admin
- [ ] Request appears in reschedule requests list with "Pending" status

### UI Elements:
- "Request Reschedule" button on interview detail
- Reschedule request form modal
- Current interview details display
- Reason dropdown
- Reason details textarea
- Proposed date/time options (radio buttons with associated inputs)
- Additional notes textarea
- Submit Request button (primary)
- Cancel button (secondary)
- Success notification

### Business Rules:
- Panel members can request reschedule for their assigned interviews
- Request reason is mandatory
- At least one proposed option should be provided (or TA reschedule option)
- System-generated InterviewRescheduleRequestID (GUID)
- Request status defaults to "Pending"
- Original interview remains "Scheduled" until request approved
- TA Team Admin notified for approval
- Request timestamp recorded

### Related FR: FR#Interview Reschedule Requests - Create Request

---

## US-012.3: Create Reschedule Request (Candidate Initiated via TA)
**As a** TA Team Admin  
**I want to** create a reschedule request on behalf of a candidate  
**So that** candidate requests are processed

### Acceptance Criteria:
- [ ] "Reschedule on Candidate's Behalf" action available in interview management
- [ ] Opens reschedule request form
- [ ] Display current interview details (read-only)
- [ ] Reschedule Reason dropdown includes "Candidate Request" option
- [ ] Reason details from candidate required
- [ ] Search for available slots matching:
  - Same or different panel member (if qualified)
  - Designation level compatibility
  - Date range preference
- [ ] Display available slots with panel member details
- [ ] Select new slot or manually specify date/time
- [ ] "Submit Request" button creates request (can auto-approve if TA has authority)
- [ ] Notifications sent to panel members (old and new if different)

### UI Elements:
- Reschedule form for TA-initiated requests
- Reason dropdown with "Candidate Request"
- Available slots search and display
- Slot selection interface
- Submit Request button
- Notifications configuration

### Business Rules:
- TA Team Admin can reschedule directly or create approval request
- If practice policy requires approval, request goes to Practice Admin
- If TA has authority, can approve own request immediately
- Candidate and panel members notified

---

## US-012.4: View Reschedule Request Details
**As a** TA Team Admin, Practice Admin, or Panel Member  
**I want to** view complete reschedule request details  
**So that** I can understand the request context

### Acceptance Criteria:
- [ ] Clicking request row opens detail modal/page
- [ ] Display all request information:
  - Request ID and status
  - Interview details (Candidate, Panel Member, Current Date/Time, Designation, Type)
  - Reschedule reason and details
  - Proposed new date/time options
  - Requestor information (Panel Member or TA)
  - Request timestamp
  - Previous reschedule request ID (if linked)
  - New interview schedule ID (if approved and rescheduled)
- [ ] Show approval/rejection details if resolved
- [ ] "Approve" and "Reject" buttons available for pending requests (if user has permission)
- [ ] "View Interview" button to see current interview details
- [ ] "Close" button returns to request list

### UI Elements:
- Reschedule request detail modal/page
- Information sections: Request Info, Current Interview Details, Proposed Changes, Reason, Resolution (if applicable)
- Action buttons: Approve, Reject, View Interview, Close
- Status indicator

---

## US-012.5: Approve Reschedule Request
**As a** TA Team Admin or Practice Admin  
**I want to** approve a reschedule request  
**So that** interview can be rescheduled

### Acceptance Criteria:
- [ ] "Approve" button available for pending reschedule requests
- [ ] Clicking "Approve" opens confirmation modal
- [ ] If proposed date/time provided, confirm using that
- [ ] If no specific date/time, prompt to select new slot
- [ ] New slot selection interface:
  - Panel member dropdown (same or different, if qualified)
  - Available slots dropdown for selected panel member
  - Date/time display from selected slot
- [ ] Confirmation shows:
  - Old interview details
  - New interview details
  - Impact summary (notifications to be sent)
- [ ] "Confirm Approval" button processes reschedule:
  - Original interview status changed to "Rescheduled"
  - Original slot freed (becomes available)
  - New interview schedule created with "Scheduled" status
  - New slot marked as scheduled
  - Reschedule request status changed to "Approved"
  - RequestStatus updated, approval timestamp recorded
- [ ] Success message confirms approval and rescheduling
- [ ] Notifications sent to candidate and panel members (old and new if different)
- [ ] Calendar invites updated

### UI Elements:
- Approve button
- Approval confirmation modal
- Slot selection interface (if needed)
- Old vs. New interview comparison
- Impact summary
- Confirm Approval button (primary)
- Cancel button (secondary)
- Success notification

### Business Rules:
- Only TA Team Admin and Practice Admin can approve
- Approval requires selecting new valid slot
- Original slot becomes available again
- New slot must be available and not overlapping
- Panel member for new slot must be qualified for designation level
- Both old and new panel members notified
- Candidate notified with new interview details
- Calendar invites cancelled for old time and sent for new time
- Reschedule history maintained

### Related FR: FR#Interview Reschedule Requests - Approve Request

---

## US-012.6: Reject Reschedule Request
**As a** TA Team Admin or Practice Admin  
**I want to** reject a reschedule request  
**So that** inappropriate requests are declined

### Acceptance Criteria:
- [ ] "Reject" button available for pending reschedule requests
- [ ] Clicking "Reject" opens rejection confirmation modal
- [ ] Rejection reason required (dropdown: No Alternate Slot Available, Invalid Reason, Business Priority, Other)
- [ ] If "Other" selected, rejection details textarea required
- [ ] Confirmation dialog warns about rejection impact
- [ ] "Confirm Rejection" button processes rejection:
  - Reschedule request status changed to "Rejected"
  - RequestStatus updated, rejection timestamp and reason recorded
  - Original interview remains "Scheduled" (unchanged)
- [ ] Success message confirms rejection
- [ ] Notification sent to requestor (panel member or TA) with reason
- [ ] Candidate notified that original schedule stands (optional, based on policy)

### UI Elements:
- Reject button
- Rejection confirmation modal
- Rejection reason dropdown
- Rejection details textarea
- Confirm Rejection button
- Cancel button
- Success notification

### Business Rules:
- Only TA Team Admin and Practice Admin can reject
- Rejection reason is mandatory
- Original interview schedule unchanged
- Requestor notified with rejection reason
- Rejection recorded in audit trail

---

## US-012.7: Search and Filter Reschedule Requests
**As a** TA Team Admin or Practice Admin  
**I want to** search and filter reschedule requests  
**So that** I can find specific requests quickly

### Acceptance Criteria:
- [ ] Search box allows searching by request ID, candidate name, panel member name
- [ ] Search results update as user types (debounced)
- [ ] Filter by request status (Pending, Approved, Rejected)
- [ ] Filter by interview (dropdown, searchable by candidate)
- [ ] Filter by panel member (dropdown)
- [ ] Filter by request date range
- [ ] Filter by reschedule reason
- [ ] Multiple filters can be applied simultaneously
- [ ] "Clear Filters" button resets all filters
- [ ] Display count of filtered results

### UI Elements:
- Search input field
- Request status filter dropdown
- Interview/Candidate filter dropdown
- Panel member filter dropdown
- Date range pickers
- Reason filter dropdown
- Clear Filters button
- Results count label

---

## US-012.8: View Reschedule Request History for Interview
**As a** TA Team Admin  
**I want to** see all reschedule requests for a specific interview  
**So that** I can track rescheduling history

### Acceptance Criteria:
- [ ] "Reschedule History" button/tab in interview detail view
- [ ] Display all reschedule requests linked to the interview (original and subsequent)
- [ ] Show request timeline with statuses
- [ ] Display for each request: Request Date, Reason, Status, Resolution
- [ ] Visual timeline showing original schedule and all reschedules
- [ ] Highlight current active schedule

### UI Elements:
- Reschedule History tab/section in interview details
- Timeline visualization
- Request cards with details
- Status indicators

---

## US-012.9: Cancel Reschedule Request
**As a** Panel Member or TA Team Admin  
**I want to** cancel a pending reschedule request  
**So that** requests no longer needed can be withdrawn

### Acceptance Criteria:
- [ ] "Cancel Request" button available for pending requests (requestor only)
- [ ] Confirmation dialog warns about cancellation
- [ ] Upon confirmation, request status changed to "Cancelled"
- [ ] Success message confirms cancellation
- [ ] Original interview remains scheduled
- [ ] Notification sent to TA Team Admin (if panel member cancelled)

### UI Elements:
- Cancel Request button
- Confirmation dialog
- Success notification

### Business Rules:
- Only requestor can cancel pending request
- Cannot cancel approved or rejected requests
- Cancellation recorded in audit trail

---

## US-012.10: Bulk Approve/Reject Reschedule Requests
**As a** TA Team Admin  
**I want to** approve or reject multiple reschedule requests at once  
**So that** I can process requests efficiently

### Acceptance Criteria:
- [ ] Checkbox selection in request table
- [ ] "Bulk Actions" dropdown appears when requests selected
- [ ] Bulk actions: Approve, Reject
- [ ] Bulk approve opens form to assign new slots for each request
- [ ] Bulk reject requires common reason
- [ ] Confirmation dialog shows list of affected requests
- [ ] Success message shows count of processed requests

### UI Elements:
- Selection checkboxes
- Bulk Actions dropdown
- Bulk action form
- Confirmation dialog
- Success notification

---

## US-012.11: View Pending Reschedule Requests Dashboard
**As a** TA Team Admin  
**I want to** see a dashboard of pending reschedule requests  
**So that** I can prioritize processing

### Acceptance Criteria:
- [ ] Dashboard widget shows pending request statistics:
  - Total pending count
  - Requests by reason (breakdown)
  - Oldest pending request age
  - Requests by panel member
- [ ] Click widget to view pending requests list
- [ ] Overdue requests highlighted (based on configured SLA)
- [ ] Quick action buttons for approve/reject

### UI Elements:
- Pending Reschedule Requests Dashboard widget
- Statistics cards
- Overdue indicator
- Reason breakdown chart
- Navigation link to full list

---

## US-012.12: Sort Reschedule Requests List
**As a** system user  
**I want to** sort reschedule requests by different columns  
**So that** I can organize requests meaningfully

### Acceptance Criteria:
- [ ] Sortable columns: Request Date, Candidate, Panel Member, Status, Previous Date, New Date
- [ ] Click column header to sort
- [ ] Sort indicator displayed
- [ ] Default sort: Request Date (newest first)

### UI Elements:
- Sort indicators in column headers

---

## US-012.13: Pagination for Reschedule Requests List
**As a** system user  
**I want to** navigate through pages of reschedule requests  
**So that** I can view large lists efficiently

### Acceptance Criteria:
- [ ] Display 20 requests per page by default
- [ ] Page size selector: 10, 20, 50
- [ ] Page navigation controls

### UI Elements:
- Pagination controls at bottom of table

---

## US-012.14: Export Reschedule Requests
**As a** TA Team Admin  
**I want to** export reschedule request information  
**So that** I can use data for reporting

### Acceptance Criteria:
- [ ] "Export" button available above requests table
- [ ] Export format options: CSV, Excel
- [ ] Exported file includes: Request ID, Request Date, Candidate, Panel Member, Previous Date/Time, New Date/Time, Reason, Status
- [ ] Export respects current filters
- [ ] File name format: RescheduleRequests_YYYYMMDD_HHMMSS

### UI Elements:
- Export button with format dropdown

---

## US-012.15: Reschedule Request Notifications
**As a** Panel Member, TA Team Admin, or Candidate  
**I want to** receive notifications about reschedule requests  
**So that** I'm informed of schedule changes

### Acceptance Criteria:
- [ ] Notification sent when reschedule request created (to TA Team Admin)
- [ ] Notification sent when request approved (to requestor, candidate, panel members)
- [ ] Notification sent when request rejected (to requestor with reason)
- [ ] In-app and email notifications
- [ ] Notification includes request details and action required
- [ ] Notification history viewable

### UI Elements:
- Notification bell icon with badge count
- Notification panel with list
- Email notifications

---

## Technical Notes:
- Implement state machine for request status transitions
- Link reschedule requests to original and new interview schedules
- Maintain reschedule history for audit
- Integrate with notification system for real-time alerts
- Generate calendar invites for rescheduled interviews
- Log all reschedule request actions for audit
- Implement SLA monitoring for pending requests
- Consider approval workflow configuration (single/multi-level approval)

## Related Functional Requirements:
- FR#Interview Reschedule Requests - Create, Approve, Reject Requests
- FR#Interview Schedule Management (linked interviews)
- FR#Availability Management (slot availability)

## Priority: P1 (High)
## Estimated Story Points: 13
