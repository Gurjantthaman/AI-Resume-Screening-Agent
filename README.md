# AI Resume Screening Agent

An AI-powered recruitment productivity agent built with n8n and Google Gemini that automates the first stage of candidate resume screening.

The agent compares a candidate's resume against a specific job description, evaluates skills and relevant experience, produces an explainable match score, and routes the candidate into a screening category.

## Problem

Recruiters often spend significant time manually reviewing resumes and comparing candidates against job requirements.

The repetitive process typically involves:

1. Reading the candidate's resume.
2. Understanding the job requirements.
3. Comparing skills and experience.
4. Identifying missing requirements.
5. Deciding whether the candidate should be shortlisted or reviewed further.

This project automates that first-level screening process while keeping a human involved for uncertain cases.

## Solution

The AI Resume Screening Agent takes a candidate resume and the job they applied for as input.

It then:

- Extracts information from the resume.
- Retrieves the corresponding job requirements.
- Analyzes the candidate's skills and experience.
- Compares the candidate against the job requirements.
- Produces an explainable match score.
- Identifies matching and missing skills.
- Provides evidence supporting its assessment.
- Assigns a confidence level.
- Makes a recommendation.
- Routes the candidate to the appropriate screening queue.

## Architecture

```text
                    JOB INTAKE
                         │
                    Job Form/Sheet
                         │
                    Generate Job ID
                         │
                    Job Database
                         │
                         │
                         ▼
                CANDIDATE SCREENING
                         │
                  Candidate Resume
                         │
                  Google Sheets Trigger
                         │
                    Download PDF
                         │
                   Extract PDF Text
                         │
                         ▼
                Get Job Requirements
                         │
                         ▼
                  ┌───────────────┐
                  │   AI AGENT    │
                  │               │
                  │ Resume        │
                  │ Analysis      │
                  │ Skill Match   │
                  │ Experience    │
                  │ Scoring       │
                  │ Recommendation│
                  └───────┬───────┘
                          │
                    Gemini Model
                          │
                          ▼
                    Clean JSON
                          │
                          ▼
              Combine Candidate Data
                          │
                          ▼
                       Switch
                   /      |       \
                  /       |        \
                 ▼        ▼         ▼
             Strong    Human      Low
             Match     Review     Match
               │         │          │
               ▼         ▼          ▼
           Strong      Review       Low
           Matches     Queue       Matches
