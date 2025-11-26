# Figma Design Handoff: All Screens Overview

This document summarizes all screens, fields, actions, and layout suggestions for the Interview Management Platform. Use this as a master reference for Figma design.

---

## 1. Login Screen
**Purpose:** Authenticate users and direct them to their role-based dashboard.
**Fields:**
- Email (required, email format)
- Password (required)
**Actions:** Login, show error message on failure
**Layout:**
[Logo]
Email: [__________]
Password: [__________]
[Login]
[Error Message]

---

## 2. Dashboard Screen
**Purpose:** Show key stats, recent activity, and quick navigation for each role.
**Fields/Components:**
- Stat Cards (customized per role)
- Recent Activity/Upcoming Items
- Navigation Sidebar
**Actions:** Navigate to modules, view stats and activity
**Layout:**
[Sidebar] [Stat Cards] [Recent Activity]

---

## 3. User Management Screen
**Purpose:** Manage users (add, edit, delete, assign roles/practices).
**Fields:**
- UserName (required, unique)
- FirstName (required)
- LastName (required)
- Password (auto-generated, required)
- RoleID (dropdown, required)
- EmailID (required, unique, email format)
- PhoneNumber (required, unique)
- PracticeID (dropdown, required for non-Master Admin)
- Source (dropdown, required)
**Actions:** Add User, Edit User, Delete User
**Layout:**
Name | Email | Role | Practice | Actions
[Add User]

---

## 4. Practice Management Screen
**Purpose:** Manage practices and assign admins.
**Fields:**
- Practice Name (required)
- Description (required)
- Assign Admins (multi-select)
- Source (dropdown, required)
**Actions:** Add Practice, Edit Practice, Delete Practice
**Layout:**
[Practice Card] [Practice Card] ...
[Add Practice]

---

## 5. Designation & JD Management Screen
**Purpose:** Manage designations and job descriptions.
**Fields:**
- Designation: Title (required), Practice (dropdown, required)
- JD: Title (required), Designation (dropdown, required), Description (textarea), Requirements (dynamic list)
**Actions:** Add/Edit/Delete Designation, Add/Edit/Delete JD
**Layout:**
[Tabs: Designations | JDs]
[Table/List]
[Add/Edit/Delete]

---

## 6. Panel Member Management Screen
**Purpose:** Manage panel members, assign roles/levels/practices.
**Fields:**
- UserName (required, unique)
- FirstName (required)
- LastName (required)
- Password (auto-generated, required)
- RoleID (dropdown, required)
- EmailID (required, unique, email format)
- PhoneNumber (required, unique)
- PracticeID (dropdown, required)
- Source (dropdown, required)
- MemberPanelApplicabilityID (system-generated, for mapping)
**Actions:** Add Panel Member, Edit Panel Member, Delete Panel Member
**Layout:**
Name | Role | Level | Practice | Actions
[Add Panel Member]

---

## 7. Slot Management Screen
**Purpose:** Manage and view interview slots (calendar or table view).
**Fields:**
- Date (required)
- Start Time (required)
- End Time (required)
- Status (dropdown: available/blocked/unavailable)
- Reason (optional, for blocked/unavailable)
- Panel Member (dropdown, required for admin/TA)
- Source (dropdown, required)
**Actions:** Add Slot, Edit Slot, Delete Slot, Filter Slots
**Layout:**
[Calendar/Table View]
[Add/Edit Slot]

---

## 8. Opportunity Management Screen
**Purpose:** Manage interview opportunities.
**Fields:**
- Title (required)
- Designation (dropdown, required)
- JD (dropdown, required)
- Practice (dropdown, required)
- Status (open/closed)
- Candidate Count (auto)
- AdditionalNotes (textarea, optional)
- PlannedCandidatesCount (number, optional)
- Source (dropdown, required)
- DeactivationReason (textarea, optional)
- DeactivatedDate (date, optional)
**Actions:** Add Opportunity, Edit Opportunity, Close Opportunity, Delete Opportunity
**Layout:**
Title | Designation | JD | Status | Candidates | Actions
[Add Opportunity]

---

## 9. Candidate Profile Management Screen
**Purpose:** Manage candidate profiles.
**Fields:**
- FirstName (required)
- LastName (required)
- Email (required, unique)
- Phone (required, unique)
- Opportunity (dropdown, required)
- Status (pending/scheduled/completed/rejected)
- DesignationAppliedFor (dropdown, required)
- DesignationPresentedFor (dropdown, optional)
- YearsOfExperience (number, required)
- CandidateSource (dropdown, required)
- ResumeDocument (file upload, required)
- MappedTATeamMemberID (dropdown, required)
- Source (dropdown, required)
**Actions:** Add Candidate, Edit Candidate, Delete Candidate
**Layout:**
Name | Email | Phone | Opportunity | Status | Actions
[Add Candidate]

---

## 10. Interview Scheduling Screen
**Purpose:** Schedule, reschedule, and cancel interviews.
**Fields:**
- Title (required)
- Notes (textarea, optional)
- TechnicalPanelMemberID (dropdown, required)
- CandidateProfileID (dropdown, required)
- HiringOpportunityID (dropdown, required)
- InterviewTypeID (dropdown, required)
- AvailabilityID (dropdown, required)
- ScheduledDate (date, required)
- ScheduledTimeslotFrom (time, required)
- ScheduledTimeslotTo (time, required)
- StatusID (dropdown, required)
- Source (dropdown, required)
**Actions:** Schedule Interview, Reschedule Interview, Cancel Interview
**Layout:**
Candidate | Opportunity | Panel | Slot | Level | Status | Actions
[Schedule Interview]

---

## 11. Feedback Management Screen
**Purpose:** Submit and review interview feedback.
**Fields:**
**Actions:** Submit Feedback, Review Feedback, View Details
**Layout:**
Candidate | Panel | Date | Rating | Decision | Actions
[View Details]


## 12. Interview Reschedule Request Screen
**Purpose:** Request and manage interview rescheduling.
**Fields:**
- InterviewRescheduleRequestID (system-generated)
- InterviewScheduleID (dropdown, required)
- PreviousInterviewScheduleID (dropdown, auto)
- NewInterviewScheduleID (dropdown, required)
- Reason (textarea, required)
- RequestStatus (dropdown, required)
- IsActive (checkbox, required)
- CreatedDate (auto)
- ModifiedDate (auto)
- ModUser (auto)
- Source (dropdown, required)
**Actions:** Create Request, Approve/Reject Request
**Layout:**
RequestID | Interview | Previous | New | Reason | Status | Actions
[Create Request]
This document is ready for Figma design handoff. Each section can be used to create a dedicated Figma screen with all required fields and actions.
---

## 13. Hiring Opportunity Deactivation History Screen
**Purpose:** Track deactivation history for opportunities.
**Fields:**
- DeactivationHistoryID (system-generated)
- HiringOpportunityID (dropdown, required)
- Reason (textarea, required)
- DeactivatedBy (dropdown, required)
- DeactivatedDate (date, required)
- PreviousStatusID (dropdown, auto)
- NewStatusID (dropdown, required)
- CreatedDate (auto)
- Source (dropdown, required)
**Actions:** View History
**Layout:**
DeactivationHistoryID | Opportunity | Reason | By | Date | Status (Prev/New) | Source
