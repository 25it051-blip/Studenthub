# StudentHub Portal

**Course**: ITUE203 - Web Development Frameworks  
**Department**: Information Technology (IT), CSPIT, CHARUSAT University  
**Student Name**: Aesha Rakeshkumar Makwana  
**Student ID**: 25IT051  

---

## 1. Problem Definition & Scope

Students and faculty require a centralized, responsive, and secure web application to access campus-related information, manage student profiles, discover and register for campus events, access academic schedules, and enable administrative oversight with audit logging.

StudentHub addresses this need by providing an integrated full-stack web application designed and built across 14 progressive practical milestones.

---

## 2. Project Architecture & Practicals Summary

| Practical | Module / Topic | Core Technologies & Features |
| :--- | :--- | :--- |
| **Practical 01** | Project Planning & Setup | Scope, sitemap, wireframes, repository architecture |
| **Practical 02** | HTML5 Semantic Skeletons | Core structural pages and accessible layouts |
| **Practical 03** | Responsive UI Design | CSS Grid, Flexbox, media queries, mobile-first styling (`style.css`) |
| **Practical 04** | JavaScript DOM & Events | Dynamic UI components: FAQ accordion, modals, image sliders, notification banner, dark mode switcher (`script.js`) |
| **Practical 05** | Form Validation | Client-side validation: Regex, real-time error states, password strength indicator (`register.html`) |
| **Practical 06** | JSON Rendering & Fetch API | Asynchronous loading of external JSON (`events.json`, `students.json`, `faqs.json`) |
| **Practical 07** | Server-Side Form Processing | PHP form validation, sanitization, CSV and JSON file storage (`pr7_contact.php`, `pr7_records.php`) |
| **Practical 08** | MySQL Schema & Connectivity | Relational database schema (`schema.sql`), 3NF design, PDO connection with UTF-8mb4 and error modes (`includes/db.php`, `test_db.php`) |
| **Practical 09** | Secure User Registration | Server-side validation, duplicate email checks, cryptographic password hashing using `PASSWORD_BCRYPT` (`secure_register.php`) |
| **Practical 10** | Authentication & RBAC | PHP session management, role-based access control (Student vs Admin), session fixation prevention, timeout checks, remember-me token handling (`secure_login.php`, `includes/auth.php`, `student_portal.php`) |
| **Practical 11** | Student Management CRUD | Admin CRUD interface for student records, parameterized MySQLi statements, search, filter, pagination, and CSV export (`manage_students.php`, `export_students.php`) |
| **Practical 12** | Event Management & File Upload | Defensive image upload handling (MIME verification, extension whitelisting, size limits, path traversal defense), event CRUD (`manage_events.php`, `uploads/.htaccess`) |
| **Practical 13** | RESTful PHP JSON API | Asynchronous JSON API endpoints (`api/events_api.php`) consumed by dynamic single-page Fetch CRUD client (`ajax_events_manager.php`) |
| **Practical 14** | Admin Dashboard & Governance | Role-based dashboard with statistical aggregation cards, quick navigation, and persistent audit logging (`admin_dashboard.php`, `includes/audit.php`) |

---

## 3. Directory Structure

