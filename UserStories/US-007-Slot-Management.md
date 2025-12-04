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
- [ ] Color coding: Available (green), Blocked (blue), Booked (orange), Cancelled (gray)
- [ ] Click on date cell to view detailed slots for that day
- [ ] "Today" button navigates to current date
- [ ] View toggle to switch between Calendar and Table views
- [ ] Panel members see only their own slots
- [ ] Admins see slots for all panel members (filterable)
- [ ] TA Team Admin sees all slots to identify available slots for scheduling

### UI Elements:
- Month calendar grid
- Date cells with slot indicators
- Color-coded slot status badges (Available: green, Blocked: blue, Booked: orange, Cancelled: gray)
- Previous/Next month navigation arrows
- Today button
- View toggle (Calendar/Table)
- Filter panel (for admins and TA Team Admin)

### Business Rules:
- Panel Member: View and manage own slots only (create, edit, cancel)
- TA Team Admin: View all panel member slots, can block and book slots for scheduling
- Practice Admin: View all panel member slots in their practice, can manage slots
- Master Admin: View all panel member slots across practices, full management access
- Status Flow: Available (created) → Blocked (by TA Team Admin) → Booked (by same TA Team Admin)
- Slots can be Cancelled at any point if not Blocked or Booked

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
- [ ] Start Time picker (60-minute intervals, 9:00 AM - 6:00 PM)
- [ ] End Time picker (60-minute intervals, must be after start time)
- [ ] Duration auto-calculated and displayed
- [ ] Status is automatically set to "Available" (not user-selectable)
- [ ] Panel Member field auto-filled (for panel members) or dropdown (for admins)
- [ ] Source dropdown (Web, Mobile, API)
- [ ] "Save" button creates slot
- [ ] "Cancel" button closes form
- [ ] Validation: No overlapping slots for same panel member
- [ ] Validation: Maximum 8 hours per day per panel member
- [ ] Validation: Time must be within business hours (9 AM - 6 PM)
- [ ] Success message confirms slot creation

### UI Elements:
- "Add Slot" button (primary action)
- Modal form with fields:
  - Date (date picker, required)
  - Start Time (time picker with 60-min intervals, required)
  - End Time (time picker with 60-min intervals, required)
  - Duration (auto-calculated display)
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
- Slot duration must be in 60-minute increments
- Time slots must be within business hours (9 AM - 6 PM)
- No overlapping slots for same panel member
- Maximum 8 hours availability per day per panel member
- All new slots default to "Available" status
- System-generated AvailabilityID (GUID)

### Related FR: FR#MAM-1 - Availability Planning

---

## US-007.4: Edit Availability Slot
**As a** panel member or admin  
**I want to** edit existing availability slots  
**So that** I can update my availability

### Acceptance Criteria:
- [ ] "Edit" action opens edit form with pre-filled data
- [ ] Allow editing: Date, Start Time, End Time
- [ ] Panel Member field read-only
- [ ] Status field read-only (status changes handled by Block/Book actions)
- [ ] Time must be in 60-minute increments within business hours (9 AM - 6 PM)
- [ ] Validation: No overlapping slots
- [ ] Validation: Maximum 8 hours per day per panel member
- [ ] Cannot edit slots with status "Blocked" or "Booked"
- [ ] Cannot edit slots in the past
- [ ] "Save" button updates slot
- [ ] "Cancel" button discards changes
- [ ] Success message confirms update
- [ ] Audit fields updated automatically

### UI Elements:
- Edit form modal with pre-filled fields
- Read-only panel member and status fields
- Save and Cancel buttons
- Validation messages
- Warning for non-editable slots
- Success notification

### Business Rules:
- Can only edit slots with "Available" status
- Cannot edit slots with scheduled interviews (status "Blocked" or "Booked")
- Panel members can only edit their own slots
- Admins can edit any panel member's slots
- Time constraints: 60-minute increments, 9 AM - 6 PM, max 8 hours/day
- Cannot edit past slots

### Related FR: FR#MAM-6 - Availability Update

---

## US-007.5: Cancel Availability Slot
**As a** panel member or admin  
**I want to** cancel availability slots  
**So that** I can remove slots I can no longer honor

### Acceptance Criteria:
- [ ] "Cancel" action available in slot row or detail view
- [ ] Opens cancellation form with slot details
- [ ] Cancellation reason field required (min 5 chars, max 500 chars)
- [ ] Cannot cancel slot with status "Blocked" or "Booked" (active bookings)
- [ ] If interview scheduled, show error message and interview details
- [ ] Confirmation dialog warns about cancellation with reason display
- [ ] Upon confirmation, slot status changed to "Cancelled" (soft delete)
- [ ] Success message confirms cancellation
- [ ] Cancelled slot shown with "Cancelled" badge in list
- [ ] Cancelled slots retained for audit purposes

