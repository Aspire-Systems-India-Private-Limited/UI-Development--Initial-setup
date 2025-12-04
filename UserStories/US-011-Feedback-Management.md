# User Stories: Feedback Management Screen

## Module: Interview Feedback Management
**Reference:** Figma_All_Screens.md - Section 11 (Feedback Management Screen)  
**Related FR:** FR#Feedback Management

---

## PART A: FEEDBACK SUBMISSION (Panel Member)

## US-011.1: View My Completed Interviews Requiring Feedback
**As a** Panel Member  
**I want to** see my completed interviews that need feedback  
**So that** I can submit feedback for them

### Acceptance Criteria:
- [ ] Display completed interviews assigned to logged-in panel member
- [ ] Show interviews with "Pending Feedback" status prominently
- [ ] Display interview details: Candidate Name, Date/Time, Designation, Interview Type
- [ ] Badge indicator showing "Feedback Pending" or "Feedback Submitted"
- [ ] "Submit Feedback" button available for pending feedback interviews
- [ ] Filter to show only pending feedback or all completed interviews
- [ ] Default sorting by interview date (most recent first)
- [ ] Count of pending feedback displayed

### UI Elements:
- Completed Interviews table/list
- Feedback status badges (Pending/Submitted)
- Submit Feedback button for each interview
- Filter toggle (Pending Feedback / All)
- Pending count indicator
- Interview cards with key details

### Business Rules:
- Panel members see only their own interviews
- Only completed interviews are eligible for feedback
- Feedback can be submitted within configured timeframe (e.g., 7 days after interview)
- Late feedback submissions flagged with warning

---

## US-011.2: Submit Interview Feedback
**As a** Panel Member  
**I want to** submit feedback for a completed interview  
**So that** candidate evaluation is recorded

### Acceptance Criteria:
- [ ] "Submit Feedback" button opens feedback submission form
- [ ] Display interview context: Candidate Name, Date/Time, Designation, Opportunity (read-only)
- [ ] Rating dropdown or star selector (1-5 stars, required)
- [ ] Decision dropdown (Selected, Rejected, On Hold, required)
- [ ] Feedback Comments textarea (required, min 50 characters)
- [ ] Strengths section (textarea, optional)
- [ ] Areas for Improvement section (textarea, optional)
- [ ] Technical Skills Rating (1-5, optional per skill area)
- [ ] Communication Skills Rating (1-5, optional)
- [ ] Cultural Fit Rating (1-5, optional)
- [ ] Attachments upload (optional, e.g., assessment sheets, notes)
- [ ] Source dropdown (Web, Mobile, API, required)
- [ ] "Submit Feedback" button enabled when required fields valid
- [ ] "Save as Draft" button to save incomplete feedback
- [ ] "Cancel" button closes form without saving
- [ ] Display validation errors inline
- [ ] Success notification confirms feedback submission
- [ ] Feedback becomes read-only after submission
- [ ] Interview status updated to "Feedback Submitted"

### UI Elements:
- "Submit Feedback" button (primary action)
- Modal/page form with sections:
  - Interview Context (read-only display)
  - Overall Rating (star selector or dropdown, required)
  - Decision (dropdown, required)
  - Detailed Feedback:
    - Feedback Comments (textarea, required)
    - Strengths (textarea, optional)
    - Areas for Improvement (textarea, optional)
  - Skill Ratings (optional):
    - Technical Skills (rating, optional)
    - Communication Skills (rating, optional)
    - Cultural Fit (rating, optional)
  - Attachments (file upload, optional)
  - Source (dropdown, required)
- Submit Feedback button (primary)
- Save as Draft button (secondary)
- Cancel button (secondary)
- Inline validation messages
- Success toast notification

