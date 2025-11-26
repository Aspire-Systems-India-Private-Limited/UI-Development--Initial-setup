# Interview Management Platform – Detailed UI/UX & App Design Document

## Table of Contents
1. Introduction
2. Feature List & User Story Mapping
3. User Roles & Access Matrix
4. Data Model & Entity Relationships
5. Screen-by-Screen Wireframe Descriptions
6. User Flows (Step-by-Step)
7. UI Component Inventory & Design System
8. API Integration Points
9. Responsive & Accessibility Guidelines
10. Error Handling & Validation
11. Appendix: Reference User Stories

---

## 1. Introduction
This document provides a comprehensive blueprint for designing and building the Interview Management Platform web application. It covers all modules, user stories, screens, flows, and technical integration points required for a production-ready React/Angular app.

## 2. Feature List & User Story Mapping
- Authentication & Authorization
- User Management
- Practice Management
- Role & JD Management
- Interview Panel Management
- Interview Slot Management
- Interview Scheduling
- Feedback Management
- Dashboard & Reporting

(Each feature is mapped to user stories and requirements in the appendix.)

## 3. User Roles & Access Matrix
| Page/Feature                | Master Admin | Practice Admin | Panel Member | TA Team |
|-----------------------------|:------------:|:--------------:|:------------:|:-------:|
| Dashboard                   |      ✅      |      ✅        |      ✅      |   ✅    |
| User Management             |      ✅      |      ❌        |      ❌      |   ❌    |
| Practice Management         |      ✅      |      ❌        |      ❌      |   ❌    |
| Designation Management      |      ✅      |      ✅        |      ❌      |   ❌    |
| JD Management               |      ❌      |      ✅        |      ❌      |   ❌    |
| Panel Management            |      ✅      |      ✅        |      ❌      |   ❌    |
| Slot Management (View All)  |      ❌      |      ✅        |      ❌      |   ✅    |
| Slot Management (Personal)  |      ❌      |      ❌        |      ✅      |   ❌    |
| Opportunities               |      ❌      |      ❌        |      ❌      |   ✅    |
| Candidate Profiles          |      ❌      |      ❌        |      ❌      |   ✅    |
| Interview Scheduling        |      ❌      |      ❌        |      ❌      |   ✅    |
| Feedback Submission         |      ❌      |      ❌        |      ✅      |   ❌    |
| Feedback Review             |      ❌      |      ✅        |      ✅*     |   ✅    |
| Feedback Templates          |      ✅      |      ✅        |      ❌      |   ❌    |
| My Interviews               |      ❌      |      ❌        |      ✅      |   ❌    |
| Profile Settings            |      ✅      |      ✅        |      ✅      |   ✅    |

*Panel Member: Can review own feedback only.

## 4. Data Model & Entity Relationships
- Users, Practices, Designations, JDs, Panel Members, Slots, Opportunities, Profiles, Interviews, Feedback, Feedback Templates
- (See detailed ER diagram and field mapping in Appendix)

## 5. Screen-by-Screen Wireframe Descriptions
(For each screen: purpose, layout, fields, actions, navigation, validation)
- Login
- Dashboard (role-based)
- User Management (list, add/edit, delete)
- Practice Management (list, add/edit, delete)
- Designation/JD Management (tabs, forms)
- Panel Member Management (list, add/edit, assign)
- Slot Management (calendar/table, add/edit, filter)
- Opportunity Management (list, add/edit, close)
- Candidate Profile Management (list, add/edit)
- Interview Scheduling (list, schedule, reschedule, cancel)
- Feedback Management (submit, review, templates)

---

### Login Screen
**Purpose:** Authenticate users and direct them to their role-based dashboard.
**Layout:**
---------------------------------------------------
| [Logo]                                          |
| Email:        [______________]                  |
| Password:     [______________]                  |
| [Login]                                         |
| [Error Message]                                 |
---------------------------------------------------
**Actions:** Login, error display.
**Validation:** Required fields, email format.

### Dashboard (Role-based)
**Purpose:** Show key stats, recent activity, and quick navigation for each role.
**Layout:**
---------------------------------------------------
| [Sidebar] | [Stat Cards] [Recent Activity]       |
|           | [Upcoming Items/Shortcuts]          |
---------------------------------------------------
**Actions:** Navigate to modules, view stats.

### User Management
**Purpose:** Manage users (add, edit, delete, assign roles/practices).
**Layout:**
---------------------------------------------------
| Name | Email | Role | Practice | Actions         |
|-----------------------------------------------   |
| ...rows...                                      |
| [Add User]                                      |
---------------------------------------------------
**Actions:** Add, edit, delete user.
**Validation:** Required fields, unique email, role/practice selection.

### Practice Management
**Purpose:** Manage practices and assign admins.
**Layout:**
---------------------------------------------------
| [Practice Card]  [Practice Card]  ...           |
| [Add Practice]                                  |
---------------------------------------------------
**Actions:** Add, edit, delete practice, assign admins.
**Validation:** Required fields.

### Designation/JD Management
**Purpose:** Manage designations and job descriptions.
**Layout:**
---------------------------------------------------
| [Tabs: Designations | JDs]                      |
| [Table/List]                                    |
| [Add/Edit/Delete]                               |
---------------------------------------------------
**Actions:** Add, edit, delete designation/JD.
**Validation:** Required fields, association with practice/designation.

### Panel Member Management
**Purpose:** Manage panel members, assign roles/levels/practices.
**Layout:**
---------------------------------------------------
| Name | Role | Level | Practice | Actions         |
|-----------------------------------------------   |
| ...rows...                                      |
| [Add Panel Member]                              |
---------------------------------------------------
**Actions:** Add, edit, delete, assign panel member.
**Validation:** Required fields, unique email.

