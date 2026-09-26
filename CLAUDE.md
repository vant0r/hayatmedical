# HAYAT Medical — Claude Code Project Rules

## 1. Project Identity

Project name: HAYAT Medical

This is a premium medical clinic website with a content management system.

Initial production domain:

`hayatmedical.uz`

Initial languages:

* Uzbek
* Russian

Default language:

* Uzbek

Timezone:

`Asia/Tashkent`

The project must remain domain-independent and hosting-independent.

---

# 2. CRITICAL DEVELOPMENT PRINCIPLES

These rules have the highest priority.

## 2.1 Repository is the source of truth

The GitHub repository is the persistent source of truth.

Never depend on previous Claude conversations.

Never assume that another Claude account explained something to you.

Project knowledge must be preserved in:

* `CLAUDE.md`
* `PROJECT_STATUS.md`
* `TODO.md`
* `DECISIONS.md`

When a new session starts, read these files first.

---

## 2.2 Minimize token usage

TOKEN EFFICIENCY IS CRITICAL.

At the beginning of a session:

1. Read `CLAUDE.md`
2. Read `PROJECT_STATUS.md`
3. Read `TODO.md`
4. Read `DECISIONS.md`

Do NOT automatically read the entire repository.

Do NOT scan every PHP, CSS, JS, image, upload, or database file.

After reading the project-control files:

* identify the current task,
* inspect only files relevant to that task,
* implement the task,
* test the task,
* update project-control files.

Use targeted inspection instead of repository-wide analysis.

---

# 3. CONTINUITY BETWEEN CLAUDE ACCOUNTS

This project may be developed using multiple Claude accounts.

Account 2, Account 3, etc. must be able to continue the project without access to previous conversations.

Therefore:

NEVER restart the project because the conversation is new.

NEVER rebuild working functionality without a technical reason.

NEVER assume missing context.

Use the GitHub repository and project-control files to determine the current state.

Before continuing work:

1. Read the four project-control files.
2. Inspect Git status.
3. Determine the current unfinished task.
4. Inspect only the relevant implementation files.
5. Continue from the existing state.

---

# 4. DEVELOPMENT ENVIRONMENT VS PRODUCTION

The project will initially be developed and tested on temporary/shared hosting.

The final application will later be deployed to a standard cPanel hosting environment.

## CRITICAL REQUIREMENT

The application must be fully portable.

Moving from development hosting to production hosting MUST NOT require rewriting application code.

Only environment-specific configuration should change.

Never hardcode:

* x10host paths
* x10host domains
* development URLs
* absolute server-specific filesystem paths
* hosting-specific APIs
* hosting-specific assumptions

Centralize environment-specific configuration.

Production migration should require only:

1. Upload files
2. Create/import MySQL database
3. Configure database credentials
4. Configure site/environment settings
5. Configure domain
6. Configure SSL
7. Run required installation/migration steps

No application logic rewrite should be required.

---

# 5. TECHNOLOGY

Use:

* PHP 8.3+
* MySQL
* PDO
* HTML5
* CSS3
* Vanilla JavaScript
* JSON where appropriate
* Apache-compatible `.htaccess`

Do NOT introduce:

* Laravel
* Symfony
* React
* Vue
* Angular
* Node.js as a runtime requirement
* unnecessary build systems
* unnecessary frameworks
* unnecessary dependencies

The project must remain lightweight and suitable for shared cPanel hosting.

---

# 6. DATA ARCHITECTURE

Use a hybrid JSON + MySQL architecture.

## JSON

Use JSON for simple/static/configuration-oriented data such as:

* site settings
* facilities
* translations where appropriate
* branding/configuration
* simple static configuration

## MySQL

Use MySQL for relational/dynamic data such as:

* administrators
* doctors
* directions
* services
* departments
* doctor-direction relationships
* doctor-service relationships
* service relationships
* appointments
* news
* media metadata
* SEO metadata where relational storage is useful

Do not put relational application data into JSON.

Do not put simple configuration into MySQL without a reason.

---

# 7. DOMAIN INDEPENDENCE

Never hardcode `hayatmedical.uz` throughout the application.

Site configuration must be centralized.

Examples of configurable values:

* site name
* domain
* logo
* favicon
* phone
* email
* address
* working hours
* timezone
* languages
* social links
* map links
* SEO defaults
* branding

