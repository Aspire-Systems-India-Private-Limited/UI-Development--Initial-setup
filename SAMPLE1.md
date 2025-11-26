Interview Management Platform - UI Flow Documentation
Table of Contents
Overview
Authentication Flow
Master Admin Flow
Practice Admin Flow
Panel Member Flow
TA Team Flow
Common Components
Overview
The Interview Management Platform supports four distinct user roles, each with tailored dashboards and navigation options:

Master Admin: System-wide oversight and configuration
Practice Admin: Practice-specific interview process management
Panel Member: Personal availability and interview management
TA Team: Candidate and interview scheduling coordination
Technology Stack
Frontend: React with TypeScript
UI Components: Shadcn/ui
Styling: Tailwind CSS
Icons: Lucide React
State Management: React Context API
Current Data: Mock data (ready for Supabase integration)
Authentication Flow
Login Screen
File: /components/login.tsx

Features:
Centralized login interface for all roles
Email and password authentication
Quick login buttons for demo/testing (4 role options)
Error handling with visual alerts
User Journey:
User lands on login screen with branded header
User enters email and password OR clicks quick login button
System validates credentials against mock user database
On success: Redirects to role-specific dashboard
On failure: Displays error message
Available Test Accounts:
Master Admin: admin@company.com
Practice Admin: practice.admin@company.com
Panel Member: panel.member@company.com
TA Team: ta.team@company.com
All passwords: password (mock authentication)

Master Admin Flow
Dashboard
File: /components/dashboard/master-admin-dashboard.tsx

Statistics Overview (4 Cards):
Total Users: System-wide user count
Active Practices: Number of practices in the organization
Designations: Total designation types across all practices
Scheduled Interviews: Upcoming interview count
Dashboard Sections:
Recent Practices

List of all practices with descriptions
Practice name and description displayed
Visual indicators with Building2 icon
System Activity

Real-time activity feed
Recent actions: interviews scheduled, panel members added, designations created
Time-stamped events
Navigation Menu:
Dashboard (Home icon)
User Management (Users icon)
Practices (Building2 icon)
Designations (Briefcase icon)
Panel Members (UserCircle icon)
Feedback Templates (ClipboardList icon)
User Management Page
File: /components/pages/user-management.tsx

Features:
View All Users: Table with name, email, role, practice, and creation date
Add New User: Dialog form with fields:
Name (required)
Email (required)
Role (dropdown: Master Admin, Practice Admin, Panel Member, TA Team)
Practice (dropdown, required for non-Master Admin roles)
Edit User: Modify existing user details
Delete User: Remove users from the system
Role Badges: Color-coded by role type
Master Admin: Purple
Practice Admin: Blue
Panel Member: Green
TA Team: Orange
User Journey:
View paginated user list in table format
Click "Add User" to open creation dialog
Fill form with validation
Select role (affects practice field visibility)
Submit to create user
Edit/Delete via action buttons in table rows
Practice Management Page
File: /components/pages/practice-management.tsx

Features:
View Practices: Card-based layout showing all practices
Add Practice: Dialog form with:
Practice name (required)
Description (required)
Assign admins (multi-select from practice_admin users)
Edit Practice: Update details and admin assignments
Delete Practice: Remove practice from system
Practice Cards Display:
Practice name and description
List of assigned admins with names
Action buttons (Edit/Delete)
User Journey:
View all practices in card grid layout
Click "Add Practice" to open creation dialog
Enter practice details
Select one or more practice admins
Submit to create practice
Manage existing practices via card actions
Designation Management Page
File: /components/pages/designation-management.tsx

Features (Master Admin View):
View All Designations: Table showing title, practice, and creation date
Add Designation: Simple form with:
Title (required)
Practice (dropdown selection)
Edit Designation: Update title and practice association
Delete Designation: Remove designation
Practice Filter: View designations by practice
User Journey:
View system-wide designation list
Click "Add Designation" to create new
Enter title and select associated practice
Submit to create
Edit/Delete via table actions
Practice Admin Flow
Dashboard
File: /components/dashboard/practice-admin-dashboard.tsx

