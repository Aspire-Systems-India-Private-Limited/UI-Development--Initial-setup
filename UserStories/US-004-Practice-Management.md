# User Stories: Practice Management Screen

## Module: Practice Management
**Reference:** Figma_All_Screens.md - Section 4 (Practice Management Screen)  
**Related FR:** FR#PMP-1 to FR#PMP-5

---

## US-004.1: View Practice List
**As a** Master Admin  
**I want to** view all practices in the system  
**So that** I can see available practices and their status

### Acceptance Criteria:
- [ ] Display practices in card view layout (grid format)
- [ ] Each practice card shows: Practice Name, Description, Admin Count, Member Count, Status
- [ ] Display practice count at the top
- [ ] Show active and inactive practices with visual indicators
- [ ] Empty state message displayed when no practices exist
- [ ] Cards are responsive and adjust to screen size
- [ ] Hover effect on practice cards

### UI Elements:
- Practice cards in grid layout (3-4 per row on desktop)
- Practice count badge
- Status indicator (active/inactive badge)
- Action menu on each card
- Empty state with illustration
- Search and filter bar

### Business Rules:
- Only Master Admin can view and manage practices
- Display all practices (active and inactive) with filter option

### Related FR: FR#PMP-4 - List All Practices

---

## US-004.2: Search and Filter Practices
**As a** Master Admin  
**I want to** search and filter practices  
**So that** I can quickly find specific practices

### Acceptance Criteria:
- [ ] Search box allows searching by practice name or description
- [ ] Search results update as user types (debounced)
- [ ] Filter by status (dropdown: All, Active, Inactive)
- [ ] "Clear Search" button visible when search is active
- [ ] Display count of filtered results
- [ ] No results message displayed when search yields no matches

### UI Elements:
- Search input field with search icon
- Status filter dropdown
- Clear search button
- Results count label
- No results message

---

## US-004.3: Create New Practice
**As a** Master Admin  
**I want to** create a new practice  
**So that** I can organize users and opportunities by business units

### Acceptance Criteria:
- [ ] "Add Practice" button displayed prominently at the top
- [ ] Clicking button opens "Create Practice" modal/form
- [ ] Form displays required fields: Practice Name, Description
- [ ] Practice Name field (min 2, max 50 characters, required)
- [ ] Description field (max 500 characters, optional)
- [ ] Source dropdown (Web, Mobile, API, Admin, required)
- [ ] "Assign Admins" multi-select dropdown (optional, can assign later)
- [ ] Practice name uniqueness validated in real-time
- [ ] "Create" button enabled when required fields are valid
- [ ] "Cancel" button closes form without saving
- [ ] Display validation errors inline
- [ ] Success notification shows created practice details
- [ ] New practice appears in practice list immediately

### UI Elements:
- "Add Practice" button (primary action)
- Modal form with fields:
  - PracticeName (text input, required)
  - Description (textarea, optional)
  - AssignAdmins (multi-select dropdown, optional)
  - Source (dropdown, required)
- Create button (primary)
- Cancel button (secondary)
- Inline validation messages
- Success toast notification

### Business Rules:
- Only Master Admin can create practices
- Practice name must be unique across system
- New practice is active by default (IsActive = true)
- System-generated PracticeID (GUID)
- CreatedDate and ModifiedDate set to current timestamp
- ModUser set to current user ID

### Related FR: FR#PMP-1 - Create New Practice

---

## US-004.4: View/Edit Practice Details
**As a** Master Admin  
**I want to** view and edit detailed information about a practice  
**So that** I can see complete practice information and update details when needed

### Acceptance Criteria:
- [ ] Clicking practice card opens practice detail modal/page in view mode
- [ ] Display practice information: Name, Description, Status
- [ ] Show assigned admins list with names and contact info
- [ ] Display member count in practice
- [ ] Show active opportunities count for practice
- [ ] Display audit information: Created Date, Modified Date
- [ ] "Edit" button enables editing mode (toggles view to edit mode)
- [ ] In edit mode:
  - Form fields become editable with pre-populated data
  - Allow editing: Practice Name, Description
  - Practice name uniqueness validated (excluding current practice)
  - All validations apply
- [ ] "Save" button updates practice and displays success message (in edit mode)
- [ ] "Cancel" button discards changes and returns to view mode
- [ ] "Deactivate" button available in view mode
- [ ] "Manage Admins" button to assign/remove admins
- [ ] "Close" button returns to practice list
- [ ] Audit fields updated automatically when saved (ModifiedDate, ModUser)
- [ ] Updated practice card reflects changes immediately

### UI Elements:
- Practice detail modal/page with view/edit toggle
- Information sections: Basic Info, Assigned Admins, Statistics, Audit Info
- Action buttons (view mode): Edit, Deactivate, Manage Admins, Close
- Action buttons (edit mode): Save, Cancel
- Editable form fields (in edit mode)
- Admin list with profile cards
- Statistics cards (Members, Opportunities)
- Success notification

