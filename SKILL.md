---
name: resume-optimizer
description: >
  Optimize, rewrite, and tailor resumes for specific job applications using AI-driven analysis.
  Use this skill whenever a user wants to improve their resume, tailor it to a job description,
  check ATS compatibility, strengthen bullet points, fix formatting, or get feedback on their CV.
  Trigger on phrases like: "improve my resume", "tailor my resume for this job", "make my resume
  ATS-friendly", "rewrite my resume bullets", "review my CV", "help me apply for [role]",
  "optimize my resume for [company]", or any request where a resume file or resume content is
  present alongside a job description or job title. Always use this skill when both a resume and
  a job context are present — even if the user just says "can you help with this?".
---

# Resume Optimizer Skill

A structured, step-by-step workflow for analyzing and optimizing resumes for job applications.
Covers ATS optimization, bullet point rewriting, tailoring for specific roles, and final QA.

---

## When to Use This Skill

- User uploads or pastes a resume (in any format: PDF, DOCX, plain text)
- User mentions a target job title, company, or pastes a job description (JD)
- User asks for resume feedback, improvement, or rewriting
- User wants to know if their resume will pass ATS screening
- User is preparing for job applications as a student, fresher, or experienced professional

---

## Workflow Overview

```
Step 1: Ingest & Parse
Step 2: Understand Target Role
Step 3: ATS & Keyword Gap Analysis
Step 4: Bullet Point Rewriting
Step 5: Structure & Formatting Review
Step 6: Tailored Resume Output
Step 7: Final QA Checklist
```

Work through each step sequentially. Do **not** skip steps — each builds on the previous.

---

## Step 1: Ingest & Parse the Resume

### If a file is uploaded:
```bash
# For PDF
python -m markitdown /mnt/user-data/uploads/<filename>.pdf

# For DOCX
python -m markitdown /mnt/user-data/uploads/<filename>.docx
```

Extract and mentally note the following sections:
- **Contact info** (name, email, phone, LinkedIn, GitHub, location)
- **Summary / Objective** (if present)
- **Education** (degrees, institutions, graduation years, GPA if listed)
- **Work Experience / Internships** (company, role, dates, bullet points)
- **Projects** (title, tech stack, description)
- **Skills** (technical + soft)
- **Certifications / Achievements / Awards**
- **Extracurriculars / Leadership** (especially for students/freshers)

### If resume is pasted as text:
Parse directly from the conversation. Identify the same sections above.

### Flag Missing Sections
Note any sections that are absent but should be present for the target role.

---

## Step 2: Understand the Target Role

Ask the user (if not already provided):
1. **Job Title** — What role are they applying for?
2. **Company** — Specific company or type of company (startup, MNC, FAANG, etc.)?
3. **Job Description** — Do they have a JD to paste? If yes, extract:
   - Required skills and tools
   - Preferred qualifications
   - Key responsibilities
   - Recurring keywords and phrases (these are ATS signals)
4. **Experience Level** — Fresher / Student / 1–3 years / Experienced?
5. **Industry** — Software Engineering, Data Science, Cybersecurity, AI/ML, etc.?

If no JD is provided, use the job title + industry to infer likely requirements from common knowledge.

---

## Step 3: ATS & Keyword Gap Analysis

### What is ATS?
Applicant Tracking Systems scan resumes before a human ever reads them. Resumes are scored
on keyword matches with the job description. Failing ATS = never reaching a recruiter.

### Perform Gap Analysis:

1. **Extract JD Keywords**: Pull all technical skills, tools, frameworks, methodologies, and
   role-specific verbs from the job description.

2. **Cross-Reference Resume**: Check which JD keywords appear in the resume and which are missing.

3. **Score Estimate**: Estimate a rough ATS match score:
   - >80% keyword match = Strong
   - 60–80% = Moderate (needs improvement)
   - <60% = Weak (needs significant tailoring)

4. **Output a Gap Table**:

