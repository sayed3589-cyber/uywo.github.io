# 🔒 Club Ledger - Secure Member Management System

## Overview
A secure web application for managing club member contributions and expenses for charity and social work activities. This system now includes comprehensive security features to protect your club's financial data.

---

## 🚀 NEW SECURITY FEATURES

### ✅ Authentication & Access Control
- **Login System**: Only authorized members can access the application
- **Session Management**: Automatic logout after 60 minutes of inactivity
- **User Tracking**: All actions are logged with user information
- **Demo Account**: 
  - Username: `admin`
  - Password: `secure123`

### ✅ Data Protection
- **Input Validation**: All user inputs are validated before storage
- **XSS Prevention**: All user-generated content is sanitized to prevent script injection
- **Encrypted Storage**: Sensitive data is encoded before storing in browser
- **Audit Logs**: Complete activity trail for compliance and security

### ✅ Data Integrity
- **Checksum Verification**: Data integrity checks ensure information hasn't been tampered with
- **User Attribution**: Every entry is tagged with who created/modified it
- **Timestamps**: All actions are recorded with exact timestamps

---

## 📁 File Structure

```
uywo.github.io/
├── login.html              # Secure login page
├── index.html              # Dashboard (now with authentication)
├── contribution.html       # Member contributions (secured)
├── expense.html            # Expense tracking (secured)
├── members.html            # Member list
├── reports.html            # Financial reports
├── security.js             # Security module (authentication & encryption)
└── README.md              # This file
```

---

## 🔐 Security Architecture

### 1. Authentication Layer (`login.html`)
- Username and password validation
- Session token generation
- Login attempt logging
- Credential verification against authorized users

### 2. Security Module (`security.js`)

#### Functions Available:

**Authentication:**
- `validateCredentials(username, password)` - Verify user credentials
- `isUserLoggedIn()` - Check if session is valid
- `getCurrentUser()` - Get logged-in username
- `enforceLogin()` - Redirect to login if not authenticated
- `logout()` - Safely logout user

**Data Protection:**
- `sanitizeInput(input)` - Remove XSS vectors from text
- `sanitizeHTML(html)` - Safe HTML rendering
- `validateNumber(value)` - Validate numeric inputs
- `validateDate(date)` - Validate date format (YYYY-MM-DD)

**Encryption:**
- `encryptData(data)` - Encode data for storage
- `decryptData(encrypted)` - Decode stored data
- `storeSecureData(key, data)` - Store encrypted data with metadata
- `getSecureData(key)` - Retrieve and decrypt data

**Validation:**
- `validateContribution(data)` - Validate contribution entries
- `validateExpense(data)` - Validate expense entries

**Audit Trail:**
- `logAccess(user, action, status)` - Log user activities
- `getAuditLogs(limit)` - Retrieve audit logs

---

## 🛡️ How It Works

### Login Flow
1. User visits the application and is redirected to `login.html`
2. User enters username and password
3. Credentials are validated against the authorized users database
4. On success, a session token is generated
5. User is redirected to the dashboard (`index.html`)
6. Session is stored in `sessionStorage` (cleared when browser closes)

### Data Security Flow
1. User enters data (contribution or expense)
2. Input is validated using `validateContribution()` or `validateExpense()`
3. Any XSS threats are removed using `sanitizeInput()`
4. Data is encrypted using `encryptData()`
5. Encrypted data is stored with metadata (timestamp, user, version)
6. All actions are logged to audit trail

### Session Management
- Sessions expire after 60 minutes of inactivity
- User activity (mouse movement, keyboard input) extends session
- Session is cleared when browser window closes
- Attempting to access without valid session redirects to login

---

## 👥 Authorized Users

You can add/modify authorized users by editing the `AUTHORIZED_USERS` object in `security.js`:

```javascript
const AUTHORIZED_USERS = {
    'admin': 'secure123',           // Default admin
    'treasurer': 'money2024',       // Treasury member
    'secretary': 'records2024'      // Records keeper
    // Add more users as needed
};
```

**Important**: Change these default passwords immediately!

---

## 📊 Features

### Dashboard (`index.html`)
- Display current club balance
- Quick access to all modules
- User identification
- Secure logout option

### Contributions (`contribution.html`)
- Record member contributions
- Date tracking
- Description/notes field
- View all contributions sorted by date
- Delete contributions (with confirmation)
- Secure data storage