Statistics Overview (4 Cards):
Panel Members: Count of panel members in the practice
Available Slots: Number of open interview slots
Scheduled Interviews: Upcoming interviews count
Feedback Submitted: Total feedback entries
Dashboard Sections:
Upcoming Interviews

List of scheduled interviews
Shows interview level
Displays date and time from slot data
Calendar icon indicators
Panel Member Activity

Overview of all panel members
Shows available slot count per member
Quick status of panel availability
Navigation Menu:
Dashboard (Home icon)
Designations & JDs (Briefcase icon)
Panel Management (UserCircle icon) - Coming Soon
Slot Management (Calendar icon)
Feedback Templates (ClipboardList icon) - Coming Soon
Feedback Review (MessageSquare icon)
Designations & JD Management Page
File: /components/pages/designation-management.tsx

Practice Admin View Features:
Tabbed Interface:
Tab 1: Designations
Tab 2: Job Descriptions
Designations Tab:
View Designations: Filtered to practice only
Add Designation: Auto-associated with practice
Edit/Delete: Manage practice designations
Job Descriptions Tab:
View JDs: Table with title, designation, requirements preview
Add JD: Dialog form with:
Title (required)
Designation (dropdown from practice designations)
Description (textarea)
Requirements (dynamic list with add/remove)
Edit JD: Update existing job descriptions
Delete JD: Remove job descriptions
Requirements Management: Add multiple requirements dynamically
User Journey:
Switch between Designations and JD tabs
For Designations: Same as Master Admin but practice-scoped
For JDs:
Click "Add Job Description"
Fill title and description
Select associated designation
Add requirements one by one (with remove option)
Submit to create JD
Edit/Delete via table actions
Slot Management Page
File: /components/pages/slot-management.tsx

Practice Admin View Features:
View by Panel Member: Dropdown filter to see specific member's slots
View All Slots: Table showing all practice slots with:
Panel member name
Date and time range
Status (available/blocked/scheduled/unavailable)
Designation and level (if applicable)
Actions (Edit/Delete)
Status Color Coding:
Available: Green
Blocked: Red
Scheduled: Blue
Unavailable: Gray
User Journey:
View all panel member slots in table
Filter by specific panel member if needed
Review slot availability and status
Edit slot details as needed
Delete slots if necessary
Feedback Review Page
File: /components/pages/feedback-management.tsx

Practice Admin View Features:
View All Feedback: Table displaying:
Candidate name
Panel member name
Interview date
Overall rating
Decision (Cleared/Not Cleared/On Hold)
View details button
Feedback Details Dialog:
Overall rating display
Decision with color-coded badge
All section ratings with individual scores
Comments and observations
Read-only view for review
User Journey:
View feedback submissions table
Review overall ratings and decisions
Click "View Details" for specific feedback
Review detailed section-wise ratings
Read comments and observations
Close dialog to return to list
Panel Member Flow
Dashboard
File: /components/dashboard/panel-member-dashboard.tsx

Statistics Overview (4 Cards):
Available Slots: Personal available interview slots
Scheduled Interviews: Upcoming interviews assigned
Pending Feedback: Completed interviews without feedback
Feedback Submitted: Total feedback count
Dashboard Sections:
Upcoming Interviews

Scheduled interviews for this panel member
Shows candidate name (from profile)
Displays date and time
Interview level badge
Empty state if no interviews
This Week's Availability

List of slots for current week
Date and time range
Status badge (available/blocked/scheduled)
Limited to 5 most recent slots
Navigation Menu:
Dashboard (Home icon)
My Availability (Calendar icon)
My Interviews (FileText icon) - Coming Soon
Feedback (MessageSquare icon)
My Availability (Slot Management) Page
File: /components/pages/slot-management.tsx

Panel Member View Features:
Personal Slot Calendar: Only shows logged-in panel member's slots
Add Availability: Dialog form with:
Date picker (calendar component)
Start time (required)
End time (required)
Status (dropdown: available/blocked/unavailable)
Reason (for blocked/unavailable slots)
Bulk Actions: Add multiple slots at once
View Slots: Table with date, time, status, and actions
Edit Slot: Modify existing slot details
Delete Slot: Remove availability slot
User Journey:
View personal availability calendar/table
Click "Add Availability" to create new slot
Select date from calendar picker
Enter start and end times
Choose status (default: available)
Add reason if blocking time
Submit to create slot
Edit/Delete existing slots as needed
Feedback Submission Page
File: /components/pages/feedback-management.tsx