The same application should be deployable for another domain by changing configuration rather than rewriting application logic.

---

# 8. LANGUAGES

The public website supports:

* Uzbek
* Russian

The admin panel also supports:

* Uzbek
* Russian

Default language:

`uz`

Use localized URLs.

Examples:

`/uz/`

`/ru/`

Uzbek examples:

`/uz/shifokorlar/`

`/uz/shifokorlar/jalolov-jahongir-ibragimovich`

`/uz/xizmatlar/`

`/uz/bolimlar/`

`/uz/yangiliklar/`

Russian examples:

`/ru/vrachi/`

`/ru/vrachi/jalolov-jahongir-ibragimovich`

`/ru/uslugi/`

`/ru/otdeleniya/`

`/ru/novosti/`

Slugs must be:

* unique
* editable
* automatically generated by default
* safe for URLs
* language-aware

---

# 9. DOCTORS

Doctors are dynamic CMS content.

A doctor may have:

* full name
* position
* photo
* biography
* education
* experience
* certificates
* work schedule
* directions
* services
* phone/contact information where appropriate
* active/inactive status
* display order
* slug
* SEO metadata

Do not hardcode doctors into PHP templates.

---

# 10. DOCTOR → DIRECTIONS RELATIONSHIP

This is a critical business rule.

Every doctor can have their own medical directions.

Different doctors may have different directions.

Relationship:

Doctor ↔ Directions

This should support many-to-many relationships.

Example:

Doctor:

Jalolov Jahongir

Directions:

* Neurosurgery
* Brain surgery
* Spine surgery

Another doctor may have completely different directions.

Do NOT create one global fixed direction list inside the doctor code.

Directions must be manageable through the admin panel.

---

# 11. SERVICES VS DIRECTIONS

Directions and services are different concepts.

Example:

Direction:

`Neyroxirurgiya`

Service:

`Miya o‘smalarini jarrohlik davolash`

Do not merge these concepts.

Services may be related to:

* doctors
* directions
* departments

where appropriate.

---

# 12. APPOINTMENT REQUEST SYSTEM

The appointment system is a REQUEST system.

It is NOT an automatic online booking system.

User flow:

1. Select doctor
2. Show only directions belonging to that doctor
3. Select direction
4. Enter patient name
5. Enter phone
6. Optional date
7. Optional message
8. Submit request

Critical rule:

After selecting a doctor, the direction list must contain ONLY that doctor's assigned directions.

Do not show unrelated directions.

The filtering may use AJAX/fetch or another lightweight approach appropriate for the architecture.

---

# 13. APPOINTMENT STATUS

Appointment/request statuses:

* New
* In Progress
* Confirmed
* Completed
* Cancelled

Clinic staff manage these statuses through the admin panel.

---

# 14. ADMIN PANEL

Admin must be convenient and simple.

Main sections:

* Dashboard
* Doctors
* Directions
* Services
* Departments
* Facilities
* Appointment Requests
* News
* Media
* Pages
* SEO
* Settings

The dashboard should show useful summary information without unnecessary complexity.

---

# 15. INSTALLER

The project must include:

`install.php`

The installer should:

1. Check PHP version
2. Check required PHP extensions
3. Check filesystem permissions
4. Collect database credentials
5. Connect to MySQL
6. Create required database tables
7. Create initial administrator
8. Create required JSON directories/files
9. Save required configuration
10. Create an installation lock
11. Prevent unauthorized reinstallation

The installer must be safe for shared hosting.

---

# 16. SECURITY

Implement practical security from the beginning.

Use:

* PDO prepared statements
* password_hash()
* password_verify()
* secure sessions
* session regeneration after login
* CSRF protection
* output escaping
* XSS protection
* input validation
* upload validation
* MIME/type validation
* safe filenames
* access control
* basic brute-force protection where practical

Never store plaintext administrator passwords.

Never trust user input.

---

# 17. MEDIA

Uploaded media should be organized.

Suggested structure:

`/uploads/doctors/`

`/uploads/services/`

`/uploads/news/`

`/uploads/gallery/`

Validate uploads before saving them.

Do not allow arbitrary executable files to be uploaded.

Optimize images where practical.

---

# 18. SEO

