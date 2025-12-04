# User Stories: Login Screen

## Module: Authentication
**Reference:** Figma_All_Screens.md - Section 1 (Login Screen)

---

## US-001.1: User Login with Valid Credentials
**As a** system user (Master Admin, Practice Admin, TA Team Admin, or Tech Panel Member)  
**I want to** log in to the Interview Management Platform using my email and password  
**So that** I can access the system features based on my assigned role

### Acceptance Criteria:
- [ ] Login form displays email and password input fields
- [ ] Email field validates proper email format
- [ ] Password field masks entered characters
- [ ] "Login" button is enabled when both fields are filled
- [ ] On successful authentication, user is redirected to role-based dashboard
- [ ] System validates credentials against Active Directory
- [ ] User session is established upon successful login
- [ ] Appropriate welcome message is displayed after login

### UI Elements:
- Logo placement at top center
- Email input field (required, email validation)
- Password input field (required, masked)
- Login button (primary action)
- Error message display area (initially hidden)

### Business Rules:
- Email must be in valid format
- Password must meet complexity requirements (min 8 characters with alphabets, numbers, and special characters)
- User must exist in the system and be active

---

## US-001.2: Display Error Messages for Invalid Login
**As a** system user  
**I want to** see clear error messages when login fails  
**So that** I know what went wrong and can take corrective action

### Acceptance Criteria:
- [ ] Display "Invalid credentials" message for incorrect email/password
- [ ] Display "Account inactive" message for deactivated users
- [ ] Display "Email required" validation message if email field is empty
- [ ] Display "Password required" validation message if password field is empty
- [ ] Display "Invalid email format" for improperly formatted email
- [ ] Error messages appear below the relevant field or in a dedicated error area
- [ ] Error messages are displayed in red color for visibility
- [ ] Previous error messages are cleared when user starts typing

### UI Elements:
- Error message container
- Field-level validation indicators
- General error message area below login button

### Business Rules:
- Maximum 3 login attempts before temporary lockout (if implemented)
- Error messages should not reveal whether email or password is incorrect (security)
- Clear error messages without exposing sensitive information

---

## US-001.3: Password Visibility Toggle
**As a** system user  
**I want to** toggle password visibility  
**So that** I can verify what I've typed before submitting

### Acceptance Criteria:
- [ ] Eye icon displayed at the end of password field only when password has been entered
- [ ] Icon is hidden when password field is empty
- [ ] Clicking eye icon toggles password visibility between masked and visible
- [ ] Icon changes to indicate current state (eye-open for show, eye-closed for hide)
- [ ] Password remains masked by default
- [ ] Toggle state resets after form submission
- [ ] Icon does not overlap with password text
- [ ] Only one eye icon is displayed at a time

### UI Elements:
- Eye icon button positioned inside password field on the right (conditional display)
- Visual indicator for show/hide state (eye-open/eye-closed icons)
- Proper spacing to prevent overlapping with input text

### Business Rules:
- Eye icon appears only when password field contains text
- Icon disappears when password field is cleared
- Default state is password masked (eye-closed icon when visible)

---

## US-001.4: Remember Me Functionality (Optional)
**As a** frequent system user  
**I want to** have the option to stay logged in  
**So that** I don't need to re-enter credentials every time

### Acceptance Criteria:
- [ ] "Remember Me" checkbox displayed below password field
- [ ] If checked, user session persists for specified duration
- [ ] User can log out manually at any time
- [ ] Session expires after configured inactivity period

### UI Elements:
- Remember Me checkbox (optional)

---

## US-001.5: Forgot Password Link (Optional)
**As a** system user who forgot my password  
**I want to** have access to a password reset option  
**So that** I can regain access to my account

### Acceptance Criteria:
- [ ] "Forgot Password?" link displayed below login form
- [ ] Clicking link navigates to password reset flow
- [ ] User receives password reset instructions via email

### UI Elements:
- Forgot Password link

---

## Technical Notes:
- Integrate with Active Directory for authentication
- Implement JWT token-based session management
- Log all login attempts (successful and failed) for security audit
- Implement CSRF protection
- Use HTTPS for all authentication requests

## Related Functional Requirements:
- FR#AUTH-1: User Authentication
- FR#AUTH-2: Session Management

## Priority: P0 (Critical)
## Estimated Story Points: 5
