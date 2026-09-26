# HAYAT Medical — Technical Decisions

This file contains important architectural and product decisions.

Do not change these decisions without a clear technical or business reason.

---

## D001 — Lightweight Architecture

**Decision:** Use a lightweight PHP architecture.

**Chosen:**

* PHP 8.3+
* MySQL
* PDO
* HTML
* CSS
* Vanilla JS
* JSON

**Rejected for this project:**

* Laravel
* React
* Vue
* Angular
* unnecessary Node.js runtime
* unnecessary enterprise architecture

**Reason:**

The project must be:

* lightweight
* maintainable
* fast
* inexpensive to host
* compatible with shared cPanel hosting
* easy to deploy

---

## D002 — Hybrid JSON + MySQL

**Decision:** Use both JSON and MySQL.

### JSON

For:

* simple configuration
* facilities
* translations where appropriate
* branding/configuration
* simple static data

### MySQL

For:

* administrators
* doctors
* directions
* services
* departments
* relationships
* appointments
* news
* media metadata
* relational CMS data

**Reason:**

Avoid unnecessary database complexity while keeping relational data reliable.

---

## D003 — Hosting Portability

**Decision:**

Development hosting and production hosting must use the same application code.

Initial development/testing:

`x10host`

Final production:

Standard cPanel hosting.

**Critical rule:**

Moving to production must NOT require rewriting application logic.

Only environment-specific configuration may change.

**Reason:**

Development hosting is temporary. The application must remain portable.

---

## D004 — Domain Independence

**Decision:**

The application must not be hardcoded specifically for `hayatmedical.uz`.

The initial site is HAYAT Medical and the planned domain is:

`hayatmedical.uz`

But domain/site configuration must be centralized.

**Reason:**

The application should be reusable and easier to migrate.

---

## D005 — Languages

**Decision:**

Public website:

* Uzbek
* Russian

Admin:

* Uzbek
* Russian

Default:

Uzbek.

Localized URLs are required.

---

## D006 — Doctors and Directions

**Decision:**

Doctor and Direction are separate entities.

Relationship:

Doctor ↔ Direction = many-to-many.

Each doctor may have different directions.

Example:

Jalolov Jahongir:

* Neyroxirurgiya
* Miya jarrohligi
* Umurtqa jarrohligi

**Reason:**

Medical specialization differs between doctors.

---

## D007 — Directions and Services

**Decision:**

Directions and Services are different entities.

Example:

Direction:

`Neyroxirurgiya`

Service:

`Miya o‘smalarini jarrohlik davolash`

A service may be related to doctors, directions, and departments where appropriate.

---

## D008 — Appointment System

**Decision:**

The appointment form creates a request.

It does NOT automatically book an appointment.

Flow:

Doctor
→ Doctor-specific Direction
→ Patient Name
→ Phone
→ Optional Date
→ Optional Message
→ Request

Statuses:

* New
* In Progress
* Confirmed
* Completed
* Cancelled

Clinic staff manually process requests.

---

## D009 — Doctor-Specific Direction Filtering

**Decision:**

When a visitor selects a doctor, the appointment form must display only directions assigned to that doctor.

Example:

Doctor A:

* Direction 1
* Direction 2

Doctor B:

* Direction 3
* Direction 4

Selecting Doctor A must never display Doctor B's directions.

---

## D010 — HTML Prototype

**Decision:**

The provided HTML prototype is the primary visual reference.

Location:

`reference/design.html`

Claude must convert the prototype into reusable PHP components.

Claude must not replace the prototype with a generic hospital template without explicit instruction.

---

## D011 — Admin as CMS

**Decision:**

The admin panel is a CMS/control center, not merely a database-entry interface.

Planned modules:

* Dashboard
* Doctors
* Directions
* Services
* Departments
* Facilities
* Appointments
* News
* Media
* Pages
* SEO
* Settings

---

## D012 — Installer

**Decision:**

The project will use:

`install.php`

The installer will:

* check environment
* configure database
* create schema
* create administrator
* create configuration
* create required directories
* lock itself after installation

---

## D013 — Security

**Decision:**

Security is required from the beginning.

Required:

* PDO prepared statements
* password hashing
* CSRF protection
* secure sessions
* output escaping
* input validation
* upload validation
* access control

---

## D014 — Multi-Account Development

**Decision:**

Multiple Claude accounts may work on the same GitHub repository.

Project continuity must never depend on Claude conversation history.

Persistent state is stored in:

* `CLAUDE.md`
* `PROJECT_STATUS.md`
* `TODO.md`
* `DECISIONS.md`
* Git history
* actual project files

---

## D015 — Token Efficiency

**Decision:**

Claude must not read the entire repository at every session.

Initial reading:

1. `CLAUDE.md`
2. `PROJECT_STATUS.md`
3. `TODO.md`
4. `DECISIONS.md`

Then inspect only files relevant to the current task.

**Reason:**

Reduce token usage and allow longer development sessions.

---

## D016 — Git Continuity

**Decision:**

Every meaningful completed feature should be committed and pushed.

Before handing work to another Claude account:

1. Test
2. Update project-control files
3. Review diff
4. Commit
5. Push

**Reason:**

Another account must be able to continue from the latest GitHub state.

---

## D017 — Production Migration

**Decision:**

Production deployment should be a migration, not a redevelopment.

Expected process:

Development hosting
→ database export
→ production database
→ application upload
→ configuration
→ domain
→ SSL
→ testing

No application rewrite.

---

## D018 — Shared Hosting Compatibility

**Decision:**

The application must work on normal cPanel shared hosting.

Avoid dependencies that require:

* root server access
* Docker
* persistent Node processes
* custom server daemons
* unusual server configuration

---

## D019 — No Premature Telegram Dependency

**Decision:**

The core website and CMS should work independently from Telegram.

Telegram integration can be added later.

The appointment system must not depend on a Telegram bot to function.

---

## D020 — No Overengineering

**Decision:**

Do not build an unnecessarily large enterprise architecture.

Every new abstraction, dependency, service, table, or layer must have a practical reason.

Prefer:

simple → reliable → maintainable → portable.

---

# Change Policy

If one of these decisions needs to change:

1. Explain why.
2. Check impact on existing code.
3. Update this file.
4. Update `PROJECT_STATUS.md`.
5. Update `TODO.md` if required.
6. Then implement the change.

Do not silently change architectural decisions.