### Slot Management
**Purpose:** Manage and view interview slots (calendar or table view).
**Layout:**
---------------------------------------------------
| [Calendar/Table View]                           |
| [Add/Edit Slot]                                 |
---------------------------------------------------
**Actions:** Add, edit, delete, filter slots.
**Validation:** Date/time, status, required fields.

### Opportunity Management
**Purpose:** Manage interview opportunities.
**Layout:**
---------------------------------------------------
| Title | Designation | JD | Status | Candidates | Actions |
|---------------------------------------------------------|
| ...rows...                                              |
| [Add Opportunity]                                       |
----------------------------------------------------------
**Actions:** Add, edit, close, delete opportunity.
**Validation:** Required fields, associations.

### Candidate Profile Management
**Purpose:** Manage candidate profiles.
**Layout:**
---------------------------------------------------
| Name | Email | Phone | Opportunity | Status | Actions    |
|---------------------------------------------------------|
| ...rows...                                              |
| [Add Candidate]                                         |
----------------------------------------------------------
**Actions:** Add, edit, delete candidate.
**Validation:** Required fields, unique email/phone.

### Interview Scheduling
**Purpose:** Schedule, reschedule, and cancel interviews.
**Layout:**
---------------------------------------------------
| Candidate | Opportunity | Panel | Slot | Level | Status | Actions |
|-------------------------------------------------------------|
| ...rows...                                                  |
| [Schedule Interview]                                        |
--------------------------------------------------------------
**Actions:** Schedule, reschedule, cancel interview.
**Validation:** Required fields, slot availability.

### Feedback Management
**Purpose:** Submit and review interview feedback.
**Layout:**
---------------------------------------------------
| Candidate | Panel | Date | Rating | Decision | Actions |
|---------------------------------------------------------|
| ...rows...                                              |
| [View Details]                                          |
----------------------------------------------------------
**Actions:** Submit, review feedback, view details.
**Validation:** Required fields, rating, comments.

### Feedback Template Management
**Purpose:** Create/edit feedback templates per role.
**Layout:**
---------------------------------------------------
| Role | Template Name | Sections | Actions         |
|--------------------------------------------------|
| ...rows...                                       |
| [Add Template]                                   |
---------------------------------------------------
**Actions:** Add, edit, delete template, manage sections.
**Validation:** Required fields, section names.

---

For each screen, use clear sectioning, consistent form layouts, and role-based navigation. These wireframe descriptions and layout suggestions can be quickly translated into Figma by a designer.

## 6. User Flows (Step-by-Step)
- Onboard User
- Create Practice
- Add Designation/JD
- Add Panel Member
- Add Slot
- Create Opportunity
- Add Candidate Profile
- Schedule Interview
- Submit Feedback
- Review Feedback

---

### User Flow Diagrams (ASCII)

#### 1. Onboard User
Dashboard
	|
	v
User Management
	|
	v
[Add User] → User Form → [Save]
	|
	v
User List (updated)

#### 2. Create Practice
Dashboard
	|
	v
Practice Management
	|
	v
[Add Practice] → Practice Form → [Save]
	|
	v
Practice List (updated)

#### 3. Add Designation/JD
Dashboard
	|
	v
Designation/JD Management
	|
	v
[Add Designation/JD] → Form → [Save]
	|
	v
Designation/JD List (updated)

#### 4. Add Panel Member
Dashboard
	|
	v
Panel Member Management
	|
	v
[Add Panel Member] → Form → [Save]
	|
	v
Panel Member List (updated)

#### 5. Add Slot
Dashboard
	|
	v
Slot Management
	|
	v
[Add Slot] → Slot Form → [Save]
	|
	v
Slot Calendar/Table (updated)

#### 6. Create Opportunity
Dashboard
	|
	v
Opportunity Management
	|
	v
[Add Opportunity] → Opportunity Form → [Save]
	|
	v
Opportunity List (updated)

#### 7. Add Candidate Profile
Dashboard
	|
	v
Candidate Profile Management
	|
	v
[Add Candidate] → Candidate Form → [Save]
	|
	v
Candidate List (updated)

#### 8. Schedule Interview
Dashboard
	|
	v
Interview Scheduling
	|
	v
[Schedule Interview] → Schedule Form → [Save]
	|
	v
Interview List (updated)

#### 9. Submit Feedback
Dashboard
	|
	v
Feedback Management
	|
	v
[Submit Feedback] → Feedback Form → [Save]
	|
	v
Feedback List (updated)

#### 10. Review Feedback
Dashboard
	|
	v
Feedback Management
	|
	v
[View Details] → Feedback Details Dialog

## 7. UI Component Inventory & Design System
- Table, Card, Modal, Form Input, Dropdown, Date/Time Picker, Tabs, Pagination, Button, Toast/Alert, Sidebar, Header, Stat Card, etc.
- Color coding, role badges, status indicators, accessibility notes

## 8. API Integration Points
- List of endpoints for each module
- Data contract (request/response fields)
- Error handling

## 9. Responsive & Accessibility Guidelines
- Breakpoints, mobile/tablet/desktop layouts
- ARIA, keyboard navigation, color contrast, focus management

## 10. Error Handling & Validation
- Inline errors, toast notifications, empty/loading/error states
- Field-level validation rules

## 11. Appendix: Reference User Stories
- List of all user stories and requirements, mapped to features/screens

---

(Each section to be expanded with detailed content as needed. Let me know which section you want to fill in next!)