### Business Rules:
- Feedback can only be submitted by assigned panel member
- Required fields: Rating, Decision, Feedback Comments
- Minimum character count for comments: 50 characters
- Feedback must be submitted within configured timeframe (warning after deadline)
- Attachments: PDF, DOC, DOCX, max 5MB per file
- System-generated InterviewFeedbackID (GUID)
- CreatedDate and ModifiedDate set to current timestamp
- ModUser set to panel member ID
- Notifications sent to TA Team Admin after submission
- Feedback becomes read-only after submission (or editable within grace period)

### Related FR: FR#Feedback Management - Submit Feedback

---

## US-011.3: Save Feedback as Draft
**As a** Panel Member  
**I want to** save incomplete feedback as draft  
**So that** I can complete it later

### Acceptance Criteria:
- [ ] "Save as Draft" button available in feedback form
- [ ] Draft saves all entered data without validation
- [ ] Draft can be reopened for editing
- [ ] Draft indicator shown for interviews with saved drafts
- [ ] Multiple saves update the same draft
- [ ] Success message confirms draft saved
- [ ] Draft retained until submitted or deleted

### UI Elements:
- Save as Draft button
- Draft status badge on interview list
- Success notification

### Business Rules:
- Drafts do not count as submitted feedback
- Interview status remains "Feedback Pending" for drafts
- Drafts auto-save periodically (optional)
- Drafts expire after configured period (e.g., 30 days)

---

## US-011.4: Edit Submitted Feedback (Grace Period)
**As a** Panel Member  
**I want to** edit my submitted feedback within a grace period  
**So that** I can correct mistakes immediately after submission

### Acceptance Criteria:
- [ ] "Edit Feedback" button available for feedback submitted within grace period (e.g., 1 hour)
- [ ] Opens feedback form in edit mode with pre-filled data
- [ ] All fields editable
- [ ] "Update Feedback" button saves changes
- [ ] Grace period countdown displayed
- [ ] After grace period, feedback becomes read-only
- [ ] Success message confirms update
- [ ] Audit trail records edit

### UI Elements:
- Edit Feedback button (visible during grace period)
- Grace period countdown timer
- Edit form with pre-filled data
- Update Feedback button
- Success notification

### Business Rules:
- Grace period: 1 hour after submission (configurable)
- After grace period, feedback locked (requires admin intervention to edit)
- Edit timestamp recorded
- TA Team Admin notified of edits

---

## US-011.5: View My Submitted Feedback
**As a** Panel Member  
**I want to** view feedback I've submitted  
**So that** I can review my evaluations

### Acceptance Criteria:
- [ ] "My Feedback History" view shows all submitted feedback
- [ ] Display feedback with interview details
- [ ] Filter by date range, decision, rating
- [ ] Click feedback to view full details (read-only)
- [ ] Search by candidate name

### UI Elements:
- My Feedback History section
- Feedback list/table
- Filters (date range, decision, rating)
- View Details link

---

---

## PART B: FEEDBACK REVIEW (TA Team Admin / Practice Admin)

## US-011.6: View All Interview Feedback
**As a** TA Team Admin or Practice Admin  
**I want to** view all interview feedback  
**So that** I can review candidate evaluations

### Acceptance Criteria:
- [ ] Display feedback in a table with columns: Candidate, Panel Member, Interview Date, Rating, Decision, Feedback Status, Actions
- [ ] TA Team Admin sees feedback for practice-scoped interviews
- [ ] Practice Admin sees feedback for practice panel members
- [ ] Master Admin sees all feedback
- [ ] Show feedback status badges: Pending, Submitted, Reviewed
- [ ] Default sorting by interview date (newest first)
- [ ] Display pending feedback count
- [ ] Empty state message when no feedback exists

### UI Elements:
- Feedback table with sortable columns
- Feedback status badges
- Pending count indicator
- Action menu for each row
- Search and filter controls
- Empty state illustration

### Business Rules:
- TA Team Admin: View feedback for candidates in practice scope
- Practice Admin: View feedback for practice panel members
- Master Admin: View all feedback

---

## US-011.7: View Feedback Details
**As a** TA Team Admin or Practice Admin  
**I want to** view complete feedback details  
**So that** I can evaluate candidate thoroughly