| JD Keyword | In Resume? | Where / Fix |
|------------|------------|-------------|
| Python     | ✅ Yes     | Skills section |
| REST APIs  | ❌ Missing | Add to Project X description |
| Agile/Scrum| ❌ Missing | Add to internship bullets |
| SQL        | ✅ Yes     | Skills + Projects |

5. **Flag Formatting ATS Killers**:
   - Tables, columns, text boxes, headers/footers → ATS can't parse these
   - Images, graphics, charts → Strip them
   - Non-standard section titles (e.g., "My Journey" instead of "Experience") → Rename
   - Fancy fonts or icons in contact info → Simplify

---

## Step 4: Bullet Point Rewriting

This is the highest-impact step. Weak bullets are the #1 reason good candidates get rejected.

### The STAR-CAR Framework for Bullets

Every bullet should ideally contain:
- **Action verb** (strong, specific)
- **Task / What you did**
- **Result / Impact** (quantified where possible)

**Formula**: `[Strong Verb] + [What You Did] + [By How Much / With What Result]`

### Strong Action Verbs by Category

| Category | Verbs |
|----------|-------|
| Built / Developed | Engineered, Developed, Architected, Implemented, Deployed, Automated |
| Improved | Optimized, Reduced, Accelerated, Streamlined, Enhanced, Refactored |
| Led | Spearheaded, Led, Coordinated, Mentored, Drove, Oversaw |
| Analysed | Analysed, Evaluated, Diagnosed, Investigated, Modelled, Assessed |
| Designed | Designed, Prototyped, Conceptualized, Formulated, Mapped |

**Avoid weak openers**: "Responsible for", "Worked on", "Helped with", "Assisted in"

### Quantification Heuristics (for students/freshers with limited metrics)

If exact numbers aren't known, use reasonable estimates or relative impact:
- Lines of code → "Built a 2,000+ line Python application..."
- Users → "Deployed to 200+ college students..."
- Time saved → "Automated a manual process, reducing report generation from 2 hours to 5 minutes"
- Performance → "Improved query response time by ~40% through indexing"
- Academic → "Achieved top 5% grade in Advanced Algorithms coursework"

### Before / After Examples

**Weak**: "Worked on a web app for managing library books"
**Strong**: "Engineered a full-stack library management system using React and Node.js, reducing
book search time by 60% and handling 500+ concurrent users in production"

**Weak**: "Did data analysis for a project"
**Strong**: "Analysed 50,000+ rows of sales data using Python (Pandas, Matplotlib) to identify
seasonal trends, contributing to a 15% inventory optimization recommendation"

### Rewrite Process

For each bullet in the resume:
1. Identify the weak pattern
2. Ask: What technology? What scale? What outcome?
3. Rewrite using the formula above
4. Ensure relevant JD keywords are naturally woven in

---

## Step 5: Structure & Formatting Review

### Recommended Resume Structure (by experience level)

**Fresher / Student (0–1 year)**:
```
1. Contact Info
2. Summary / Objective (2–3 lines, role-targeted)
3. Education (prominent — GPA, relevant coursework, awards)
4. Projects (3–5, most relevant first)
5. Internships / Work Experience (if any)
6. Skills (Technical > Tools > Soft Skills)
7. Certifications & Courses
8. Extracurriculars / Leadership
```

**Experienced (2+ years)**:
```
1. Contact Info
2. Professional Summary (3–4 lines)
3. Work Experience (reverse chronological)
4. Skills
5. Projects (if relevant)
6. Education
7. Certifications
```

### Formatting Rules
- **Length**: 1 page for freshers/students. 2 pages max for 5+ years experience.
- **Font**: Calibri, Arial, or Georgia. Size 10–12pt body, 14–16pt name.
- **Margins**: 0.5"–1" all sides.
- **File format**: PDF (preserves formatting, ATS-safe).
- **File name**: `FirstName_LastName_Resume.pdf` — never "resume_final_v3_LATEST.pdf"
- **No photos** for US/UK/India tech roles (standard practice).
- **Consistent date format**: Use "Month Year" or "MM/YYYY" throughout.
- **Hyperlinks**: LinkedIn URL, GitHub URL, and portfolio should be clickable.

