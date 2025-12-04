# User Stories: Dashboard Screen

## Module: Dashboard
**Reference:** Figma_All_Screens.md - Section 2 (Dashboard Screen)

---

## US-002.1: View Role-Based Dashboard
**As a** logged-in system user  
**I want to** see a personalized dashboard based on my role  
**So that** I can quickly access relevant information and features

### Acceptance Criteria:
- [ ] Dashboard displays immediately after successful login
- [ ] Layout includes navigation sidebar, stat cards, and recent activity sections
- [ ] Stat cards show key metrics relevant to user's role
- [ ] Navigation sidebar displays only modules accessible to user's role
- [ ] User name and role are displayed in the header
- [ ] Dashboard content updates in real-time or on refresh

### UI Elements:
- Header with user profile and logout option
- Left navigation sidebar with menu items
- Main content area with stat cards
- Recent activity/upcoming items section
- Quick action buttons (role-specific)

### Business Rules:
- Master Admin sees all system statistics across practices
- Practice Admin sees statistics for their assigned practice only
- TA Team Admin sees candidate and interview scheduling statistics
- Tech Panel Member sees their upcoming interviews and slot availability

---

## US-002.2: Master Admin Dashboard View
**As a** Master Admin  
**I want to** see system-wide statistics and metrics  
**So that** I can monitor overall system health and activities

### Acceptance Criteria:
- [ ] Display total number of active practices
- [ ] Display total number of system users by role
- [ ] Display total active hiring opportunities across all practices
- [ ] Display total candidates in the system
- [ ] Display total scheduled interviews (today, this week, this month)
- [ ] Display recent system activities (new users, practices, opportunities)
- [ ] Display pending actions requiring attention
- [ ] All navigation menu items are accessible (no restrictions)

### UI Elements:
- Stat cards: Total Practices, Total Users, Active Opportunities, Total Candidates, Scheduled Interviews
- Recent Activity feed
- Quick actions: Add Practice, Add User

### Navigation Menu Items:
- Dashboard
- User Management
- Practice Management
- Designation & JD Management
- Panel Member Management
- Slot Management
- Opportunity Management
- Candidate Management
- Interview Scheduling
- Feedback Management

---

## US-002.3: Practice Admin Dashboard View
**As a** Practice Admin  
**I want to** see statistics and activities for my assigned practice  
**So that** I can manage practice-specific operations effectively

### Acceptance Criteria:
- [ ] Display practice name in dashboard header
- [ ] Display total users in assigned practice
- [ ] Display active hiring opportunities for practice
- [ ] Display candidates associated with practice opportunities
- [ ] Display scheduled interviews for practice
- [ ] Display panel members available in practice
- [ ] Display recent activities within practice scope
- [ ] Navigation menu shows only practice-scoped modules

### UI Elements:
- Practice name badge/label
- Stat cards: Practice Users, Active Opportunities, Candidates, Panel Members, Interviews
- Recent Activity feed (practice-scoped)
- Quick actions: Add Panel Member, Create Opportunity, Schedule Interview

### Navigation Menu Items:
- Dashboard
- Practice Users Management
- Panel Member Management
- Designation & JD Management (practice-specific)
- Slot Management (practice members)
- Opportunity Management (practice)
- Candidate Management (practice)
- Interview Scheduling (practice)
- Feedback Review

---

## US-002.4: TA Team Admin Dashboard View
**As a** TA Team Admin  
**I want to** see candidate and interview scheduling metrics  
**So that** I can efficiently manage recruitment activities

### Acceptance Criteria:
- [ ] Display total candidates under management
- [ ] Display interviews scheduled (pending, completed, cancelled)
- [ ] Display upcoming interviews (today and this week)
- [ ] Display candidates by status (pending, scheduled, completed, rejected)
- [ ] Display pending interview reschedule requests
- [ ] Display pending feedback submissions
- [ ] Display recent candidate profile updates
- [ ] Quick access to scheduling and candidate management features

### UI Elements:
- Stat cards: Total Candidates, Pending Interviews, Completed Interviews, Reschedule Requests
- Calendar view with upcoming interviews
- Recent Activity: New candidates, schedule changes
- Quick actions: Add Candidate, Schedule Interview, View Requests

### Navigation Menu Items:
- Dashboard
- Opportunity Management (view only)
- Candidate Management
- Interview Scheduling
- Interview Reschedule Requests
- Feedback Review

---