### UI Elements:
- Cancel button
- Cancellation form with reason field
- Confirmation dialog with reason display
- Error message for scheduled interviews
- Success notification
- Cancelled badge in slot list

### Business Rules:
- Cannot cancel slots with scheduled interviews (status "Blocked" or "Booked")
- Panel members can only cancel their own slots
- Admins can cancel any slot (with appropriate permissions)
- Cancellation reason is mandatory (min 5 chars)
- Cancellation is soft delete (status = "Cancelled", not physically deleted)
- Cancelled slots retained for audit trail
- Cannot cancel past slots
- Cannot cancel already cancelled slots

### Related FR: FR#MAM-3 - Availability Cancellation

---

## US-007.6: Bulk Add Availability Slots
**As a** panel member  
**I want to** add multiple availability slots at once  
**So that** I can efficiently set my availability for a week or month

### Acceptance Criteria:
- [ ] "Bulk Add Slots" button opens bulk add modal
- [ ] Select date range (start date, end date, max 90 days)
- [ ] Select days of week (checkboxes: Mon, Tue, Wed, Thu, Fri, Sat, Sun)
- [ ] Define time ranges in 60-minute increments within business hours (9 AM - 6 PM)
- [ ] Add Time Range button to add additional time ranges
- [ ] Each time range: Start Time, End Time (60-minute increments)
- [ ] All slots created with status "Available"
- [ ] Preview shows all slots to be created with validation warnings
- [ ] "Create Slots" button generates all slots
- [ ] Validation: Skip overlapping slots or show warning
- [ ] Validation: Maximum 8 hours per day per panel member
- [ ] Success message shows count of created slots and any skipped slots

### UI Elements:
- "Bulk Add Slots" button
- Bulk add modal with:
  - Date range picker (start, end, max 90 days)
  - Days of week checkboxes
  - Time ranges section (dynamic, 60-min increments)
  - Add Time Range button
  - Preview section with warnings
- Create Slots button (primary)
- Cancel button (secondary)
- Success notification with count and warnings

### Business Rules:
- Only create slots for future dates
- Skip dates that already have overlapping slots
- Maximum date range: 90 days
- Maximum time ranges per day: 5
- Each time slot must be 60-minute increment
- Time must be within business hours (9 AM - 6 PM)
- Maximum 8 hours per day per panel member across all slots
- All generated slots belong to logged-in panel member (or selected member for admins)
- All bulk-created slots have status "Available"

---

## US-007.7: Filter Slots
**As a** TA Team Admin or Practice Admin  
**I want to** filter slots by various criteria  
**So that** I can find available slots for scheduling

### Acceptance Criteria:
- [ ] Filter panel available on calendar and table views
- [ ] Filter by panel member (multi-select dropdown)
- [ ] Filter by practice (dropdown, for Master Admin)
- [ ] Filter by date range (start date, end date, max 90 days span)
- [ ] Filter by status (Available, Blocked, Booked, Cancelled)
- [ ] Filter by qualification level (to match candidate requirements)
- [ ] "Apply Filters" button executes filter
- [ ] "Clear Filters" button resets all filters
- [ ] Filtered results count displayed
- [ ] Filters persist during session
- [ ] Default date range: Today + 30 days if not specified

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
- Consider slot duration matches interview duration (60-minute increments)
- Results limited to selected practice scope (for Practice Admin)
- Maximum date range for search: 90 days
- Results sorted by date, then time

### Related FR: FR#MAM-2 - Availability Retrieval

---

## US-007.9: View Slot Details
**As a** panel member or admin  
**I want to** view detailed information about a slot  
**So that** I can see complete slot information

### Acceptance Criteria:
- [ ] Clicking slot in calendar or table opens detail modal
- [ ] Display all slot information: Date, Start Time, End Time, Duration, Panel Member, Status
- [ ] If status is "Blocked": Show who blocked it and when
- [ ] If status is "Booked": Show who booked it, when, and associated interview details
- [ ] If status is "Cancelled": Show cancellation reason, who cancelled, and when
- [ ] Display audit information: Created Date, Modified Date, Created By, Modified By
- [ ] "Edit" button available for "Available" status slots (if permissions allow)
- [ ] "Cancel" button available for "Available" status slots (if permissions allow)
- [ ] "Block" button available for "Available" status slots (TA Team Admin only)
- [ ] "Unblock" button available for "Blocked" status slots (only for blocking TA Team Admin)
- [ ] "Book" button available for "Blocked" status slots (only for blocking TA Team Admin)
- [ ] "Close" button returns to previous view