```text
StudentHub/
│
├── api/
│   └── events_api.php            # RESTful JSON API endpoints for event CRUD
│
├── css/
│   └── backend.css               # Admin dashboard and management portal styles
│
├── data/
│   ├── contacts.csv              # CSV data storage for contact form submissions
│   └── contacts.json             # JSON structured storage for form records
│
├── database/
│   └── schema.sql                # Complete MySQL relational database schema & seed data
│
├── docs/
│   ├── sitemap/                  # Information architecture diagrams
│   └── wireframes/               # UI blueprint wireframe images
│
├── includes/
│   ├── audit.php                 # Central audit logging function
│   ├── auth.php                  # Authentication helpers, session verification, RBAC guard
│   ├── db.php                    # PDO database connection with prepared statement configuration
│   ├── footer.php                # Shared administrative footer
│   └── header.php                # Shared administrative navigation and session banner
│
├── pages/                        # Initial static page templates from Practicals 1 & 2
│
├── uploads/
│   ├── posters/                  # Secure directory for uploaded event poster images
│   └── .htaccess                 # Direct script execution prevention in upload directory
│
├── about.html                    # About Us page with campus details
├── admin_dashboard.php           # Practical 14: Administrative overview with KPI cards & audit log
├── ajax_events_manager.php       # Practical 13: Single-page asynchronous event manager
├── attendance.html               # Attendance tracking view
├── contact.html                  # Static contact page
├── dashboard.html                # Static dashboard interface
├── events.json                   # Mock data for campus events
├── export_students.php           # Practical 11: CSV export handler
├── faqs.json                     # Mock data for campus FAQ items
├── fees.html                     # Fee structure page
├── index.html                    # Main landing page with hero, notices, and dynamic components
├── login.html                    # Static login mock page
├── logout.php                    # Practical 10: Secure session termination & cookie destruction
├── manage_events.php             # Practical 12: Admin event CRUD with file upload
├── manage_students.php           # Practical 11: Admin student CRUD with search and filter
├── pr7_contact.php               # Practical 7: PHP contact form handler with dual file storage
├── pr7_records.php               # Practical 7: Stored records viewer
├── profile.html                  # Student profile management page
├── register.html                 # Practical 5: Comprehensive client-validated registration form
├── result.html                   # Examination results page
├── script.js                     # Practicals 4, 5, 6: Client-side JavaScript logic
├── secure_login.php              # Practical 10: Secure login with password verification
├── secure_register.php           # Practical 9: Secure database registration with bcrypt
├── students.json                 # Mock data for enrolled students
├── student_portal.php            # Practical 10: Role-restricted student dashboard
├── style.css                     # Practical 3: Global responsive CSS (Grid, Flexbox, media queries)
├── test_db.php                   # Practical 8: Database connectivity & diagnostic tool
├── timetable.html                # Weekly lecture and laboratory schedule
└── unauthorized.php              # Access denial page for RBAC violations
```

---

## 4. Database Setup & Configuration

1. **Prerequisites**: MySQL Server / MariaDB (via XAMPP, WAMP, or standalone).
2. **Import Database**:
   ```sql
   mysql -u root -p < database/schema.sql
   ```
   Or import `database/schema.sql` via **phpMyAdmin**.
3. **Database Credentials**:
   Configured in `includes/db.php`:
   - Host: `localhost`
   - Database: `studenthub_db`
   - Username: `root`
   - Password: `""` (empty by default)
   - Charset: `utf8mb4`

4. **Default Accounts**:
   - **Admin Account**: `admin@studenthub.edu` / `Admin@123`
   - **Student Account**: `student@studenthub.edu` / `Student@123`

---

## 5. Security Measures Implemented

- **Password Hashing**: Cryptographic `PASSWORD_BCRYPT` with adaptive cost factor.
- **SQL Injection Prevention**: 100% prepared statements with parameterized queries using PDO and MySQLi.
- **Cross-Site Scripting (XSS)**: All user-rendered outputs sanitized using `htmlspecialchars($val, ENT_QUOTES, 'UTF-8')`.
- **Session Security**:
  - `session_regenerate_id(true)` called upon login to mitigate session fixation.
  - Idle timeout enforcement (30-minute expiration).
  - Secure destruction on logout.
- **Role-Based Access Control (RBAC)**: Strict role checking (`admin` vs `student`) gating access to sensitive routes.
- **Defensive File Uploads**:
  - Whitelist validation of extensions (`jpg`, `jpeg`, `png`, `webp`).
  - MIME-type verification using `finfo_file` (not trusting client headers).
  - File size capping (max 2 MB).
  - File renaming to cryptographically random names to avoid collisions and directory traversal.
  - `.htaccess` disabling script execution inside `uploads/`.

---

## 6. How to Run Locally

1. Place the project directory inside your local server webroot (e.g., `C:/xampp/htdocs/Studenthub`).
2. Start Apache and MySQL services in the XAMPP Control Panel.
3. Import the database schema from `database/schema.sql`.
4. Open your browser and navigate to:
   - Landing Page: `http://localhost/Studenthub/index.html`
   - Secure Login: `http://localhost/Studenthub/secure_login.php`
   - Admin Dashboard: `http://localhost/Studenthub/admin_dashboard.php`
   - Stored Records (Practical 7): `http://localhost/Studenthub/pr7_records.php`