## US-002.5: Tech Panel Member Dashboard View
**As a** Tech Panel Member  
**I want to** see my upcoming interviews and availability  
**So that** I can prepare for interviews and manage my schedule

### Acceptance Criteria:
- [ ] Display upcoming interviews assigned to me (today, this week)
- [ ] Display interview details: candidate name, time, designation, type
- [ ] Display my current slot availability status
- [ ] Display pending feedback submissions
- [ ] Display total interviews conducted (this month, all-time)
- [ ] Display calendar view of my interview schedule
- [ ] Quick access to slot management and feedback submission

### UI Elements:
- Stat cards: Upcoming Interviews, Pending Feedback, Interviews Conducted
- Calendar with interview schedule
- Interview cards with candidate details
- Availability status indicator
- Quick actions: Manage Slots, Submit Feedback, View Details

### Navigation Menu Items:
- Dashboard
- My Interview Schedule
- Slot Management (my slots)
- Feedback Submission
- Interview History

---

## US-002.6: Navigate from Dashboard to Modules
**As a** system user  
**I want to** navigate to different modules from the dashboard  
**So that** I can access various features of the system

### Acceptance Criteria:
- [ ] Sidebar menu displays all accessible modules for user role
- [ ] Clicking menu item navigates to respective module
- [ ] Active menu item is visually highlighted
- [ ] Breadcrumb navigation shows current location
- [ ] "Back to Dashboard" option available in all screens
- [ ] Menu can be collapsed/expanded for more screen space

### UI Elements:
- Collapsible navigation sidebar
- Menu items with icons and labels
- Active state indicator
- Breadcrumb trail
- Home/Dashboard button

---

## US-002.7: View Recent Activity Feed
**As a** system user  
**I want to** see recent activities and updates relevant to my role  
**So that** I stay informed about important changes and actions

### Acceptance Criteria:
- [ ] Recent activity section displays chronological list of activities
- [ ] Each activity shows: timestamp, action type, actor, and brief description
- [ ] Activities are filtered based on user's role and scope
- [ ] Click on activity item navigates to relevant detail page
- [ ] Display "No recent activities" message if feed is empty
- [ ] Show last 10 activities with "View All" option

### UI Elements:
- Activity feed container
- Activity items with icons, timestamps, and descriptions
- "View All Activities" link
- Refresh button for manual updates

### Activity Types:
- New user onboarded
- Practice created/updated
- Opportunity created/updated
- Candidate profile added
- Interview scheduled/rescheduled
- Feedback submitted
- User role changed

---

## US-002.8: Display Quick Action Buttons
**As a** system user  
**I want to** access frequently used actions quickly from the dashboard  
**So that** I can perform common tasks efficiently

### Acceptance Criteria:
- [ ] Quick action buttons displayed prominently on dashboard
- [ ] Buttons vary based on user role and permissions
- [ ] Clicking button opens relevant form/modal or navigates to feature
- [ ] Buttons have clear labels and icons
- [ ] Tooltips provide additional context on hover

### UI Elements:
- Quick action button group
- Primary action buttons with icons
- Hover tooltips

### Quick Actions by Role:
**Master Admin:** Add Practice, Add User  
**Practice Admin:** Add Panel Member, Create Opportunity, Schedule Interview  
**TA Team Admin:** Add Candidate, Schedule Interview, View Requests  
**Tech Panel Member:** Manage Slots, Submit Feedback, View Schedule

---

## US-002.9: Dashboard Data Auto-Refresh
**As a** system user  
**I want to** see updated dashboard data automatically  
**So that** I always have current information without manual refresh

### Acceptance Criteria:
- [ ] Dashboard data refreshes automatically every 5 minutes
- [ ] User can manually trigger refresh with refresh button
- [ ] Loading indicator shows during data refresh
- [ ] Refresh doesn't disrupt user interaction with dashboard
- [ ] Last updated timestamp displayed

### UI Elements:
- Refresh button
- Last updated timestamp
- Loading spinner/indicator

---

## Technical Notes:
- Implement role-based rendering for dashboard components
- Use WebSocket or polling for real-time updates
- Optimize API calls to fetch role-specific data only
- Implement caching for improved performance
- Ensure responsive design for mobile and tablet views

## Related Functional Requirements:
- FR#AUTH-3: Role-Based Access Control
- FR#Dashboard-1: Display Role-Based Statistics

## Priority: P0 (Critical)
## Estimated Story Points: 8