### UI Elements:
- Slot detail modal
- Information sections: Time Details, Panel Member Info, Status & History, Interview Info (if booked), Audit Info
- Action buttons: Edit, Cancel, Block, Unblock, Book, Close (contextual based on status and role)

---

## US-007.10: Block/Unblock Availability Slots (TA Team Admin)
**As a** TA Team Admin  
**I want to** block available slots temporarily during interview scheduling  
**So that** I can reserve slots while confirming interview details

### Acceptance Criteria:
- [ ] "Block Slot" action available for slots with "Available" status
- [ ] Only TA Team Admin can block slots
- [ ] Clicking block changes status from "Available" to "Blocked"
- [ ] Blocked slots shown with blue indicator and lock icon
- [ ] Blocked slot is reserved for the TA Team Admin who blocked it
- [ ] Other TA Team Admins cannot modify or book the blocked slot
- [ ] "Unblock" action available only to the TA Team Admin who blocked the slot
- [ ] Unblock changes status back to "Available"
- [ ] Success messages for block/unblock actions
- [ ] Slot details show who blocked the slot and when

### UI Elements:
- Block Slot button/action (for Available slots)
- Unblock button (for Blocked slots, only for blocker)
- Locked indicator icon for blocked slots
- Blocker info display (name and date)
- Success notifications

### Business Rules:
- Only TA Team Admin role can block slots
- Can only block slots with "Available" status
- Cannot block slots that are "Cancelled", already "Blocked", or "Booked"
- Once blocked, only the blocking TA Team Admin can unblock or book the slot
- Other TA Team Admins see the slot as blocked but cannot modify it
- Blocked slots not available for scheduling by other users
- Panel members and other admins cannot block slots
- Blocking is temporary - intended for short-term reservation during scheduling process
- Audit trail records who blocked and when

### Related FR: FR#MAM-4 - Block Availability Slot

---

## US-007.11: Book Availability Slot (TA Team Admin)
**As a** TA Team Admin  
**I want to** book a blocked slot when interview is confirmed  
**So that** the slot is finalized and protected from changes

### Acceptance Criteria:
- [ ] "Book Slot" action available for slots with "Blocked" status
- [ ] Only the TA Team Admin who blocked the slot can book it
- [ ] Clicking book changes status from "Blocked" to "Booked"
- [ ] Booked slots shown with green indicator and confirmed icon
- [ ] Booked slot is locked and cannot be modified by anyone except the booking TA Team Admin
- [ ] Only the booking TA Team Admin can cancel or revert the booked slot
- [ ] Success message confirms booking
- [ ] Slot details show who booked the slot and when
- [ ] Panel member receives notification about the booked interview slot

### UI Elements:
- Book Slot button/action (for Blocked slots, only for blocker)
- Booked indicator icon
- Booking info display (name and date)
- Success notification
- Confirmation icon for booked status

### Business Rules:
- Only TA Team Admin who blocked the slot can book it
- Can only book slots with "Blocked" status
- Cannot book slots that are "Available", "Cancelled", or already "Booked"
- Once booked, slot is finalized for interview and protected from changes
- Only the booking TA Team Admin can cancel the booked slot if needed
- Booked status indicates interview is confirmed and scheduled
- Panel member cannot modify their own booked slots
- Booking triggers notifications to panel member and candidate

### Related FR: FR#MAM-5 - Book Availability Slot

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
  - Blocked slots count
  - Booked slots count (upcoming interviews)
  - Cancelled slots this period
- [ ] Filter by practice
- [ ] Sort by availability count
- [ ] Click member to view detailed calendar

### UI Elements:
- Availability Summary view/tab
- Panel member cards with stats
- Status breakdown (Available, Blocked, Booked, Cancelled)
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
- Enforce business rules: 60-minute increments, 9 AM - 6 PM, max 8 hours/day
- Log all slot management actions for audit trail
- Implement role-based access control for Block/Book operations (TA Team Admin only)
- Track who blocked/booked slots for accountability
- Consider time zone handling for distributed teams
- Soft delete for cancelled slots (maintain audit history)

## Related Functional Requirements:
- FR#MAM-1 - Availability Planning
- FR#MAM-2 - Availability Retrieval
- FR#MAM-3 - Availability Cancellation
- FR#MAM-4 - Block Availability Slot
- FR#MAM-5 - Book Availability Slot
- FR#MAM-6 - Availability Update
- FR#Interview Scheduling (depends on slot availability)

## Priority: P1 (High)
## Estimated Story Points: 13