### Acceptance Criteria:
- [ ] Clicking feedback row opens detail modal/page
- [ ] Display all feedback information:
  - Interview context (Candidate, Panel Member, Date/Time, Designation, Opportunity)
  - Overall rating and decision
  - Feedback comments, strengths, areas for improvement
  - Skill ratings (technical, communication, cultural fit)
  - Attachments (view inline or in modal)
- [ ] Show submission timestamp and panel member info
- [ ] Display feedback status
- [ ] "Mark as Reviewed" button (if not yet reviewed)
- [ ] "Close" button returns to feedback list

### UI Elements:
- Feedback detail modal/page
- Information sections: Interview Context, Overall Evaluation, Detailed Feedback, Skill Ratings, Attachments
- Action buttons: Mark as Reviewed, Close
- Attachment viewer

---

## US-011.8: Mark Feedback as Reviewed
**As a** TA Team Admin or Practice Admin  
**I want to** mark feedback as reviewed  
**So that** feedback review progress is tracked

### Acceptance Criteria:
- [ ] "Mark as Reviewed" button available for submitted feedback
- [ ] Clicking button displays confirmation
- [ ] Upon confirmation, feedback status changed to "Reviewed"
- [ ] Review timestamp and reviewer recorded
- [ ] Success message confirms action
- [ ] Reviewed feedback shown with "Reviewed" badge
- [ ] Reviewed by and review date displayed in feedback details

### UI Elements:
- Mark as Reviewed button
- Confirmation dialog
- Success notification
- Reviewed badge
- Reviewer info display

### Business Rules:
- Only TA Team Admin and Practice Admin can mark as reviewed
- Review action logged in audit trail
- Reviewed status helps track feedback processing
- Optional: Review comments can be added

---

## US-011.9: Search and Filter Feedback
**As a** TA Team Admin or Practice Admin  
**I want to** search and filter feedback  
**So that** I can find specific feedback quickly

### Acceptance Criteria:
- [ ] Search box allows searching by candidate name, panel member name
- [ ] Search results update as user types (debounced)
- [ ] Filter by candidate (dropdown, searchable)
- [ ] Filter by panel member (dropdown)
- [ ] Filter by opportunity (dropdown)
- [ ] Filter by rating (1-5 stars)
- [ ] Filter by decision (Selected, Rejected, On Hold)
- [ ] Filter by feedback status (Pending, Submitted, Reviewed)
- [ ] Filter by date range (interview date)
- [ ] Multiple filters can be applied simultaneously
- [ ] "Clear Filters" button resets all filters
- [ ] Display count of filtered results

### UI Elements:
- Search input field
- Candidate filter dropdown
- Panel member filter dropdown
- Opportunity filter dropdown
- Rating filter
- Decision filter dropdown
- Feedback status filter dropdown
- Date range pickers
- Clear Filters button
- Results count label

---

## US-011.10: View Candidate Feedback Summary
**As a** TA Team Admin or Practice Admin  
**I want to** see aggregated feedback for a candidate  
**So that** I can make hiring decisions

### Acceptance Criteria:
- [ ] "View Candidate Feedback" option shows all feedback for selected candidate
- [ ] Display feedback from all interview rounds
- [ ] Show average rating across all interviews
- [ ] Show decision summary (e.g., 3/4 Selected, 1/4 On Hold)
- [ ] Display feedback from each round with panel member details
- [ ] Visual summary chart (ratings, decisions)
- [ ] Recommendation indicator based on feedback

### UI Elements:
- Candidate Feedback Summary view
- Average rating display
- Decision breakdown chart
- Feedback cards for each round
- Visual charts/graphs

---

## US-011.11: Compare Feedback Across Candidates
**As a** TA Team Admin  
**I want to** compare feedback for multiple candidates  
**So that** I can make comparative hiring decisions

### Acceptance Criteria:
- [ ] "Compare Candidates" feature allows selecting multiple candidates
- [ ] Side-by-side comparison view
- [ ] Display for each candidate: Average rating, decision summary, key feedback points
- [ ] Highlight differences and similarities
- [ ] Sort candidates by average rating