Panel Member View Features:
My Interviews Tab: List of assigned interviews

Candidate name and interview details
Interview date and level
Status indicator
"Submit Feedback" button for completed interviews
"View Feedback" for already submitted
Feedback Submission Dialog:

Overall rating (1-5 stars)
Decision dropdown (Cleared/Not Cleared/On Hold)
Multiple rating sections (loaded from template):
Technical Skills
Communication
Problem Solving
Cultural Fit
Each with 1-5 rating
Comments textarea (required)
Observations textarea (optional)
Submit validation
User Journey:
View list of assigned interviews
Identify completed interviews needing feedback
Click "Submit Feedback" button
Fill overall rating (required)
Select decision (required)
Rate each section individually
Write detailed comments
Add observations (optional)
Submit feedback
Success confirmation with toast notification
TA Team Flow
Dashboard
File: /components/dashboard/ta-team-dashboard.tsx

Statistics Overview (4 Cards):
Active Opportunities: Open job opportunities count
Candidate Profiles: Total candidates in system
Available Slots: Panel member slots available for scheduling
Scheduled Interviews: Total scheduled interviews
Dashboard Sections:
Recent Candidate Profiles

List of all candidate profiles
Shows name and associated opportunity title
Status badge (pending/scheduled/completed/rejected)
Color-coded status indicators
Upcoming Interviews

Scheduled interviews overview
Candidate name
Date and time
Interview level badge
Empty state if none scheduled
Active Opportunities

Open job opportunities list
Opportunity title
Candidate count per opportunity
Status badge
Navigation Menu:
Dashboard (Home icon)
Opportunities (Briefcase icon)
Candidate Profiles (Users icon)
Slot Management (Calendar icon)
Interview Scheduling (FileText icon)
Feedback Review (MessageSquare icon)
Opportunities Management Page
File: /components/pages/interview-scheduling.tsx (Tab 1)

Features:
View Opportunities: Table showing:
Opportunity title
Associated designation
Job description reference
Status (open/closed)
Candidate count
Actions
Add Opportunity: Dialog form with:
Title (required)
Practice (dropdown)
Designation (dropdown, filtered by practice)
Job Description (dropdown, filtered by designation)
Status (open by default)
Edit Opportunity: Update details
Close Opportunity: Mark as closed
Delete Opportunity: Remove from system
User Journey:
View all opportunities in table
Click "Add Opportunity" to create new
Enter title
Select practice (affects designation options)
Select designation (affects JD options)
Select associated job description
Submit to create opportunity
Manage via table actions
Candidate Profiles Management Page
File: /components/pages/interview-scheduling.tsx (Tab 2)

Features:
View Profiles: Table displaying:
Name, email, phone
Associated opportunity
Status (pending/scheduled/completed/rejected)
Actions
Add Profile: Dialog form with:
Name (required)
Email (required)
Phone (required)
Opportunity selection (dropdown)
Initial status (pending by default)
Edit Profile: Update candidate details
Delete Profile: Remove candidate
Status Management: Track candidate progress
User Journey:
View candidate profiles table
Click "Add Candidate" to create new profile
Enter candidate personal information
Select associated opportunity
Submit to create profile
Track status changes through interview process
Edit/Delete via table actions
Slot Management Page (TA Team View)
File: /components/pages/slot-management.tsx

TA Team View Features:
View All Available Slots: System-wide view of panel member availability
Filter by Panel Member: Dropdown to narrow results
Slot Details: Table showing:
Panel member name
Date and time range
Status
Designation and level (if applicable)
Read-only view
Availability Overview: Help schedule interviews based on slot availability
User Journey:
View all available interview slots
Filter by specific panel member if needed
Check availability for interview scheduling
Use information to schedule interviews in scheduling page
Interview Scheduling Page
File: /components/pages/interview-scheduling.tsx (Tab 3)

