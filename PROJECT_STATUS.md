# HAYAT Medical — Project Status

## Project

**Name:** HAYAT Medical

**Domain:** hayatmedical.uz

**Status:** Planning / Initial Development

**Default language:** Uzbek

**Additional language:** Russian

**Timezone:** Asia/Tashkent

---

# Current Phase

## Phase 0 — Project Initialization

The project has not yet been fully implemented.

Current priority:

1. Prepare repository
2. Prepare project documentation
3. Add HTML design prototype
4. Analyze prototype
5. Establish lightweight architecture
6. Create database structure
7. Create installer
8. Build public website
9. Build admin CMS
10. Test
11. Deploy to production

---

# Development Environment

Current development/testing hosting:

**x10host**

Purpose:

* development
* testing
* prototype implementation
* client-side review
* functionality verification

Production hosting will be a standard cPanel hosting environment.

Production hosting must not require application code rewrites.

---

# Technology

* PHP 8.3+
* MySQL
* PDO
* HTML5
* CSS3
* Vanilla JavaScript
* JSON
* Apache / `.htaccess`

No unnecessary frameworks.

---

# Architecture

Hybrid:

### JSON

Used for:

* configuration
* simple static content
* facilities
* translations where appropriate

### MySQL

Used for:

* administrators
* doctors
* directions
* services
* departments
* doctor-direction relationships
* doctor-service relationships
* appointments
* news
* media metadata
* relational CMS data

---

# Core Business Rules

## Doctors

Doctors are managed dynamically through the admin panel.

Each doctor may have different medical directions.

---

## Doctor → Direction

Many-to-many relationship.

Example:

Jalolov Jahongir:

* Neyroxirurgiya
* Miya jarrohligi
* Umurtqa jarrohligi

Other doctors may have different directions.

---

## Directions vs Services

These are separate entities.

Example:

Direction:

`Neyroxirurgiya`

Service:

`Miya o‘smalarini jarrohlik davolash`

---

## Appointment

Appointment is a request, not automatic booking.

Flow:

Doctor
→ Doctor-specific directions
→ Patient name
→ Phone
→ Optional date
→ Optional message
→ Request

Statuses:

* New
* In Progress
* Confirmed
* Completed
* Cancelled

---

# Languages

Public website:

* Uzbek
* Russian

Admin:

* Uzbek
* Russian

Default:

Uzbek

Localized URLs are required.

---

# Design

Design direction:

**Apple × Luxury Medical × Modern Technology**

Main characteristics:

* premium
* calm
* trustworthy
* clean
* modern
* sophisticated
* medically credible

Avoid generic hospital design.

---

# Design Prototype

Prototype location:

`reference/design.html`

The prototype is the primary visual reference.

It should be converted into the actual PHP website rather than replaced with a generic template.

---

# Admin Sections

Planned:

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

---

# Installation

Planned:

`install.php`

Installer requirements:

* PHP checks
* extension checks
* permission checks
* MySQL setup
* database schema creation
* initial admin creation
* configuration
* installation lock

---

# SEO

Planned:

* SEO title
* SEO description
* canonical
* Open Graph
* OG image
* clean localized slugs
* sitemap.xml
* robots.txt

---

# Security

Required:

* PDO prepared statements
* password hashing
* CSRF
* session security
* output escaping
* input validation
* upload validation
* access control

---

# Hosting Portability

Critical requirement:

Development hosting → Production cPanel must not require rewriting application code.

Only environment-specific configuration should change.

---

# Current Completed

* Project concept defined
* Lightweight architecture selected
* JSON/MySQL responsibilities defined
* Doctor → Direction relationship defined
* Appointment request flow defined
* Admin sections defined
* Hosting migration principle defined
* Claude multi-account continuity strategy defined

---

# Current In Progress

* GitHub repository preparation
* Project-control files
* HTML prototype upload
* Initial Claude Code development

---

# Next Task

1. Add final `CLAUDE.md`
2. Add `PROJECT_STATUS.md`
3. Add `TODO.md`
4. Add `DECISIONS.md`
5. Upload HTML prototype to `reference/design.html`
6. Start Claude Code project initialization
7. Inspect prototype
8. Create project architecture
9. Create database schema
10. Create installer

---

# Last Session

Initial project planning.

No production deployment yet.

---

# Important

Do not assume that unfinished sections are completed.

Always update this file after meaningful implementation changes.
