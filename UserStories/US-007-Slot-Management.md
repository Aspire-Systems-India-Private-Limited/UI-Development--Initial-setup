# User Stories: Slot Management Screen

## Module: Slot Management (Availability Management)
**Reference:** Figma_All_Screens.md - Section 7 (Slot Management Screen)  
**Related FR:** FR#Availability Management

---

## US-007.1: View Interview Slots - Calendar View
**As a** panel member, TA Team Admin, or Practice Admin  
**I want to** view interview slots in a calendar format  
**So that** I can see availability at a glance

### Acceptance Criteria:
- [ ] Display interview slots in calendar view by default
- [ ] Calendar shows current month with navigation to previous/next months
- [ ] Each day cell displays slot count and status summary
- [ ] Color coding: Available (green), Blocked (yellow), Unavailable (red), Scheduled (blue)
- [ ] Click on date cell to view detailed slots for that day
- [ ] "Today" button navigates to current date
- [ ] View toggle to switch between Calendar and Table views
- [ ] Panel members see only their own slots
- [ ] Admins/TA see slots for all panel members (filterable)

### UI Elements:
- Month calendar grid
- Date cells with slot indicators
- Color-coded slot status badges
- Previous/Next month navigation arrows
- Today button
- View toggle (Calendar/Table)
- Filter panel (for admins)

### Business Rules:
- Panel Member: View and manage own slots only
- TA Team Admin: View all panel member slots for scheduling
- Practice Admin: View all panel member slots in their practice
- Master Admin: View all panel member slots across practices

---

## US-007.2: View Interview Slots - Table View
**As a** panel member, TA Team Admin, or Practice Admin  
**I want to** view interview slots in a table format  
**So that** I can see detailed slot information in a list

### Acceptance Criteria:
- [ ] Display slots in a table with columns: Date, Start Time, End Time, Panel Member, Status, Reason, Actions
- [ ] Panel members see only their own slots
- [ ] Admins see slots for all panel members with filters
- [ ] Default sorting by date and start time (ascending)
- [ ] Status badges with color coding
- [ ] Pagination: 20 slots per page
- [ ] Empty state message when no slots exist

### UI Elements:
- Slots table with sortable columns
- Status indicator badges
- Action menu for each row
- Pagination controls
- View toggle (Calendar/Table)

---

## US-007.3: Add New Availability Slot
**As a** panel member  
**I want to** add my available time slots  
**So that** I can be scheduled for interviews

### Acceptance Criteria:
- [ ] "Add Slot" button opens add slot form
- [ ] Date picker for slot date (cannot select past dates)
- [ ] Start Time picker (15-minute intervals)
- [ ] End Time picker (15-minute intervals, must be after start time)
- [ ] Duration auto-calculated and displayed
- [ ] Status dropdown: Available, Blocked, Unavailable
- [ ] Reason field (optional for Available, required for Blocked/Unavailable)
- [ ] Panel Member field auto-filled (for panel members) or dropdown (for admins)
- [ ] Source dropdown (Web, Mobile, API)
- [ ] "Save" button creates slot
- [ ] "Cancel" button closes form
- [ ] Validation: No overlapping slots for same panel member
- [ ] Success message confirms slot creation

### UI Elements:
- "Add Slot" button (primary action)
- Modal form with fields:
  - Date (date picker, required)
  - Start Time (time picker, required)
  - End Time (time picker, required)
  - Duration (auto-calculated display)
  - Status (dropdown, required)
  - Reason (textarea, conditionally required)
  - Panel Member (dropdown, conditionally enabled)
  - Source (dropdown, required)
- Save button (primary)
- Cancel button (secondary)
- Inline validation messages
- Success notification

### Business Rules:
- Panel members can only add slots for themselves
- Admins can add slots for any panel member
- Cannot create slots in the past
- Slot duration must be at least 30 minutes
- No overlapping slots for same panel member
- Available slots can be used for scheduling interviews
- Blocked/Unavailable slots cannot be scheduled
- System-generated AvailabilityID (GUID)

### Related FR: FR#Availability Management - Create Availability

---

## US-007.4: Edit Availability Slot
**As a** panel member or admin  
**I want to** edit existing availability slots  
**So that** I can update my availability

### Acceptance Criteria:
- [ ] "Edit" action opens edit form with pre-filled data
- [ ] Allow editing: Date, Start Time, End Time, Status, Reason
- [ ] Panel Member field read-only
- [ ] Validation: No overlapping slots
- [ ] Cannot edit date/time if slot has scheduled interview
- [ ] Can change status (e.g., Available to Blocked) if no scheduled interview
- [ ] "Save" button updates slot
- [ ] "Cancel" button discards changes
- [ ] Success message confirms update
- [ ] Audit fields updated automatically

### UI Elements:
- Edit form modal with pre-filled fields
- Read-only panel member field
- Save and Cancel buttons
- Validation messages
- Warning for scheduled interviews
- Success notification