### Business Rules:
- Practice name must remain unique
- Cannot edit PracticeID
- Cannot edit if practice has active dependencies (validate server-side)
- ModifiedDate and ModUser updated on save

### Related FR: FR#PMP-3 - Get Practice Details, FR#PMP-2 - Update Practice Details

---

## US-004.5: Assign Practice Admins
**As a** Master Admin  
**I want to** assign or remove admins for a practice  
**So that** practices have dedicated administrators

### Acceptance Criteria:
- [ ] "Manage Admins" button in practice detail view opens admin assignment modal
- [ ] Display currently assigned admins list
- [ ] Multi-select dropdown to add new admins (filtered to show Master Admin and Practice Admin roles)
- [ ] Each assigned admin has "Remove" button
- [ ] Confirmation dialog before removing admin
- [ ] "Save Changes" button applies admin assignments
- [ ] Success message confirms admin assignment/removal
- [ ] Updated admin list reflected in practice details

### UI Elements:
- Manage Admins modal
- Current admins list with remove buttons
- Add Admins multi-select dropdown
- Save Changes button
- Confirmation dialog for removal
- Success notification

### Business Rules:
- Only users with Master Admin or Practice Admin roles can be assigned
- Practice can have multiple admins
- Cannot remove last admin if practice has active users/opportunities (optional rule)
- Admin assignment creates/updates MemberPracticeMapping

---

## US-004.6: Deactivate Practice
**As a** Master Admin  
**I want to** deactivate a practice  
**So that** inactive practices are not shown in dropdowns and operations

### Acceptance Criteria:
- [ ] "Deactivate" button available in practice detail view
- [ ] Clicking "Deactivate" displays confirmation dialog
- [ ] Confirmation explains consequences (practice hidden from dropdowns, no new assignments)
- [ ] User must confirm deactivation action
- [ ] Upon confirmation, practice IsActive status set to false
- [ ] Deactivated practice shown with "Inactive" badge in list
- [ ] Success message displayed after deactivation
- [ ] Deactivated practice still viewable but not selectable in dropdowns

### UI Elements:
- Deactivate button
- Confirmation dialog with warning
- Inactive status badge
- Success notification

### Business Rules:
- Cannot deactivate practice with active hiring opportunities (validate server-side)
- Can deactivate practice with assigned users (users remain assigned but practice inactive)
- Deactivation is soft delete (IsActive = false)
- DeactivatedDate and DeactivatedBy recorded
- Deactivated practices appear in list with filter

### Related FR: FR#PMP-5 - Deactivate Practice

---

## US-004.7: Reactivate Practice
**As a** Master Admin  
**I want to** reactivate a previously deactivated practice  
**So that** it can be used again for operations

### Acceptance Criteria:
- [ ] "Reactivate" button available for inactive practices
- [ ] Clicking "Reactivate" displays confirmation dialog
- [ ] Upon confirmation, practice IsActive status set to true
- [ ] Reactivated practice appears as active in list
- [ ] Success message displayed after reactivation
- [ ] Practice becomes selectable in dropdowns again

### UI Elements:
- Reactivate button (for inactive practices)
- Confirmation dialog
- Success notification

---

## US-004.8: View Practice Statistics
**As a** Master Admin  
**I want to** see statistics for each practice  
**So that** I understand practice utilization and activity

### Acceptance Criteria:
- [ ] Display member count for each practice (on card)
- [ ] Display active opportunities count (on card)
- [ ] In detail view, show additional stats:
  - Total panel members
  - Total candidates
  - Scheduled interviews (this month)
  - Completed interviews (this month)
- [ ] Statistics update in real-time or on refresh

### UI Elements:
- Stat badges on practice cards
- Detailed statistics section in practice detail view
- Refresh button for stats

---

## US-004.9: Sort Practice List
**As a** Master Admin  
**I want to** sort practices by different criteria  
**So that** I can organize practices meaningfully

### Acceptance Criteria:
- [ ] Sort dropdown with options: Name (A-Z), Name (Z-A), Newest First, Oldest First, Most Members
- [ ] Selecting sort option reorganizes practice cards
- [ ] Default sort: Name (A-Z)
- [ ] Sort persists during session

### UI Elements:
- Sort dropdown above practice grid
- Sort direction indicator

---

## Technical Notes:
- Implement server-side validation for practice name uniqueness
- Use optimistic UI updates for better UX
- Cache practice list with periodic refresh
- Log all practice management actions for audit
- Implement responsive grid layout for practice cards
- Handle long practice names and descriptions with truncation and tooltips

## Related Functional Requirements:
- FR#PMP-1 - Create New Practice
- FR#PMP-2 - Update Practice Details
- FR#PMP-3 - Get Practice Details
- FR#PMP-4 - List All Practices
- FR#PMP-5 - Deactivate Practice

## Priority: P0 (Critical)
## Estimated Story Points: 10
