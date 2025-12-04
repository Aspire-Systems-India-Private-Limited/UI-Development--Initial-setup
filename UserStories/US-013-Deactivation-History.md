# User Stories: Hiring Opportunity Deactivation History Screen

## Module: Hiring Opportunity Deactivation History
**Reference:** Figma_All_Screens.md - Section 13 (Hiring Opportunity Deactivation History Screen)  
**Related FR:** FR#HOP-4 Deactivation, Deactivation History

---

## US-013.1: View Deactivation History List
**As a** Master Admin or TA Team Admin  
**I want to** view deactivation history for all hiring opportunities  
**So that** I can track when and why opportunities were deactivated

### Acceptance Criteria:
- [ ] Display deactivation history in a table with columns: Deactivation ID, Opportunity, Reason, Deactivated By, Deactivated Date, Previous Status, New Status, Actions
- [ ] Master Admin sees deactivation history for all opportunities
- [ ] TA Team Admin sees history for practice-scoped opportunities
- [ ] Practice Admin sees history for practice opportunities
- [ ] Display history entry count at the top
- [ ] Default sorting by deactivation date (newest first)
- [ ] Empty state message when no history exists

### UI Elements:
- Deactivation history table with sortable columns
- History entry count badge
- Status indicators for Previous/New status
- Action menu for each row
- Filter controls
- Empty state illustration

### Business Rules:
- Master Admin: View all deactivation history
- TA Team Admin: View history for practice opportunities
- Practice Admin: View history for practice opportunities
- Each deactivation creates a history entry
- History is read-only (cannot be edited or deleted)

---

## US-013.2: View Deactivation History for Specific Opportunity
**As a** Master Admin, TA Team Admin, or Practice Admin  
**I want to** view deactivation history for a specific hiring opportunity  
**So that** I can understand the opportunity's lifecycle

### Acceptance Criteria:
- [ ] "View History" button/link in opportunity detail view
- [ ] Opens deactivation history modal/page filtered for that opportunity
- [ ] Display all deactivation entries for the opportunity (if multiple deactivation/reactivation cycles)
- [ ] Show timeline view of deactivations
- [ ] Display for each entry: Deactivation Date, Deactivated By, Reason, Previous Status, New Status
- [ ] Chronological order (newest first or oldest first, user selectable)
- [ ] "Close" button returns to opportunity details

### UI Elements:
- "View History" button in opportunity detail
- Deactivation history modal/page
- Timeline visualization
- History entry cards with details
- Chronological sorting toggle
- Close button

---

## US-013.3: View Deactivation History Entry Details
**As a** Master Admin or TA Team Admin  
**I want to** view complete details of a deactivation history entry  
**So that** I can see full context of deactivation

### Acceptance Criteria:
- [ ] Clicking history entry row opens detail modal
- [ ] Display all deactivation information:
  - DeactivationHistoryID
  - Hiring Opportunity (title, ID)
  - Deactivation Reason (full text)
  - Deactivated By (user name and ID)
  - Deactivated Date and time
  - Previous StatusID and status name
  - New StatusID and status name (should be "Inactive" or "Deactivated")
  - Created Date (timestamp of history entry creation)
  - Source (application source)
- [ ] Show related opportunity details: Practice, Designation, Current Status
- [ ] "View Opportunity" button to navigate to opportunity details
- [ ] "Close" button returns to history list

### UI Elements:
- Deactivation history detail modal
- Information sections: Deactivation Details, Opportunity Info, Deactivated By Info
- View Opportunity button
- Close button

---

## US-013.4: Search and Filter Deactivation History
**As a** Master Admin or TA Team Admin  
**I want to** search and filter deactivation history  
**So that** I can find specific history entries quickly

### Acceptance Criteria:
- [ ] Search box allows searching by opportunity title, deactivation reason
- [ ] Search results update as user types (debounced)
- [ ] Filter by opportunity (dropdown, searchable)
- [ ] Filter by practice (dropdown) - for Master Admin
- [ ] Filter by deactivated by user (dropdown)
- [ ] Filter by date range (deactivation date)
- [ ] Filter by previous status
- [ ] Filter by source (Web, Mobile, API, Admin)
- [ ] Multiple filters can be applied simultaneously
- [ ] "Clear Filters" button resets all filters
- [ ] Display count of filtered results

### UI Elements:
- Search input field
- Opportunity filter dropdown
- Practice filter dropdown (Master Admin only)
- Deactivated By user filter dropdown
- Date range pickers (start date, end date)
- Previous Status filter dropdown
- Source filter dropdown
- Clear Filters button
- Results count label

---

## US-013.5: Sort Deactivation History List
**As a** system user  
**I want to** sort deactivation history by different columns  
**So that** I can organize history meaningfully

### Acceptance Criteria:
- [ ] Sortable columns: Deactivation Date, Opportunity, Deactivated By, Previous Status
- [ ] Click column header to sort ascending, click again for descending
- [ ] Sort indicator displayed in active column
- [ ] Default sort: Deactivation Date (newest first)
- [ ] Sort persists during pagination

### UI Elements:
- Sort indicators in column headers
- Sort direction arrows

---

