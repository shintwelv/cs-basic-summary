# Agent Guidelines: CS-Basic-Summary

This document provides essential information for AI agents contributing to or maintaining this repository.

## Project Overview
- **Objective**: Summarize Computer Science fundamentals at an undergraduate level.
- **Primary Audience**: Students preparing for exams or technical interviews.
- **Source Management**: Content is primarily managed via **Obsidian** (Markdown).
- **Web Hosting**: Real-time rendering via **Docsify** on **GitHub Pages**.

## Tech Stack & Configuration
- **Docsify**: `index.html` acts as the entry point. It fetches `.md` files asynchronously.
- **Sidebar**: Manual navigation is managed in `_sidebar.md`.
- **Styling**: Custom CSS embedded in `index.html` follows a dark, modern blue/slate theme.
- **GitHub Pages**: Requires a `.nojekyll` file in the root to bypass Jekyll processing and serve files correctly.

## Directory Structure
- `/operating-system/`: OS concepts (Process, Deadlock, Scheduling, Memory).
- `/network/`: Networking protocols (OSI, TCP/UDP, HTTP).
- `/database/`: DB design and performance (SQL/NoSQL, Index, ACID).
- `/data-structure/`: Logical data arrangements (Stack, Queue, Tree).
- `/algorithm/`: Problem-solving patterns (Sort, Search, DP).

## Content Guidelines
When editing or creating new Markdown files, follow these rules:

1. **Obsidian Compatibility**: Use **Callouts** for Q&A sections.
2. **Technical Precision**: 
    - Always differentiate between Single-core (Time-sharing) and Multi-core (Parallelism) when discussing multitasking.
    - Include low-level details where applicable (e.g., PCB/TCB in context switches, Stack/Register/PC in thread contexts).
3. **Language**: Use Korean for the content (unless requested otherwise), but internal documentation (like this file) should be in English.
4. **Markdown Formatting**: Use standard GFM (GitHub Flavored Markdown) with clear hierarchies (`#`, `##`, `###`).

## Maintenance Tasks
- **Updating Sidebar**: When adding a new file or directory, ensure the link is added to `_sidebar.md`.
- **Docsify Theme**: If styles are updated, ensure they are compatible with Docsify's internal structure (e.g., `.markdown-section`).
- **Static Assets**: Avoid large binaries. Use externally hosted images or generated icons where possible.

---
*Last Updated: 2026-04-07*