The system should support:

* SEO title
* SEO description
* canonical URL
* Open Graph metadata
* OG image
* clean slug
* sitemap.xml
* robots.txt
* language-aware URLs

Dynamic pages should generate appropriate metadata.

---

# 19. DESIGN

The design direction is:

Apple × Luxury Medical × Modern Technology.

The website should feel:

* premium
* calm
* trustworthy
* modern
* sophisticated
* clean
* medically credible

Avoid:

* generic hospital templates
* childish UI
* excessive gradients
* excessive glassmorphism
* unnecessary animations
* visually noisy layouts
* huge amounts of decorative elements

The provided HTML prototype is the primary visual reference.

---

# 20. HTML PROTOTYPE

The prototype will be provided under:

`reference/design.html`

The prototype must be treated as the main visual reference.

Do not redesign it unnecessarily.

Convert its structure into reusable PHP components and dynamic CMS content.

Preserve the visual language unless there is a technical or usability reason to change something.

Do not replace a working design with a generic template.

---

# 21. RESPONSIVENESS

The website must work properly on:

* desktop
* laptop
* tablet
* mobile

Do not treat mobile as an afterthought.

---

# 22. CODE QUALITY

Prefer:

* simple code
* readable code
* reusable components
* clear naming
* small functions
* centralized configuration
* minimal duplication

Avoid:

* overengineering
* unnecessary abstraction
* unnecessary classes
* unnecessary files
* unnecessary dependencies

The project is intentionally lightweight.

---

# 23. CHANGE POLICY

Before modifying existing functionality:

1. Understand what the existing code does.
2. Identify dependencies.
3. Make the smallest safe change.
4. Test the affected functionality.
5. Verify that existing functionality still works.

Do not rewrite working systems just for stylistic reasons.

---

# 24. GIT WORKFLOW

Use Git consistently.

Before major changes:

* inspect `git status`
* inspect relevant changes

After completing a meaningful feature:

1. Test
2. Review diff
3. Update project-control files
4. Commit
5. Push to GitHub

Use clear commit messages.

Examples:

`feat: add doctor management`

`feat: add doctor direction relationships`

`feat: add appointment requests`

`fix: filter directions by selected doctor`

`feat: add russian localization`

`fix: improve upload validation`

Never commit passwords, secrets, API keys, or database credentials.

---

# 25. PROJECT STATUS MANAGEMENT

After completing a meaningful task, update:

`PROJECT_STATUS.md`

Update:

`TODO.md`

If an architectural decision changes or a new important decision is made, update:

`DECISIONS.md`

The project-control files must remain concise and useful.

Do not fill them with unnecessary explanations.

---

# 26. SESSION END PROTOCOL

If the current session is ending or usage is getting close to its limit:

STOP starting large new features.

Before stopping:

1. Finish the current safe unit of work if possible.
2. Test changes.
3. Update `PROJECT_STATUS.md`.
4. Update `TODO.md`.
5. Update `DECISIONS.md` if necessary.
6. Review Git diff.
7. Commit changes.
8. Push to GitHub.

The next Claude account must be able to continue from the repository without the previous conversation.

---

# 27. NEW SESSION PROTOCOL

When starting a new session:

Read:

1. `CLAUDE.md`
2. `PROJECT_STATUS.md`
3. `TODO.md`
4. `DECISIONS.md`

Then:

* inspect `git status`
* identify the current task
* inspect only relevant files
* continue existing work

Do NOT scan the entire repository unless explicitly required.

Do NOT restart completed work.

Do NOT redesign the project without instruction.

---

# 28. DECISION PRIORITY

When information conflicts, use this priority:

1. Current explicit user instruction
2. `CLAUDE.md`
3. `PROJECT_STATUS.md`
4. `DECISIONS.md`
5. `TODO.md`
6. Existing implementation
7. Previous conversation context

The repository is more reliable than conversation history.

---

# 29. FINAL PRINCIPLE

Build the smallest robust system that satisfies the requirements.

Do not build an enterprise system unnecessarily.

Do not sacrifice maintainability for speed.

Do not sacrifice portability for development convenience.

Do not sacrifice security for simplicity.

Do not waste tokens analyzing files that are unrelated to the current task.

Work incrementally.

Keep the project deployable at every major milestone.
