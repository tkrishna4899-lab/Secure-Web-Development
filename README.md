# Secure Task Manager

A modern, secure web application for managing tasks with advanced security features including two-factor authentication (2FA), role-based access control, and comprehensive audit logging.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Flask](https://img.shields.io/badge/Flask-3.0%2B-lightblue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)

---

## Features

### Security
- **Password Hashing**: Industry-standard bcrypt/PBKDF2 encryption
- **Two-Factor Authentication (2FA)**: TOTP (Time-based One-Time Password) support
- **CSRF Protection**: Flask-WTF built-in CSRF token validation
- **Secure Sessions**: HTTPOnly, SameSite cookies with automatic expiration
- **Role-Based Access Control**: Admin and User roles with authorization checks
- **Login Attempt Logging**: Track failed login attempts with IP addresses
- **Audit Trail**: Comprehensive logging of user actions

### Task Management
- Create, read, update, and delete tasks
- Task ownership enforcement
- Admin can view and manage all user tasks
- Task creation and modification timestamps
- Rich task descriptions with markdown support

###  User Management (Admin)
- View all registered users
- User statistics dashboard (total users, admins, 2FA enabled)
- User detail page with security status
- 2FA status monitoring
- Account health indicators

### User Experience
- Modern, responsive design with Bootstrap 5
- Glass-morphism effects and smooth animations
- Real-time form validation with password strength meter
- Mobile-friendly interface
- Beautiful error pages
- Flash messages with auto-close functionality
- Quick action buttons and shortcuts

### Dashboard
- Welcome message with user statistics
- Task overview cards
- 2FA status indicator
- Account security status
- Member since information

---

## Quick Start

### Prerequisites
- Python 3.8+
- pip or uv package manager
- SQLite3 (included with Python)

### Installation

1. **Clone the repository**
```bash
cd secure_task_manager
```

2. **Create and activate virtual environment** (if not using uv)
```bash
source .venv/bin/activate  # On Windows: .venv\Scripts\activate.ps1
```

3. **Install dependencies**
```bash
uv sync
```

4. **Run the application**
```bash
uv run run.py

```

5. **Access the application**
Open your browser and navigate to: **http://127.0.0.1:5000**

---

##  Default Admin Account

After starting the application for the first time, create the default admin user:

```bash
uv run create_admin.py
```

This will create an admin account with the following credentials:
- **Username**: `admin`
- **Password**: `Admin@123456`

### IMPORTANT SECURITY NOTES:
1. **Change the default password immediately** after first login
2. Enable 2FA for the admin account
3. Never share the admin credentials
4. Use a strong, unique password (8+ characters, mix of upper/lowercase, numbers, special characters)

---

##  User Guide

### Registration
1. Click "Sign Up" on the homepage
2. Choose a unique username (3-80 characters)
3. Enter a valid email address
4. Create a strong password (8+ characters)
5. Confirm your password
6. Accept the Terms of Service
7. Click "Register"

### Login
1. Enter your username
2. Enter your password
3. If 2FA is enabled, enter your 6-digit authentication code
4. Check "Remember Me" to stay logged in (optional)
5. Click "Login"

### Setting Up 2FA
1. Log in to your account
2. Click your username → "2FA Settings"
3. Scan the QR code with an authenticator app (Google Authenticator, Microsoft Authenticator, Authy, etc.)
4. Or manually enter the secret key
5. Enter the 6-digit code from your authenticator
6. Click "Verify and Enable 2FA"
7. 2FA is now enabled!

### Creating Tasks
1. Go to Dashboard → "Tasks" or click "My Tasks"
2. Click "Add New Task"
3. Enter task title (max 200 characters)
4. Enter task description (max 2000 characters, optional)
5. Click "Save Task"

### Managing Tasks
- **View**: Click on any task to see full details
- **Edit**: Click the "Edit" button to modify task details
- **Delete**: Click "Delete" button (confirmation required)
- **List**: View all your tasks in the Tasks page

### Admin Features
1. Click "Manage Users" (admin only)
2. View user statistics:
   - Total users
   - Admin users
   - Regular users
   - Users with 2FA enabled
3. View user list with roles and 2FA status
4. Click "View" to see user details
5. Monitor user account health and security status

---

## Project Structure

```
secure_task_manager/
├── app/
│   ├── static/
│   │   ├── css/
│   │   │   └── styles.css          # Custom CSS with animations
│   │   └── js/
│   │       └── main.js              # Form validation & UX enhancements
│   ├── templates/
│   │   ├── errors/
│   │   │   ├── 404.html            # Page not found
│   │   │   ├── 403.html            # Access denied
│   │   │   └── 500.html            # Server error
│   │   ├── admin/
│   │   │   ├── manage_users.html    # User management dashboard
│   │   │   └── user_detail.html     # Detailed user view
│   │   ├── tasks/
│   │   │   ├── list_tasks.html      # Task list
│   │   │   ├── add_task.html        # Create task
│   │   │   ├── view_task.html       # Task details
│   │   │   └── edit_task.html       # Edit task
│   │   ├── layout.html              # Base template
│   │   ├── index.html               # Homepage
│   │   ├── login.html               # Login page
│   │   ├── register.html            # Registration page
│   │   ├── dashboard.html           # User dashboard
│   │   ├── enable_2fa.html          # 2FA setup
│   │   └── verify_2fa.html          # 2FA verification
│   ├── __init__.py                  # Flask app factory
│   ├── config.py                    # Configuration settings
│   ├── models.py                    # Database models
│   ├── routes.py                    # Application routes
│   ├── forms.py                     # WTF form definitions
│   └── utils/
│       ├── security.py              # Security utilities
│       └── twofa.py                 # 2FA utilities
├── create_admin.py                  # Admin user creation script
├── run.py                           # Application entry point
├── main.py                          # Alternative entry point
├── requirements.txt                 # Python dependencies
└── README.md                        # This file
```

---

## Configuration

### Environment Variables
Create a `.env` file or set these in your environment:

```bash
FLASK_ENV=production
SECRET_KEY=your-super-secret-key-change-this
DATABASE_URL=sqlite:///instance/tasks.db
```

### Security Settings (app/config.py)
The application includes production-ready security settings:
- Session timeout: 7 days
- Cookie security: HTTPOnly, SameSite=Lax
- CSRF protection: Enabled
- Password requirements: Minimum 8 characters
- Login attempt logging: Enabled

---

## Technical Stack

### Backend
- **Flask**: Web framework
- **SQLAlchemy**: ORM for database operations
- **Flask-Login**: User session management
- **Flask-WTF**: Form handling and CSRF protection
- **PyOTP**: TOTP 2FA implementation
- **Werkzeug**: Password hashing and security utilities

### Frontend
- **Bootstrap 5.3.2**: Responsive UI framework
- **Font Awesome 6.4.0**: Icon library
- **Custom CSS**: Glass-morphism effects and animations
- **Vanilla JavaScript**: Form validation and UX enhancements

### Database
- **SQLite** (Development & Testing)
- Can be switched to PostgreSQL for production

---

##  Security Best Practices

### For Administrators
1. **Change Default Password**: Immediately after setup
2. **Enable 2FA**: Use a secure authenticator app
3. **Backup Database**: Regularly backup `instance/tasks.db`
4. **Monitor Logs**: Check application logs for suspicious activity
5. **Update Dependencies**: Keep Flask and dependencies updated
6. **Use HTTPS**: In production, always use HTTPS (SSL/TLS)
7. **Strong SECRET_KEY**: Generate a cryptographically secure key
8. **Database Security**: Use a strong database connection string in production

### For Users
1. **Strong Passwords**: Use 12+ characters with mixed case, numbers, symbols
2. **Enable 2FA**: Protect your account with two-factor authentication
3. **Authenticator App**: Use a trusted authenticator app (not SMS if possible)
4. **Backup Codes**: Save your authenticator recovery codes securely
5. **Don't Share**: Never share your credentials or recovery codes
6. **Logout**: Always logout from shared computers

---

##  Testing

### Manual Testing Checklist
- [ ] User registration with validation
- [ ] Login with valid credentials
- [ ] 2FA setup and verification
- [ ] Creating, editing, and deleting tasks
- [ ] Admin user management
- [ ] Logout functionality
- [ ] Error handling and flash messages
- [ ] Responsive design (mobile, tablet, desktop)
- [ ] Form validation and error messages

### Running Tests
```bash
# Future: Unit tests
python -m pytest tests/

# Future: Integration tests
python -m pytest tests/integration/
```

---

##  Deployment

### Development
```bash
uv run run.py
```

### Production (using Gunicorn)
```bash
# Install Gunicorn
uv pip install gunicorn

# Run with Gunicorn
gunicorn -w 4 -b 0.0.0.0:5000 run:app
```

### Production Checklist
- [ ] Set `FLASK_ENV=production`
- [ ] Generate a strong `SECRET_KEY`
- [ ] Use PostgreSQL or production database
- [ ] Set up HTTPS/SSL certificates
- [ ] Configure proper logging
- [ ] Enable database backups
- [ ] Set up monitoring and alerts
- [ ] Use a production WSGI server (Gunicorn, uWSGI)
- [ ] Configure firewall rules
- [ ] Use a reverse proxy (Nginx, Apache)

---

##  Troubleshooting

### Issue: CSRF Token Missing
**Solution**: Ensure all forms include `<input type="hidden" name="csrf_token" value="{{ csrf_token() }}"/>`

### Issue: Login Attempts Blocked
**Solution**: Check login attempt logs. Too many failed attempts may trigger rate limiting.

### Issue: 2FA Not Working
**Solution**: 
- Ensure your device time is synchronized
- Try a backup code if available
- Regenerate TOTP secret from account settings

### Issue: Tasks Not Saving
**Solution**: 
- Check database permissions
- Ensure SQLite file is writable
- Check application logs for errors

### Issue: Admin User Not Found
**Solution**: 
```bash
uv run create_admin.py
```

---

## Performance Tips

1. **Database Indexing**: Already optimized with foreign key indexes
2. **Caching**: Consider adding Redis for session caching
3. **Compression**: Enable gzip compression on your web server
4. **CDN**: Use a CDN for static assets (CSS, JS, fonts)
5. **Connection Pooling**: Use SQLAlchemy connection pooling
6. **Load Balancing**: Deploy multiple instances behind a load balancer

---

## Contributing

Contributions are welcome! Please ensure:
- Code follows PEP 8 style guide
- All security best practices are followed
- New features include error handling
- Templates are responsive
- Documentation is updated

---

## License

This project is licensed under the MIT License. See LICENSE file for details.

---

##  Support

### Getting Help
- Check the [Troubleshooting](#troubleshooting) section
- Review application logs in `run.py` output
- Check the [User Guide](#-user-guide) section

### Reporting Issues
Please provide:
1. Detailed description of the issue
2. Steps to reproduce
3. Error messages or logs
4. System information (OS, Python version)

---

## Future Enhancements

- [ ] Email notifications for tasks
- [ ] Task categories and tags
- [ ] Task priorities and due dates
- [ ] Task completion tracking
- [ ] Advanced search and filtering
- [ ] Team collaboration features
- [ ] Mobile app (iOS/Android)
- [ ] API endpoints
- [ ] Dark mode theme
- [ ] Activity history dashboard
- [ ] Export tasks as PDF/CSV
- [ ] Task reminders and scheduling

---

## Contact

For questions or feedback, please reach out to the project maintainer.

---

## Acknowledgments

- Bootstrap for the responsive UI framework
- Font Awesome for beautiful icons
- Flask and SQLAlchemy communities
- PyOTP for 2FA implementation

---

**Version**: 1.0.0  
**Last Updated**: December 4, 2025  
**Status**: Production Ready 

---

## Quick Reference

| Action | URL | Method |
|--------|-----|--------|
| Home | `/` | GET |
| Register | `/register` | GET, POST |
| Login | `/login` | GET, POST |
| Logout | `/logout` | POST |
| Dashboard | `/dashboard` | GET |
| List Tasks | `/tasks` | GET |
| Add Task | `/tasks/add` | GET, POST |
| View Task | `/tasks/<id>` | GET |
| Edit Task | `/tasks/<id>/edit` | GET, POST |
| Delete Task | `/tasks/<id>/delete` | POST |
| Enable 2FA | `/enable_2fa` | GET, POST |
| Verify 2FA | `/verify_2fa` | GET, POST |
| Manage Users | `/admin/users` | GET |
| User Detail | `/admin/users/<id>` | GET |

---

**Happy task managing!**