## US-013.6: Pagination for Deactivation History List
**As a** system user  
**I want to** navigate through pages of deactivation history  
**So that** I can view large lists efficiently

### Acceptance Criteria:
- [ ] Display 20 history entries per page by default
- [ ] Page size selector: 10, 20, 50
- [ ] Page navigation: First, Previous, Next, Last
- [ ] Display current page and total pages
- [ ] Display total history entry count
- [ ] Pagination controls disabled appropriately

### UI Elements:
- Pagination controls at bottom of table
- Page size dropdown
- Page navigation buttons
- Page and count display

---

## US-013.8: View Deactivation Statistics
**As a** Master Admin  
**I want to** see statistics about opportunity deactivations  
**So that** I can understand deactivation patterns

### Acceptance Criteria:
- [ ] Deactivation Statistics dashboard shows:
  - Total deactivations count
  - Deactivations by reason (breakdown)
  - Deactivations by practice (breakdown)
  - Deactivations by time period (monthly/quarterly chart)
  - Top deactivated opportunities
  - Average opportunity lifetime before deactivation
- [ ] Visual charts and graphs
- [ ] Date range filter for statistics
- [ ] Drill-down capability to underlying data

### UI Elements:
- Deactivation Statistics Dashboard
- Charts: Bar, Pie, Line
- Date range filter
- Drill-down links

---

## US-013.9: Compare Deactivation Reasons
**As a** Master Admin or Practice Admin  
**I want to** analyze deactivation reasons  
**So that** I can identify common reasons and take corrective action

### Acceptance Criteria:
- [ ] "Deactivation Reasons Analysis" view shows:
  - Reason frequency distribution (chart)
  - Most common reasons (list with counts)
  - Reasons by practice (if applicable)
  - Reason trends over time
- [ ] Filter by date range, practice

### UI Elements:
- Deactivation Reasons Analysis view
- Frequency distribution chart
- Top reasons list
- Trend chart
- Filter controls

---

## US-013.10: View Deactivation Audit Trail
**As a** Master Admin  
**I want to** see complete audit trail for deactivations  
**So that** I can ensure compliance and accountability

### Acceptance Criteria:
- [ ] Audit trail view shows all deactivation actions with:
  - Timestamp
  - User who performed action
  - Action type (Deactivate, Reactivate)
  - Opportunity affected
  - Reason provided
  - Source application
- [ ] Filter by user, date range, opportunity

### UI Elements:
- Audit Trail view
- Detailed action log table
- Filter controls

---

## US-013.11: Link Deactivation History to Opportunity Lifecycle
**As a** TA Team Admin  
**I want to** see deactivation events in opportunity lifecycle timeline  
**So that** I understand opportunity evolution

### Acceptance Criteria:
- [ ] Opportunity detail view includes lifecycle timeline
- [ ] Timeline shows: Created, Opened, Deactivated, Reactivated, Closed events
- [ ] Deactivation events highlighted with reason
- [ ] Click deactivation event to view history details
- [ ] Visual timeline with milestones

### UI Elements:
- Lifecycle timeline in opportunity detail
- Event milestones with icons
- Deactivation event indicator
- Details on click

---

## US-013.13: Set Up Deactivation Alerts
**As a** Master Admin or Practice Admin  
**I want to** receive alerts when opportunities are deactivated  
**So that** I'm informed of important changes

### Acceptance Criteria:
- [ ] Alert configuration in settings
- [ ] Configure alert recipients (users/roles)
- [ ] Configure alert triggers (all deactivations, specific practices, specific reasons)
- [ ] Alert delivery methods (email, in-app notification)
- [ ] Alert includes deactivation details and reason
- [ ] Alert history viewable

### UI Elements:
- Alert configuration page
- Recipient selector
- Trigger configuration
- Delivery method checkboxes
- Save configuration button

---

## US-013.14: View Reactivation Events in History
**As a** Master Admin or TA Team Admin  
**I want to** see reactivation events alongside deactivation history  
**So that** I understand complete activation/deactivation cycles

### Acceptance Criteria:
- [ ] History includes both deactivation and reactivation events
- [ ] Reactivation entries show: Reactivated Date, Reactivated By, Previous Status (Inactive), New Status (Active/Open)
- [ ] Visual indicator differentiates deactivation vs. reactivation
- [ ] Paired deactivation/reactivation highlighted as cycles
- [ ] Filter to show only deactivations, only reactivations, or both

### UI Elements:
- Combined history view with event type indicator
- Color coding (red for deactivation, green for reactivation)
- Cycle grouping (optional)
- Event type filter

---

## Technical Notes:
- Store deactivation history in separate table for audit compliance
- Ensure history entries are immutable (insert-only, no updates/deletes)
- Index history table on OpportunityID, DeactivatedDate for performance
- Implement soft delete for opportunities (IsActive flag)
- Log all deactivation actions in application logs
- Generate timestamps in UTC for consistency
- Implement data retention policy for history (e.g., retain for 7 years)
- Consider archival strategy for old history entries

## Related Functional Requirements:
- FR#HOP-4 – Deactivate Hiring Opportunity
- FR#Hiring Opportunity Deactivation History

## Priority: P2 (Medium)
## Estimated Story Points: 8