### Business Rules:
- Cannot edit slots with scheduled interviews (date/time locked)
- Can change status if interview not yet scheduled
- Panel members can only edit their own slots
- Admins can edit any panel member's slots
- Changing Available to Unavailable requires reason

---

## US-007.5: Delete Availability Slot
**As a** panel member or admin  
**I want to** delete availability slots  
**So that** I can remove incorrect or outdated availability

### Acceptance Criteria:
- [ ] "Delete" action available in slot row or detail view
- [ ] Confirmation dialog warns about deletion
- [ ] Cannot delete slot with scheduled interview
- [ ] If interview scheduled, show error message and interview details
- [ ] Upon confirmation, slot is deleted (soft delete: IsActive = false)
- [ ] Success message confirms deletion
- [ ] Deleted slot removed from calendar and table views

### UI Elements:
- Delete button
- Confirmation dialog
- Error message for scheduled interviews
- Success notification

### Business Rules:
- Cannot delete slots with scheduled interviews (must cancel interview first)
- Panel members can only delete their own slots
- Admins can delete any slot (with appropriate permissions)
- Deletion is soft delete (IsActive = false)
- Deleted slots retained for audit purposes

---

## US-007.6: Bulk Add Availability Slots
**As a** panel member  
**I want to** add multiple availability slots at once  
**So that** I can efficiently set my availability for a week or month

### Acceptance Criteria:
- [ ] "Bulk Add Slots" button opens bulk add modal
- [ ] Select date range (start date, end date)
- [ ] Select days of week (checkboxes: Mon, Tue, Wed, Thu, Fri, Sat, Sun)
- [ ] Define time ranges (multiple time ranges per day)
- [ ] Add Time Range button to add additional time ranges
- [ ] Each time range: Start Time, End Time
- [ ] Status selection (Available, Blocked, Unavailable)
- [ ] Reason field (if Blocked/Unavailable)
- [ ] Preview shows all slots to be created
- [ ] "Create Slots" button generates all slots
- [ ] Validation: Skip overlapping slots or show warning
- [ ] Success message shows count of created slots

### UI Elements:
- "Bulk Add Slots" button
- Bulk add modal with:
  - Date range picker (start, end)
  - Days of week checkboxes
  - Time ranges section (dynamic)
  - Add Time Range button
  - Status dropdown
  - Reason textarea
  - Preview section
- Create Slots button (primary)
- Cancel button (secondary)
- Success notification with count

### Business Rules:
- Only create slots for future dates
- Skip dates that already have overlapping slots
- Maximum date range: 90 days
- Maximum time ranges per day: 5
- All generated slots belong to logged-in panel member (or selected member for admins)

---

## US-007.7: Filter Slots
**As a** TA Team Admin or Practice Admin  
**I want to** filter slots by various criteria  
**So that** I can find available slots for scheduling

### Acceptance Criteria:
- [ ] Filter panel available on calendar and table views
- [ ] Filter by panel member (multi-select dropdown)
- [ ] Filter by practice (dropdown, for Master Admin)
- [ ] Filter by date range (start date, end date)
- [ ] Filter by status (Available, Blocked, Unavailable, Scheduled)
- [ ] Filter by qualification level (to match candidate requirements)
- [ ] "Apply Filters" button executes filter
- [ ] "Clear Filters" button resets all filters
- [ ] Filtered results count displayed
- [ ] Filters persist during session

### UI Elements:
- Filter panel (collapsible)
- Panel member multi-select
- Practice dropdown (Master Admin)
- Date range pickers
- Status multi-select
- Qualification level multi-select
- Apply Filters button
- Clear Filters button
- Results count label

---

## US-007.8: Search Available Slots for Interview Scheduling
**As a** TA Team Admin  
**I want to** search for available slots matching specific criteria  
**So that** I can efficiently schedule interviews

### Acceptance Criteria:
- [ ] "Find Available Slots" feature accessible from slot management and interview scheduling
- [ ] Input criteria:
  - Designation level (dropdown)
  - Date range (start date, end date)
  - Time preference (Morning, Afternoon, Evening, Any)
  - Duration required (e.g., 60 minutes)
  - Practice (dropdown, optional)
- [ ] Search results show matching available slots with panel member details
- [ ] Sort results by date, then time
- [ ] Display panel member name, qualification levels, slot time
- [ ] "Schedule Interview" button on each result (quick schedule)
- [ ] Pagination for large result sets

### UI Elements:
- "Find Available Slots" button/feature
- Search criteria form
- Results table with panel member info and slot details
- Schedule Interview button on each row
- Pagination controls

### Business Rules:
- Only show slots with status "Available"
- Match panel member qualifications with requested designation level
- Exclude past slots
- Consider slot duration matches interview duration
- Results limited to selected practice scope (for Practice Admin)

---

## US-007.9: View Slot Details
**As a** panel member or admin  
**I want to** view detailed information about a slot  
**So that** I can see complete slot information