### UI Elements:
- Compare Candidates button
- Candidate selection interface
- Comparison table/view
- Sort controls

---

## US-011.12: Send Feedback Reminder to Panel Member
**As a** TA Team Admin  
**I want to** send reminders to panel members with pending feedback  
**So that** feedback is submitted timely

### Acceptance Criteria:
- [ ] "Send Reminder" action available for pending feedback
- [ ] Reminder sent via email and in-app notification
- [ ] Reminder includes interview details and deadline
- [ ] Success message confirms reminder sent
- [ ] Reminder history recorded
- [ ] Bulk reminder option for multiple pending feedback

### UI Elements:
- Send Reminder button/action
- Bulk Send Reminders option
- Success notification

### Business Rules:
- Automated reminders: 1 day and 3 days after interview
- Manual reminders can be sent anytime
- Escalation to practice admin if feedback overdue

---

## US-011.13: View Pending Feedback Dashboard
**As a** TA Team Admin  
**I want to** see a dashboard of pending feedback  
**So that** I can monitor feedback submission status

### Acceptance Criteria:
- [ ] Dashboard widget shows pending feedback statistics:
  - Total pending feedback count
  - Overdue feedback count
  - Feedback by panel member (breakdown)
  - Average feedback submission time
- [ ] Click widget to view pending feedback list
- [ ] Overdue feedback highlighted in red
- [ ] Panel members with most pending feedback identified
- [ ] "Send Reminders" quick action

### UI Elements:
- Pending Feedback Dashboard widget
- Statistics cards
- Overdue indicator
- Panel member breakdown chart
- Send Reminders button
- Navigation link to full list

---

## US-011.14: Sort Feedback List
**As a** system user  
**I want to** sort feedback by different columns  
**So that** I can organize feedback meaningfully

### Acceptance Criteria:
- [ ] Sortable columns: Interview Date, Candidate, Panel Member, Rating, Decision, Status
- [ ] Click column header to sort
- [ ] Sort indicator displayed
- [ ] Default sort: Interview Date (newest first)

### UI Elements:
- Sort indicators in column headers

---

## US-011.15: Pagination for Feedback List
**As a** system user  
**I want to** navigate through pages of feedback  
**So that** I can view large lists efficiently

### Acceptance Criteria:
- [ ] Display 20 feedback entries per page by default
- [ ] Page size selector: 10, 20, 50
- [ ] Page navigation controls

### UI Elements:
- Pagination controls at bottom of table

---

## US-011.17: Feedback Analytics Dashboard
**As a** Practice Admin or Master Admin  
**I want to** see feedback analytics  
**So that** I can understand interview and hiring trends

### Acceptance Criteria:
- [ ] Analytics dashboard shows:
  - Average rating by designation level
  - Decision distribution (Selected/Rejected/On Hold %)
  - Average feedback submission time
  - Top performing panel members (by rating given)
  - Interview success rate by opportunity
  - Feedback trends over time
- [ ] Visual charts and graphs
- [ ] Date range filter for analytics
- [ ] Drill-down capability to underlying data

### UI Elements:
- Feedback Analytics Dashboard
- Charts: Bar, Line, Pie, Donut
- Date range filter
- Drill-down links

---

## Technical Notes:
- Implement rich text editor for feedback comments
- Support file upload for attachments with virus scanning
- Log all feedback submissions and reviews for audit
- Implement automated reminder scheduler
- Generate PDF reports for feedback summary
- Calculate aggregated ratings and statistics
- Implement grace period logic for feedback editing
- Consider anonymous feedback option (future enhancement)
- Integrate with notification system for reminders

## Related Functional Requirements:
- FR#Feedback Management - Submit, Review, Retrieve Feedback
- FR#Interview Schedule Management (linked interviews)
- FR#Candidate Profile Management (linked candidates)

## Priority: P0 (Critical)
## Estimated Story Points: 13