Features:
View Scheduled Interviews: Table showing:
Candidate name (from profile)
Opportunity title
Panel member assigned
Interview level
Scheduled date and time
Status
Actions (Reschedule/Cancel)
Schedule Interview: Dialog form with:
Candidate selection (dropdown from profiles)
Opportunity (auto-filled or selectable)
Available slots (dropdown, filtered by available status)
Interview level (L1, L2, L3, etc.)
Automatic slot status update on scheduling
Reschedule Interview: Change assigned slot
Cancel Interview: Mark as cancelled with reason
Status Tracking: scheduled/completed/cancelled/rescheduled
User Journey:
View all scheduled interviews in table
Click "Schedule Interview" to create new
Select candidate from dropdown
Choose opportunity (may auto-populate from candidate)
Select from available panel member slots
Choose interview level
Submit to schedule (slot status auto-updates)
Reschedule if needed with reason
Cancel with reason if necessary
Feedback Review Page (TA Team View)
File: /components/pages/feedback-management.tsx

TA Team View Features:
Same as Practice Admin - read-only review of all feedback: - View all submitted feedback - Review ratings and decisions - View detailed feedback in dialog - Track interview outcomes

User Journey:
Access feedback review page
View feedback table with all submissions
Review overall ratings and decisions
Click details for comprehensive view
Use data for candidate progress tracking
Common Components
Layout Component
File: /components/layout.tsx

Features:
Header:
Application branding
Current user name and role badge
User dropdown menu:
Profile settings (coming soon)
Logout
Sidebar Navigation:
Role-based menu items
Active page highlighting
Icon + text labels
Responsive design
Main Content Area:
Renders current page component
Consistent padding and layout
Navigation Behavior:
Click sidebar items to navigate
Active page highlighted with indigo background
Icon indicators for visual recognition
Smooth transitions between pages
Authentication Context
File: /lib/auth-context.tsx

Features:
User State Management: Centralized user session
Login Function: Validates credentials against mock data
Logout Function: Clears user session
Authentication Check: isAuthenticated boolean
User Object: Contains id, email, name, role, practiceId
Context Provider:
Wraps entire application
Accessible via useAuth() hook
Persists during session
Resets on logout
Toast Notifications
Component: Shadcn Sonner

Usage Across Pages:
Success messages on create/update/delete operations
Error messages for validation failures
Confirmation messages for important actions
Auto-dismiss after 3-5 seconds
User Role Access Matrix
Page/Feature	Master Admin	Practice Admin	Panel Member	TA Team
Dashboard	✅	✅	✅	✅
User Management	✅	❌	❌	❌
Practice Management	✅	❌	❌	❌
Designation Management	✅ (All)	✅ (Practice)	❌	❌
JD Management	❌	✅	❌	❌
Panel Management	✅ (Coming)	✅ (Coming)	❌	❌
Slot Management (View All)	❌	✅	❌	✅ (Read-only)
Slot Management (Personal)	❌	❌	✅	❌
Opportunities	❌	❌	❌	✅
Candidate Profiles	❌	❌	❌	✅
Interview Scheduling	❌	❌	❌	✅
Feedback Submission	❌	❌	✅	❌
Feedback Review	❌	✅	✅ (Own)	✅ (All)
Feedback Templates	✅ (Coming)	✅ (Coming)	❌	❌
My Interviews	❌	❌	✅ (Coming)	❌
Profile Settings	✅ (Coming)	✅ (Coming)	✅ (Coming)	✅ (Coming)
Data Flow Architecture
Current State: Mock Data
File: /lib/mock-data.ts