### Acceptance Criteria:
- [ ] Clicking slot in calendar or table opens detail modal
- [ ] Display all slot information: Date, Start Time, End Time, Duration, Panel Member, Status, Reason
- [ ] Show associated interview details (if scheduled)
- [ ] Display audit information: Created Date, Modified Date
- [ ] "Edit" and "Delete" buttons available (if permissions allow)
- [ ] "Schedule Interview" button (if slot is available)
- [ ] "Close" button returns to previous view

### UI Elements:
- Slot detail modal
- Information sections: Time Details, Panel Member Info, Status & Reason, Interview Info (if applicable), Audit Info
- Action buttons: Edit, Delete, Schedule Interview, Close

---

## US-007.10: Block/Unblock Time Slots
**As a** panel member  
**I want to** block time slots for personal reasons  
**So that** I'm not scheduled during those times

### Acceptance Criteria:
- [ ] "Block Time" action available for Available slots
- [ ] Opens block time form with pre-filled date/time
- [ ] Reason field required (e.g., "Personal appointment", "On leave")
- [ ] "Block" button changes status to Blocked
- [ ] Blocked slots shown with yellow indicator
- [ ] "Unblock" action available to revert to Available
- [ ] Unblock requires confirmation
- [ ] Success messages for block/unblock actions

### UI Elements:
- Block Time button/action
- Block time form with reason field
- Unblock button
- Confirmation dialog
- Success notifications

### Business Rules:
- Can only block slots without scheduled interviews
- Cannot block slots in the past
- Blocked slots not available for interview scheduling
- Panel members can only block their own slots
- Admins can block any panel member's slots

---

## US-007.11: Mark Slots as Unavailable
**As a** panel member or admin  
**I want to** mark slots as unavailable  
**So that** extended unavailability periods are recorded

### Acceptance Criteria:
- [ ] "Mark Unavailable" action available
- [ ] Opens unavailability form
- [ ] Date range selection (for extended periods)
- [ ] Time range selection (or all-day option)
- [ ] Reason field required (e.g., "Vacation", "Training", "Project deadline")
- [ ] "Mark Unavailable" button creates unavailable slots for entire period
- [ ] Unavailable slots shown with red indicator
- [ ] Cannot mark slots with scheduled interviews as unavailable
- [ ] Success message confirms unavailability

### UI Elements:
- Mark Unavailable button/action
- Unavailability form with date/time ranges
- Reason textarea
- Mark Unavailable button (primary)
- Success notification

### Business Rules:
- Unavailable slots cannot be scheduled for interviews
- Reason is mandatory
- Cannot mark past slots
- Existing scheduled interviews prevent marking as unavailable

---

## US-007.12: View Panel Member Availability Summary
**As a** TA Team Admin or Practice Admin  
**I want to** see availability summary for panel members  
**So that** I can plan interview scheduling

### Acceptance Criteria:
- [ ] "Availability Summary" view shows panel members with availability stats
- [ ] Display for each panel member:
  - Name and qualification levels
  - Available slots this week
  - Available slots next week
  - Blocked/Unavailable periods
  - Upcoming scheduled interviews
- [ ] Filter by practice
- [ ] Sort by availability count
- [ ] Click member to view detailed calendar

### UI Elements:
- Availability Summary view/tab
- Panel member cards with stats
- Filter and sort controls
- Drill-down links to detailed calendar

---

## US-007.13: Sort and Pagination for Table View
**As a** user viewing slots in table view  
**I want to** sort and paginate the slot list  
**So that** I can navigate large lists efficiently

### Acceptance Criteria:
- [ ] Sortable columns: Date, Start Time, End Time, Panel Member, Status
- [ ] Click column header to sort
- [ ] Sort indicator displayed
- [ ] Pagination controls at bottom
- [ ] Page size options: 20, 50, 100
- [ ] Default: 20 slots per page
- [ ] Total count display

### UI Elements:
- Sort indicators in column headers
- Pagination controls
- Page size dropdown

---

## US-007.15: Receive Slot Reminders (Future Enhancement)
**As a** panel member  
**I want to** receive reminders about my upcoming availability  
**So that** I can prepare for potential interview scheduling

### Acceptance Criteria:
- [ ] Reminder notification 1 day before available slot
- [ ] Reminder shows slot details
- [ ] Option to confirm or update availability
- [ ] Email and in-app notifications

### UI Elements:
- Notification badge
- Reminder message
- Confirm/Update buttons

---

## Technical Notes:
- Use full-featured calendar component (e.g., FullCalendar, React Big Calendar)
- Implement real-time updates for slot changes (WebSocket or polling)
- Optimize calendar rendering for large datasets
- Cache panel member and practice lookups
- Validate no overlapping slots on server-side
- Log all slot management actions for audit
- Consider time zone handling for distributed teams
- Implement drag-and-drop for slot editing in calendar view (future enhancement)

## Related Functional Requirements:
- FR#Availability Management - Create, Update, Retrieve, Delete Availability
- FR#Interview Scheduling (depends on slot availability)

## Priority: P1 (High)
## Estimated Story Points: 13
