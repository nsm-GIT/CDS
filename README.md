# CDS — Canal Digging Software

**CDS (Canal Digging Software)** is a desktop engineering application developed for canal excavation, earthwork calculation, cross-section analysis, quantity calculation, and engineering reporting.

The application is designed as a modern Windows desktop solution using **Python, PySide6, and SQLite**, with an interface and workflow inspired by traditional engineering database applications.

---

## Features

### Project Management

- Create and open CDS projects
- Project-based SQLite database
- Project details management
- Automatic project database creation from a template
- Project number and project name management
- District, Division and Paurosova information
- Project start date
- Working zone configuration
- BOX type and dimensional parameters

### Cross-Section Management

- Enter and edit chainage records
- Existing ground levels
- Design levels
- Left and right side measurements
- Soil type information
- Cut and fill calculations
- Cross-section visualization
- Automatic navigation between records
- First, previous, next and last record navigation

### Earthwork Calculation

CDS provides engineering calculations for:

- Existing ground profile
- Design profile
- Cut area
- Fill area
- Net area
- Excavation quantities
- Embankment quantities
- Cross-section-based calculations

### Graphical Visualization

The application provides graphical representations of engineering data, including:

- Cross-section diagrams
- Existing ground lines
- Design lines
- Embankment lines
- Grid and datum lines
- Cut/fill areas
- Long-section visualization

### Reports

CDS supports engineering reports and graphical output for project data and calculated quantities.

### Settings

Application settings allow users to configure:

- Decimal precision
- Line styles
- Line colors
- Text colors
- Graph appearance
- Report appearance

---

# Technology Stack

| Technology | Purpose |
|---|---|
| Python 3.13 | Application development |
| PySide6 | Desktop GUI |
| SQLite | Project database |
| PyInstaller | Windows executable |
| Inno Setup | Windows installer |
| Git / GitHub | Source-code management |

---

# Application Architecture

The application follows a modular Python architecture.

```text
CDS
│
├── Main.py
├── authenticator.py
├── api.py
├── globals.py
│
├── earthwork.py
├── calculation.py
├── total_calculation_x.py
├── x_section.py
├── long_section.py
├── three_d.py
│
├── project_details.py
├── project_loader.py
├── settings.py
├── basic_rates.py
│
├── reports.py
├── blank.py
│
├── ui/
│   ├── authenticator.ui
│   ├── project_details.ui
│   └── ...
│
├── assets/
│   ├── _icons/
│   ├── _pics/
│   └── _templates/
│
├── templates/
│
├── reports/
│
├── textures/
│
├── Dbase/
│
└── cds_template.sqlite
```

---

# Database

CDS uses **SQLite** for project data.

A new project is created from the database template:

```text
cds_template.sqlite
```

The template provides the initial database structure required by the application.

Project databases can then be created independently for individual projects.

This approach keeps each project self-contained and makes project backup and transfer straightforward.

---

# Installation

## From Source

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/CDS.git
```

Enter the project directory:

```bash
cd CDS
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate the environment on Windows:

```powershell
.venv\Scripts\Activate.ps1
```

Install the required packages:

```bash
pip install -r requirements.txt
```

Run CDS:

```bash
python Main.py
```

---

# Required Python Packages

Typical dependencies include:

```text
PySide6
requests
mysql-connector-python
```

Additional packages may be required depending on the enabled CDS modules.

A `requirements.txt` file should be maintained with the exact versions used for production builds.

Example:

```text
PySide6
requests
mysql-connector-python
```

---

# Building the Windows Application

CDS can be packaged using **PyInstaller**.

For example:

```bash
python -m PyInstaller Main.spec
```

The generated application will be placed in the `dist` directory.

For a one-directory deployment:

```text
dist/
└── CDS/
    ├── CDS.exe
    └── _internal/
        ├── python313.dll
        ├── Qt6Core.dll
        ├── Qt6Gui.dll
        ├── Qt6Widgets.dll
        └── ...
```

The entire `CDS` directory should be distributed together.

---

# Windows Installer

The production application can be packaged using **Inno Setup**.

The installer creates:

```text
C:\Program Files (x86)\CDS\
```

or the selected installation directory.

The installer can provide:

- Start Menu shortcut
- Desktop shortcut
- Application icon
- Uninstaller
- Automatic application launch after installation

---

# Authentication and Licensing

CDS includes an online authentication and licensing system.

The application identifies a computer using machine information such as:

- Computer name
- Windows user
- Machine GUID
- PC ID
- Motherboard serial
- BIOS serial
- HDD serial
- MAC address
- CPU ID

The application communicates with the CDS licensing server through an HTTP API.

The authentication workflow is:

```text
Start CDS
    │
    ▼
Collect Computer Identity
    │
    ▼
Contact Licensing Server
    │
    ▼
Check PC Registration
    │
    ├── Not Registered
    │       │
    │       ▼
    │   Registration Form
    │
    ├── Pending
    │
    ├── Approved
    │       │
    │       ▼
    │   Email Activation
    │
    ├── Activated
    │       │
    │       ▼
    │   Start CDS
    │
    ├── Rejected
    │
    └── Blocked
```

The licensing server uses a separate web API and database to manage registered users and computers.

---

# User Registration

When a new computer starts CDS for the first time, the application can display the registration form.

The user provides:

- Full name
- Organization
- Email address

The application automatically adds the computer identity information.

The registration is then submitted to the licensing server.

---

# License Activation

After administrator approval, CDS generates an activation token.

The user receives an activation email containing an activation link.

The activation process changes the license status from:

```text
Approved
```

to:

```text
Activated
```

After successful activation, the user can start CDS.

---

# Security

The application uses:

- HTTPS communication
- Password hashing on the server
- Unique PC identification
- Activation tokens
- Activation expiry
- Server-side license validation
- User status management

Possible account states include:

```text
Pending
Approved
Activated
Rejected
Blocked
```

---

# User Interface

CDS is developed using **PySide6**, providing a native desktop application experience on Windows.

The application includes:

- Main window
- Project management
- Cross-section interface
- Long-section interface
- Reports
- Settings
- Authentication
- Splash screen
- Engineering visualization

---

# Splash Screen

CDS uses a custom splash screen during application startup.

The splash screen provides startup information such as:

```text
Starting CDS...
Loading modules...
Connecting database...
Checking license...
Loading interface...
```

This provides users with visual feedback while the application initializes.

---

# Project Workflow

A typical CDS workflow is:

```text
Create Project
      │
      ▼
Enter Project Details
      │
      ▼
Enter Chainage Data
      │
      ▼
Enter Existing Ground Data
      │
      ▼
Define Design Parameters
      │
      ▼
Calculate Cross Sections
      │
      ▼
Calculate Earthwork
      │
      ▼
Review Graphs
      │
      ▼
Generate Reports
```

---

# Development

## Recommended Development Environment

- Windows 10 / Windows 11
- Python 3.13+
- PyCharm
- Git
- SQLite
- Qt Designer

---

# Project Structure

The major modules are organized according to their responsibilities.

### Core

```text
Main.py
globals.py
settings.py
```

### Authentication

```text
authenticator.py
api.py
```

### Project Management

```text
project_details.py
project_loader.py
```

### Engineering Calculation

```text
earthwork.py
calculation.py
total_calculation_x.py
```

### Cross Sections

```text
x_section.py
```

### Long Sections

```text
long_section.py
```

### Visualization

```text
three_d.py
```

### Reports

```text
reports.py
```

### UI

```text
ui/
```

### Resources

```text
assets/
templates/
textures/
reports/
Dbase/
```

---

# GitHub Repository Structure

For GitHub, the repository should ideally contain:

```text
CDS/
│
├── README.md
├── requirements.txt
├── Main.py
├── Main.spec
│
├── assets/
├── ui/
├── templates/
├── textures/
├── reports/
├── Dbase/
│
└── src/
```

Temporary and generated files should normally **not** be committed:

```text
__pycache__/
build/
dist/
.venv/
.idea/
*.pyc
```

A `.gitignore` file should therefore be used.

---

# Example `.gitignore`

```gitignore
# Python
__pycache__/
*.py[cod]
*.pyo

# Virtual environment
.venv/
venv/
env/

# PyCharm
.idea/

# PyInstaller
build/
dist/
*.spec.bak

# Temporary files
*.tmp
*.log

# SQLite temporary files
*-journal
*-wal
*-shm

# OS files
.DS_Store
Thumbs.db
```

---

# Roadmap

Future development may include:

- [ ] Improved project dashboard
- [ ] Advanced cross-section editing
- [ ] Automatic quantity summaries
- [ ] Improved reporting system
- [ ] PDF report generation
- [ ] Excel export
- [ ] Advanced graphical customization
- [ ] 3D canal visualization
- [ ] Online license management
- [ ] Automatic application updates
- [ ] Cloud project backup
- [ ] Multi-language support

---

# License

CDS is proprietary software.

The source code is provided for authorized development and maintenance purposes only.

Unauthorized copying, redistribution, modification, or commercial use is not permitted without permission from the software owner.

---

# Author

**CDS — Canal Digging Software**

Developed as an engineering desktop application for canal excavation and earthwork management.

---

## Disclaimer

CDS is intended as an engineering calculation and project-management tool.

Users should verify engineering calculations, design parameters, quantities, and reports before using the results for construction or official engineering purposes.

---

## Status

**Development Status:** Active Development

**Platform:** Windows

**Application Type:** Desktop Engineering Software

**Primary Language:** Python

**GUI Framework:** PySide6

**Database:** SQLite

**Build System:** PyInstaller

**Installer:** Inno Setup