Data Entities:
Users: System users with roles
Practices: Organizational units
Designations: Job titles/levels
Job Descriptions: Detailed role requirements
Panel Members: Interview panel members with expertise
Interview Slots: Available time slots for interviews
Opportunities: Open positions
Profiles: Candidate information
Interviews: Scheduled interview sessions
Feedback: Interview evaluation data
Feedback Templates: Evaluation criteria templates
Relationships:
Users → Practices (many-to-one for Practice Admin)
Designations → Practices (many-to-one)
Job Descriptions → Designations (many-to-one)
Panel Members → Users, Practices (references)
Slots → Panel Members (many-to-one)
Opportunities → Designations, Practices, JDs (references)
Profiles → Opportunities (many-to-one)
Interviews → Profiles, Opportunities, Slots, Panel Members (references)
Feedback → Interviews, Panel Members (references)
Form Validation Rules
Common Patterns:
Required Fields: Marked with asterisk, validated on submit
Email Fields: Standard email format validation
Dropdown Selections: Required selections validated
Date Fields: Calendar picker with date validation
Time Fields: HH:MM format validation
Text Areas: Minimum length requirements for comments
Validation Feedback:
Inline error messages
Red border on invalid fields
Toast notifications for submit errors
Success confirmations on valid submission
Responsive Design
Breakpoints:
Mobile: < 768px (stacked layouts, simplified navigation)
Tablet: 768px - 1024px (2-column grids)
Desktop: > 1024px (full layout with sidebar)
Mobile Adaptations:
Collapsible sidebar navigation
Stacked stat cards
Responsive tables (horizontal scroll if needed)
Touch-friendly button sizes
Optimized dialog sizes
Future Enhancements (Coming Soon)
Pending Pages:
Panel Management: Add/edit panel members, assign designations and levels
Feedback Templates: Create custom evaluation templates
My Interviews: Panel member's interview schedule view
Profile Settings: User account management
Planned Features:
Email notifications for scheduled interviews
Calendar integrations
Interview feedback analytics
Candidate pipeline visualization
Advanced filtering and search
Export functionality (PDF reports)
Bulk operations for scheduling
Interview history tracking
Best Practices for Navigation
General Flow:
Start at Dashboard: Overview of relevant metrics
Setup Phase (Master/Practice Admin):
Create practices
Add users
Define designations and JDs
Create feedback templates
Preparation Phase (Panel Members):
Set availability via slot management
Recruitment Phase (TA Team):
Create opportunities
Add candidate profiles
Schedule interviews using available slots
Execution Phase (Panel Members):
View scheduled interviews
Conduct interviews
Submit feedback
Review Phase (Practice Admin/TA Team):
Review feedback
Make hiring decisions
Track candidate progress
Page State Management
Loading States:
Skeleton loaders for initial data fetch
Loading spinners for form submissions
Disabled buttons during processing
Empty States:
Informative messages when no data exists
Call-to-action buttons to create first item
Visual indicators for empty tables/lists
Error States:
Error boundaries for component failures
Retry mechanisms for failed operations
Clear error messages for users
Keyboard Shortcuts (Future Enhancement)
Planned shortcuts for power users: - Ctrl/Cmd + K: Quick search - Ctrl/Cmd + N: Create new item - Esc: Close dialogs/modals - Arrow keys: Navigate tables - Enter: Confirm actions

Accessibility Features
Current Implementation:
Semantic HTML structure
ARIA labels on interactive elements
Keyboard navigation support
Focus indicators on interactive elements
Color contrast compliance (WCAG AA)
Screen reader friendly labels
Form Accessibility:
Label associations with inputs
Error announcements
Required field indicators
Focus management in dialogs
Color Coding System
Role Badges:
Master Admin: Purple (bg-purple-100, text-purple-800)
Practice Admin: Blue (bg-blue-100, text-blue-800)
Panel Member: Green (bg-green-100, text-green-800)
TA Team: Orange (bg-orange-100, text-orange-800)
Status Indicators:
Available: Green
Scheduled: Blue
Completed: Green
Blocked: Red
Unavailable: Gray
Pending: Yellow
Rejected: Red
Cancelled: Gray
On Hold: Yellow
Decision Badges:
Cleared: Green
Not Cleared: Red
On Hold: Yellow
Summary
This Interview Management Platform provides a comprehensive solution for managing the end-to-end interview process across multiple practices. Each role has carefully designed workflows that support their specific responsibilities while maintaining data consistency and process integrity across the organization.

The current implementation uses mock data and is ready for Supabase integration to enable persistent data storage, real-time updates, and multi-user collaboration capabilities.