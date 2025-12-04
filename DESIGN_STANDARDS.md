# UI Design Standards & Guidelines

## Purpose
This document defines the common design standards and patterns to ensure consistent look and feel across all screens in the Interview Management Platform.

---

## Technology Stack

### Core Technologies
- **React:** Fluent Base framework for UI components
- **React Hook Form:** Form handling and validation
- **Zod:** Validation schema definitions
- **Zustand:** State management across the application
- **Axios:** HTTP client for API calls

### Design Implementation
- All design components should be built as reusable React components
- Forms should utilize React Hook Form with Zod validation schemas
- Global state (user session, notifications) should use Zustand
- API integration should use Axios with proper error handling
- Component styling should follow Material Design principles

---

## 1. Layout Standards

### Page Structure
- **Header:** Fixed top header with logo, user profile, and logout
- **Navigation:** Left sidebar (collapsible) with menu items
- **Content Area:** Main content with breadcrumbs, page title, and content sections
- **Footer:** Optional footer for copyright/version info

### Spacing
- Page padding: 24px
- Section spacing: 16px between sections
- Element spacing: 8px between related elements
- Card padding: 16px internal padding

---

## 2. Typography Standards

### Hierarchy
- **Page Title:** 24px, Bold, Primary color
- **Section Title:** 20px, Semi-bold, Dark gray
- **Card Title:** 16px, Semi-bold, Dark gray
- **Body Text:** 14px, Regular, Dark gray
- **Helper Text:** 12px, Regular, Medium gray
- **Error Text:** 12px, Regular, Red

---

## 3. Color Standards

