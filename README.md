<div align="center">

# 🤖 HireLens

### AI-Powered Recruitment & Job Application Platform

**CV analysis · Job matching · ATS auditing · Interview preparation · Application tracking**

<p>
  <a href="https://hirelens-alpha.vercel.app">
    <img src="https://img.shields.io/badge/Live_Demo-2563EB?style=for-the-badge&logo=vercel&logoColor=white" />
  </a>
  <a href="https://github.com/azim-haffar/HireLens">
    <img src="https://img.shields.io/badge/Repository-181717?style=for-the-badge&logo=github&logoColor=white" />
  </a>
</p>

<p>
  <img src="https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/FastAPI-0.111-009688?style=flat-square&logo=fastapi&logoColor=white" />
  <img src="https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=111827" />
  <img src="https://img.shields.io/badge/Vite-5-646CFF?style=flat-square&logo=vite&logoColor=white" />
  <img src="https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?style=flat-square&logo=supabase&logoColor=white" />
  <img src="https://img.shields.io/badge/Redis-7-DC382D?style=flat-square&logo=redis&logoColor=white" />
  <img src="https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/License-MIT-16A34A?style=flat-square" />
</p>

</div>

---

## Overview

**HireLens** is a full-stack recruitment platform that helps job seekers understand how well their CV matches a specific vacancy and identify areas they can improve.

Users can upload a PDF CV, paste or ingest a job posting, and receive structured analysis across skills, experience, education, and keyword coverage.

The platform also includes:

- weighted CV-to-job match scoring
- AI-generated match explanations
- ATS auditing
- CV comparison
- interview preparation
- cover-letter generation
- application tracking
- analysis history
- multilingual support
- contextual AI chat

The application combines a **React frontend**, **FastAPI backend**, **Supabase / PostgreSQL**, **Redis**, and **Groq-hosted LLMs**, with public deployment through **Vercel and Render**.

---

## 📸 Screenshots

<table>
<tr>
<td width="50%" valign="top">

### Landing

<img src="screenshots/landing.png" alt="HireLens landing page" />

</td>
<td width="50%" valign="top">

### Dashboard

<img src="screenshots/dashboard.png" alt="HireLens dashboard" />

</td>
</tr>

<tr>
<td width="50%" valign="top">

### Job Analysis

<img src="screenshots/analysis.png" alt="HireLens CV and job analysis" />

</td>
<td width="50%" valign="top">

### ATS Checker

<img src="screenshots/ats-checker.png" alt="HireLens ATS checker" />

</td>
</tr>
</table>

<div align="center">

### Roast My CV

<img src="screenshots/roast.png" width="80%" alt="HireLens Roast My CV page" />

</div>

---

## ✨ Core Features

<table>
<tr>
<td width="50%" valign="top">

### 📄 CV & Job Analysis

- PDF CV upload and parsing
- Job description ingestion
- Job URL scraping
- Structured CV/job extraction
- Weighted match scoring
- Skills and keyword coverage
- Education and experience analysis

</td>

<td width="50%" valign="top">

### 🎯 Application Support

- ATS compliance audit
- Role-specific interview questions
- STAR answer frameworks
- Tailored cover-letter generation
- CV-to-CV comparison
- Analysis history and trends

</td>
</tr>

<tr>
<td width="50%" valign="top">

### 📋 Job Tracking

- Drag-and-drop Kanban board
- Saved
- Applied
- Interview
- Offer
- Rejected
- Ghosted

</td>

<td width="50%" valign="top">

### 🤖 AI Features

- SSE-streamed explanations
- Contextual AI chat
- Public CV feedback endpoint
- Multi-model fallback
- Structured LLM outputs
- Rate-limited public features

</td>
</tr>
</table>

---

## 🧠 Match Scoring

HireLens calculates a weighted CV-to-job match score using four categories:

| Category | Weight |
|---|---:|
| Skills | **35%** |
| Experience | **25%** |
| Education | **15%** |
| Keywords | **25%** |

The numerical score is generated from the weighted analysis, while a detailed explanation is generated separately and streamed to the frontend using **Server-Sent Events (SSE)**.

This separates the structured scoring logic from the natural-language explanation shown to the user.

---

## 🏗️ Architecture

```mermaid
flowchart LR

    U[User]

    subgraph Frontend
        R[React 18]
        V[Vite]
        T[Tailwind CSS]
    end

    subgraph Backend
        F[FastAPI]
        P[PDF Parsing]
        S[Job Scraping]
        RL[Rate Limiting]
    end

    subgraph Data
        SB[(Supabase PostgreSQL)]
        AU[Supabase Auth]
        RD[(Redis)]
    end

    subgraph AI
        G[Groq API]
        M1[LLaMA 3.3 70B]
        M2[LLaMA 3 8B]
        M3[LLaMA 3.1 8B]
    end

    U --> R
    R -->|HTTP / SSE| F

    F --> P
    F --> S
    F --> RL

    F --> SB
    F --> AU
    F --> RD

    F --> G

    G --> M1
    M1 -. fallback .-> M2
    M2 -. fallback .-> M3