### Expenses (`expense.html`)
- Log club expenses
- Categorize expenses (Food, Charity, Events, etc.)
- Track who paid for expenses
- Add descriptions
- View expense history
- Delete records with audit trail

### Members (`members.html`)
- View all club members
- Member contribution summary
- Member details and contact information

### Reports (`reports.html`)
- Financial summary
- Monthly contribution trends
- Expense breakdown by category
- Member-wise contribution reports
- Balance sheet

---

## 🔑 Session Timeout Configuration

Default session timeout is **60 minutes**. To change it, edit `security.js`:

```javascript
const SESSION_TIMEOUT = 60; // Change to desired minutes
```

---

## 📝 Audit Logs

All user activities are logged. Access logs using browser console:

```javascript
// In browser console:
getAuditLogs(100) // Get last 100 log entries
```

Logs include:
- Timestamp
- Username
- Action performed
- Status (Success/Failed)
- Additional details

---

## ⚠️ Important Security Notes

### For Production Use:
1. **Move credentials to server**: Don't store passwords in client-side code
2. **Use HTTPS**: Always deploy with SSL/TLS encryption
3. **Implement server-side validation**: Never rely only on client-side checks
4. **Use proper encryption**: Replace Base64 with AES-256 or similar
5. **Set up database**: Replace localStorage with secure database
6. **Enable CORS**: Configure proper cross-origin policies
7. **Add rate limiting**: Prevent brute force attacks

### Best Practices:
- ✅ Change default passwords immediately
- ✅ Use strong, unique passwords (mix upper, lower, numbers, symbols)
- ✅ Don't share credentials
- ✅ Log out when done
- ✅ Don't use public WiFi for sensitive operations
- ✅ Clear browser cache periodically
- ✅ Review audit logs regularly

---

## 🚨 Troubleshooting

### Issue: "Invalid username or password"
- Verify username and password are correct
- Check if user exists in `AUTHORIZED_USERS`
- Ensure there are no extra spaces in input

### Issue: Session expires quickly
- Increase `SESSION_TIMEOUT` value in `security.js`
- This is set to 60 minutes by default
- Move mouse or press keys to keep session active

### Issue: Data not saving
- Check browser console for errors (F12 → Console)
- Verify localStorage is enabled in browser
- Ensure you're logged in with valid session

### Issue: Redirected to login unexpectedly
- Your session may have expired (60 minutes of inactivity)
- Browser may have been closed/refreshed
- Log back in to continue

---

## 🔄 Updates & Maintenance

### Adding New Features:
1. Always add security checks with `enforceLogin()`
2. Use `sanitizeInput()` for all user inputs
3. Use `getSecureData()` and `storeSecureData()` for data handling
4. Log important actions with `logAccess()`
5. Validate inputs with appropriate validation functions

### Regular Maintenance:
- Review audit logs monthly
- Update authorized users list as members change
- Test backup and recovery procedures
- Update encryption method to stronger algorithms
- Monitor for suspicious activities

---

## 📞 Support

For issues or security concerns:
1. Check the **Troubleshooting** section above
2. Review browser console for error messages
3. Check audit logs for unusual activities
4. Contact the system administrator

---

## 📄 Version History

**v2.0 - Secure Edition (Current)**
- Added authentication system
- Implemented session management
- Added input validation and XSS prevention
- Implemented data encryption
- Added audit logging system
- Enhanced user experience with security feedback

**v1.0 - Initial Release**
- Basic contribution tracking
- Expense management
- Member management
- Reports generation

---

## ⚖️ License & Compliance

This system is designed for club management and charitable work. All member data should be treated as confidential. Ensure compliance with:
- Data protection regulations
- Privacy laws in your jurisdiction
- Club bylaws and policies
- Tax and financial reporting requirements

---

## 🎯 Future Enhancements

Planned security improvements:
- [ ] Multi-factor authentication (2FA)
- [ ] Role-based access control (RBAC)
- [ ] Export data with encryption
- [ ] Backup and restore functionality
- [ ] Real-time activity notifications
- [ ] IP-based access restrictions
- [ ] API-based architecture
- [ ] Mobile app

---

**Last Updated**: June 17, 2026

**⚠️ Remember**: Security is an ongoing process. Keep your system updated and review security practices regularly!