### Primary Colors
- **Primary:** Blue (#1976D2)
- **Secondary:** Gray (#757575)
- **Success:** Green (#388E3C)
- **Warning:** Orange (#F57C00)
- **Error:** Red (#D32F2F)
- **Info:** Light Blue (#0288D1)

### Status Colors
- **Active/Available:** Green (#4CAF50)
- **Inactive/Unavailable:** Gray (#9E9E9E)
- **Pending:** Yellow/Orange (#FF9800)
- **Scheduled:** Blue (#2196F3)
- **Completed:** Green (#4CAF50)
- **Cancelled/Rejected:** Red (#F44336)

### Background Colors
- **Page Background:** Light gray (#F5F5F5)
- **Card Background:** White (#FFFFFF)
- **Hover State:** Light gray (#EEEEEE)
- **Selected State:** Light blue (#E3F2FD)

---

## 4. Component Standards

### Buttons
**Primary Button:**
- Background: Primary color
- Text: White
- Padding: 10px 24px
- Border-radius: 4px
- Font-weight: Semi-bold
- Use for: Main actions (Save, Create, Submit)

**Secondary Button:**
- Background: White
- Text: Primary color
- Border: 1px solid Primary color
- Padding: 10px 24px
- Border-radius: 4px
- Use for: Cancel, Back actions

**Tertiary/Text Button:**
- Background: Transparent
- Text: Primary color
- No border
- Use for: Less important actions

**Button States:**
- Hover: Darken by 10%
- Disabled: 50% opacity, cursor not-allowed
- Loading: Show spinner, disable interaction

### Form Elements

**Text Input:**
- Height: 40px
- Border: 1px solid #CCCCCC
- Border-radius: 4px
- Padding: 8px 12px
- Font-size: 14px
- Focus: Border color changes to Primary

**Dropdown:**
- Height: 40px
- Border: 1px solid #CCCCCC
- Border-radius: 4px
- Padding: 8px 12px
- Chevron icon on right
- Font-size: 14px

**Checkbox/Radio:**
- Size: 20px x 20px
- Border: 2px solid #CCCCCC
- Checked: Primary color fill
- Label: 14px, 8px spacing from control

**Date Picker:**
- Input: Same as text input
- Calendar popup with month/year navigation
- Today button highlighted
- Selected date in Primary color

**Time Picker:**
- Input: Same as text input
- Dropdown with 15-minute intervals
- Format: HH:MM AM/PM

**File Upload:**
- Drag-and-drop area with dashed border
- Browse button (secondary style)
- File size and type restrictions shown
- Progress bar during upload
- Preview of uploaded file

### Tables

**Standard Table:**
- Header: Background #F5F5F5, bold text
- Borders: 1px solid #E0E0E0
- Row height: 48px
- Row hover: Background #FAFAFA
- Alternating rows: Optional, light gray
- Pagination: Bottom, showing "Page X of Y", page size selector

**Sortable Columns:**
- Arrow icon next to header text
- Up arrow: Ascending sort
- Down arrow: Descending sort
- Gray when not active, Primary when active

**Action Column:**
- Three-dot menu icon (kebab menu)
- Opens dropdown with actions
- Actions: View, Edit, Delete, etc.

### Cards

**Standard Card:**
- Background: White
- Border: 1px solid #E0E0E0 (optional)
- Border-radius: 8px
- Padding: 16px
- Box-shadow: 0 2px 4px rgba(0,0,0,0.1) (optional)

**Card Header:**
- Title: 16px, semi-bold
- Subtitle: 14px, gray (optional)
- Action buttons/icons on right

**Card Content:**
- Body text: 14px
- Spacing: 12px between elements

### Modals

**Standard Modal:**
- Overlay: Dark background, 50% opacity
- Modal: White background, centered
- Width: 500px (small), 800px (medium), 1200px (large)
- Border-radius: 8px
- Box-shadow: 0 4px 12px rgba(0,0,0,0.15)

**Modal Structure:**
- **Header:** Title (20px, semi-bold), close icon (X)
- **Content:** Scrollable if needed, 24px padding
- **Footer:** Action buttons (right-aligned), consistent spacing

### Status Badges

**Standard Badge:**
- Border-radius: 12px
- Padding: 4px 12px
- Font-size: 12px
- Font-weight: Semi-bold
- Text: Uppercase

**Status Colors:**
- Active: Green background, dark green text
- Inactive: Gray background, dark gray text
- Pending: Orange background, dark orange text
- Scheduled: Blue background, dark blue text
- Completed: Green background, dark green text
- Cancelled: Red background, dark red text

### Toast Notifications

**Standard Toast:**
- Position: Top-right corner
- Width: 350px
- Border-radius: 4px
- Padding: 16px
- Auto-dismiss: 5 seconds
- Close button (X) on right

**Types:**
- **Success:** Green background, white text, checkmark icon
- **Error:** Red background, white text, error icon
- **Warning:** Orange background, white text, warning icon
- **Info:** Blue background, white text, info icon

### Icons

**Standard:**
- Size: 20px x 20px (small), 24px x 24px (medium)
- Color: Inherit from parent or themed
- Line-weight: 2px
- Style: Outlined (Material Icons or similar)

**Common Icons:**
- Add: Plus sign
- Edit: Pencil
- Delete: Trash can
- View: Eye
- Search: Magnifying glass
- Filter: Funnel
- Sort: Arrows up/down
- Download: Down arrow
- Upload: Up arrow
- Close: X
- Back: Left arrow
- Calendar: Calendar grid
- Time: Clock

### Search & Filter Bar

**Standard Search:**
- Input with search icon on left
- Clear button (X) on right when text entered
- Placeholder text: "Search by..."
- Debounced: 300ms delay

**Filter Controls:**
- Dropdowns for categorical filters
- Date range pickers for date filters
- Number inputs for numeric ranges
- "Clear Filters" button to reset all

**Layout:**
- Horizontal layout: Search on left, filters on right
- "Show X results" count displayed
- Consistent spacing: 12px between controls

### Pagination

**Standard Pagination:**
- Position: Bottom of table/list
- Components: First, Previous, [Page Numbers], Next, Last
- Current page: Primary color, bold
- Other pages: Gray, clickable
- Disabled state: Gray, not clickable
- Page size selector: Dropdown (10, 20, 50, 100)
- Total count: "Showing X-Y of Z"

### Empty States

**Standard Empty State:**
- Centered illustration/icon (optional)
- Message: "No [items] found"
- Helper text: Suggest action (e.g., "Add your first...")
- Action button: Primary action (e.g., "Add [Item]")

### Loading States

**Spinner:**
- Centered on page/modal
- Size: 40px x 40px
- Color: Primary
- Animation: Rotating

**Skeleton Loader:**
- Gray placeholder matching content structure
- Animated shimmer effect
- Use for tables and cards

---

## 5. Interaction Standards

### Hover States
- Buttons: Darken by 10%
- Table rows: Light gray background
- Cards: Subtle shadow increase
- Links: Underline

### Active States
- Buttons: Darken by 15%
- Tabs: Border bottom or background change
- Menu items: Primary color text and background

### Disabled States
- Opacity: 50%
- Cursor: not-allowed
- No hover effects

### Focus States
- Outline: 2px solid Primary color
- Offset: 2px
- Apply to all focusable elements

---

## 6. Responsive Design

### Breakpoints
- **Mobile:** < 768px
- **Tablet:** 768px - 1024px
- **Desktop:** > 1024px

### Mobile Adaptations
- Navigation: Hamburger menu (collapsible)
- Tables: Horizontal scroll or card view
- Modals: Full-screen on mobile
- Form: Single column layout
- Buttons: Full-width on mobile

---

## 7. Accessibility Standards

### WCAG 2.1 Level AA Compliance
- Color contrast ratio: 4.5:1 for normal text
- Keyboard navigation: All interactive elements
- ARIA labels: For screen readers
- Focus indicators: Visible on all focusable elements
- Alt text: For all images

---

## 8. Animation Standards

### Transitions
- Duration: 200ms (fast), 300ms (normal), 500ms (slow)
- Easing: ease-in-out
- Use for: Hover, active, modal open/close

### Micro-interactions
- Button click: Scale down slightly (98%)
- Card hover: Lift (shadow increase)
- Loading: Spinner rotation
- Toast: Slide-in from top-right

---

## 9. Common Patterns

### CRUD Operations
1. **List View:**
   - Table or card grid
   - Search and filter bar
   - Add button (top-right)
   - Action menu for each item

2. **Create/Edit Form:**
   - Modal or dedicated page
   - Form validation (inline errors)
   - Primary button: Save/Create
   - Secondary button: Cancel
   - Success toast on completion

3. **Detail View:**
   - Read-only display of all fields
   - Edit and Delete buttons (if permitted)
   - Back/Close button

4. **Delete Confirmation:**
   - Modal with warning message
   - List dependencies (if any)
   - Confirm and Cancel buttons
   - Success toast on completion

### Error Handling
- **Field-level errors:** Red text below field
- **Form-level errors:** Red banner at top of form
- **Page-level errors:** Toast notification or error page
- **Network errors:** Retry button with message

---

## 10. Consistency Checklist

For each screen, ensure:
- [ ] Page title and breadcrumbs present
- [ ] Search and filter controls consistent
- [ ] Table columns sortable with standard icons
- [ ] Action menus use three-dot icon
- [ ] Status badges use standard colors
- [ ] Buttons follow primary/secondary pattern
- [ ] Modals have close button (X)
- [ ] Forms have inline validation
- [ ] Empty states have illustration and action
- [ ] Loading states use spinner or skeleton
- [ ] Success/error toasts displayed
- [ ] Pagination shows total count
- [ ] Responsive behavior defined

---

## Implementation Notes

- Use a UI component library (e.g., Material-UI, Ant Design, Chakra UI) for consistency
- Define design tokens for colors, spacing, typography
- Create reusable components for common patterns
- Conduct design reviews to ensure adherence to standards
- Update standards document as patterns evolve

---

**Last Updated:** December 3, 2025
**Version:** 1.0
