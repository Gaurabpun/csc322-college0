# College0: An AI-Enabled Online College Program Management System

## Table of Contents
- [Project Overview](#project-overview)
- [User Roles](#user-roles)
- [System Requirements](#system-requirements)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [AI Feature](#ai-feature)
- [Team](#team)

---

## Project Overview

**College0** is a full-featured, AI-enabled college program management system built as part of a Software Engineering group project. The system manages the full lifecycle of an academic semester — from class setup and student registration to grading and graduation — for a simulated college environment. It is designed as a single-window GUI application (web or local) supporting multiple user roles with distinct permissions.

> **Note:** This is a toy/demo system. A small dataset (~10 students) is sufficient to showcase all features.

---

## User Roles

| Role | Description |
|------|-------------|
| **Registrar** | Super user. Has full administrative control over the system. |
| **Instructor** | Can access and manage courses they are assigned to. |
| **Student** | Can manage their own course registrations and academic records. |
| **Visitor** | Can browse basic public information such as classes and student listings. |

---

## System Requirements

### 1. Public Dashboard (All Users)
- A GUI home page displaying:
  - General program introduction
  - Highest-rated classes
  - Lowest-rated classes
  - Students with the highest GPA

### 2. Application & Enrollment
- Visitors can apply to become a student or an instructor.
- **Student applications** are reviewed by the Registrar:
  - Auto-accepted if GPA > 3.0 and program quota is not reached.
  - Otherwise rejected; Registrar must provide justification if overriding the rule.
  - Accepted students receive a unique student ID and temporary password (must be changed on first login).
- **Instructor applications** are approved or rejected by the Registrar with no justification required.
  - Approved instructors are assigned class(es).

### 3. Semester Periods
A semester consists of four sequential periods managed by Registrars:

| Period | Description |
|--------|-------------|
| **Class Set-Up Period** | Registrars configure classes, schedules, instructors, and class sizes. |
| **Course Registration Period** | Matriculated students register for 2–4 courses (no time conflicts; upper enrollment limits enforced). Students on the waitlist can only be admitted by the course instructor. A student may retake a class only if they previously received an F. |
| **Class Running Period** | No new registrations (except a special re-registration window). Students with fewer than 2 courses are warned. Courses with fewer than 3 students are cancelled; affected students get one chance to re-register. Instructors whose courses are all cancelled are suspended. |
| **Grading Period** | Instructors assign final grades. Instructors who fail to grade are warned. Class GPAs outside the 2.5–3.5 range trigger a registrar review. |

### 4. Student Academic Standing
- Students with GPA < 2.0 or who fail the same course twice are **automatically terminated**.
- Students with GPA between 2.0–2.25 receive a **warning** and must meet with the Registrar.
- Students with semester GPA > 3.75 or cumulative GPA > 3.5 (after 1+ semesters) are labeled **Honor Roll students** automatically. One honor distinction can be used to remove one existing warning.
- Students completing 8 classes may **apply for graduation**. If all required courses are completed, the student graduates with a Bachelor's degree and exits the system. Otherwise, they receive a warning for a reckless graduation application.

### 5. Reviews & Ratings
- Students enrolled in a class can submit written reviews and star ratings (1–5) during the class running period.
- Reviews are anonymous to everyone except Registrars.
- Ratings cannot be submitted after the instructor posts the final grade.
- Instructors with an average class rating < 2 receive a **warning**. Three warnings result in **suspension**.
- **Taboo word filtering** (taboo word list is managed by Registrars):
  - Reviews with 1–2 taboo words: displayed with those words replaced by `*`; author receives 1 warning.
  - Reviews with 3+ taboo words: hidden entirely; author receives 2 warnings.

### 6. Complaints
- **Students** can file complaints against other students or instructors with the Registrar.
  - Registrar investigates and may issue a warning to the relevant party.
- **Instructors** can file complaints to warn or de-register a student.
  - Registrar must take action: punish the student or issue 1 warning to the instructor.
- Students accumulating **3 warnings** are **suspended for 1 semester** and must pay a fine.

### 7. User Dashboards
- **Instructor dashboard:** View basic info and academic records of students in current class(es).
- **Student dashboard:** View personal academic records. New students receive an onboarding tutorial.
- **Registrar dashboard:** Full system access and oversight.

### 8. AI-Powered Assistant (Feature 9)
See the [AI Feature](#ai-feature) section below.

### 9. Creative Feature (Feature 10)
*(To be defined by the team — see [Team](#team) section for our chosen enhancement.)*

---

## AI Feature

College0 includes a context-aware AI assistant powered by a local vector database and an LLM backend.

- **Visitors** can ask general questions about classes and admission requirements.
- **Students** can ask additional questions about their enrolled courses.
- **Instructors** can ask additional questions about students in their class(es).

**How it works:**
1. User query is first searched against a local vector store containing College0-specific information.
2. If a relevant answer is found locally, it is returned directly.
3. If no local match is found, the query is forwarded to a general-purpose LLM with a disclaimer:
   > ⚠️ *This answer was generated by a general LLM and may not be accurate for College0. Hallucinations are possible.*

---

## Tech Stack

| Layer | Technology                           |
|-------|--------------------------------------|
| Frontend / GUI | *HTML, CSS, JS*                      |
| Backend | *Python/Flask*                       |
| Database | *MySQL*                              |
| Vector Store (AI) | *ChromaDB, Pinecone*                 |
| LLM Integration | *OpenAI API, Claude API, Gemini API* |

---

## Installation

```bash
# Clone the repository
git clone https://github.com/<your-team>/<your-repo>.git
cd <your-repo>

# Install dependencies
# (Update with your actual package manager and commands)
pip install -r requirements.txt
# or
npm install

# Set up environment variables
cp .env.example .env
# Fill in your API keys and database config in .env

# Initialize the database
# (Add your actual DB setup command)
python setup_db.py

# Run the application
python app.py
# or
npm start
```

---

## Usage

1. Launch the application — the main window will open.
2. Log in as a **Registrar**, **Instructor**, or **Student**, or continue as a **Visitor**.
3. Navigate through the single-window GUI using the sidebar/tab navigation.
4. Use the **AI Assistant** text area (bottom of screen) to ask questions at any time.

> **Default Registrar Credentials (demo):**
> - Username: `admin`
> - Password: `changeme`

---

## Team

| Name               | Role / Responsibilities |
|--------------------|-------------------------|
| *Decong Deng*      | *Backend*               |
| *Eddie Zhu*        | *Frontend*              |
| *Gaurab Pun*       | *Backend*               |
| *Sangita Shrestha* | *Database*              |
| *Tristan Chong*    | *AI Feature*            |

---

## License

This project is developed for academic purposes as part of a Software Engineering course. All rights reserved by the project team.