---

## Step 6: Tailored Resume Output

After analysis, produce one of the following based on what the user needs:

### Option A: Annotated Feedback Report
If the user wants suggestions without full rewrite — provide:
- ATS gap table (Step 3 output)
- List of bullets to rewrite with before/after suggestions
- Structure/formatting notes
- Summary score and priority fixes

### Option B: Full Rewritten Resume (as DOCX)
If the user wants a complete rewrite, follow the DOCX skill to produce a polished file.

Read the DOCX skill before creating:
```
/mnt/skills/public/docx/SKILL.md
```

**Key output requirements**:
- Clean, ATS-safe single-column layout
- All JD keywords naturally incorporated
- All bullets rewritten using STAR-CAR framework
- Consistent formatting throughout
- Saved as: `FirstName_LastName_Resume_[Role].docx`

### Option C: Targeted Summary / Cover Letter Snippet
If the user wants just their summary/objective rewritten for a specific role — output 3–4 lines
that mirror the JD's language, highlight their top 2–3 relevant strengths, and name the role explicitly.

---

## Step 7: Final QA Checklist

Before presenting the output, verify each item:

**Content**
- [ ] All JD keywords incorporated naturally (not keyword-stuffed)
- [ ] Every bullet starts with a strong action verb
- [ ] At least 60% of bullets have a quantified result
- [ ] No spelling or grammar errors
- [ ] Contact info complete and accurate
- [ ] Dates are consistent and in correct order (reverse chronological)
- [ ] No unexplained gaps in timeline

**ATS Safety**
- [ ] No tables, text boxes, or multi-column layouts
- [ ] No graphics or images embedded in resume body
- [ ] Section headers use standard titles (Education, Experience, Skills, etc.)
- [ ] Saved as PDF with selectable text (not scanned image)

**Formatting**
- [ ] 1 page (fresher) or ≤2 pages (experienced)
- [ ] Font size 10–12pt throughout (name 14–16pt)
- [ ] Consistent spacing and alignment
- [ ] File named correctly

**Tailoring**
- [ ] Summary/objective mentions the specific role
- [ ] Most relevant experience and projects listed first
- [ ] Skills section matches JD requirements

---

## Special Guidance: Engineering Freshers & Students

This skill is optimized for engineering undergraduates in India applying to tech roles. Key tips:

**Projects matter most** — For freshers, projects ARE the experience. Dedicate significant
space (3–5 projects) and treat each like a job role with strong bullets.

**Tech stack visibility** — Always name exact technologies: not "built a web app" but
"built using React.js, Node.js, MongoDB, deployed on AWS EC2".

**Competitive programming / DSA** — Include LeetCode/CodeChef/Codeforces ratings if strong
(e.g., "LeetCode: 1800+ rating, 300+ problems solved"). Signals problem-solving ability.

**CGPA** — Include if 7.5+ out of 10 (or equivalent). If lower, consider omitting.

**Company-specific tailoring**:
- **Mass recruiters (TCS, Infosys, Wipro)**: Emphasize teamwork, communication, adaptability
- **Product companies (Zomato, Swiggy, CRED, Razorpay)**: Emphasize impact, scale, ownership
- **FAANG / Google / Microsoft**: Emphasize DSA, system design keywords, project scale
- **Startups**: Emphasize initiative, full-stack breadth, learning agility

---

## Quick Reference: Common Mistakes to Fix

| Mistake | Fix |
|---------|-----|
| "Responsible for developing..." | "Developed..." |
| Generic objective ("seeking a challenging role") | Role-specific: "Seeking SDE Intern role at [Company] to apply ML expertise in NLP pipelines" |
| Listed skills without context | Show skills *used* in project bullets |
| Projects without outcomes | Add metrics, users, performance improvements |
| No GitHub / Portfolio link | Add clickable links |
| One resume for all applications | Tailor for each role / company type |
| Education listed last (fresher) | Move education to top |
| Unexplained 6-month gap | Add any relevant learning, freelance, or personal project |
