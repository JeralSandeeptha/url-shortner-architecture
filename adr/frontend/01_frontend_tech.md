# ADR 01: Use React as the Frontend Technology

## Status
Accepted

## Context
We needed to choose a frontend technology for a web application that is dashboard-heavy, interactive, and requires real-time updates. Key requirements included:
  - Single Page Application (SPA) for a fast and responsive user experience.
  - Integration with APIs for dynamic data handling.
  - SEO considerations only for landing pages, not the full application.
  - Dashboard-heavy, interactive components with frequent updates.

The team wanted a frontend technology that is `modern`, `widely adopted`, and has `strong community support` for building rich web interfaces.

## Decision
We use monolith architecturehave for frontend. We are excepting as frontend service, it should be fast, SPA application, real time updates, dashboard heavy and interactive. We are building this as a Web Application. Most of the times are try to use APIs. We are targeting SEO part only for the landing pages. Others are Web application parts / Dashboard. So we don't need Nextjs. That's why we are proceeding with the Reactjs with Vite.

## Consequences

Positive:
  - React with Vite provides fast development setup and hot module replacement for quick iteration.
  - SPA architecture ensures a smooth and responsive user experience for dashboard-heavy interactions.
  - Easy integration with APIs and WebSockets for real-time updates.
  - Strong ecosystem and community support for libraries, tools, and best practices.

Negative:
  - SEO will be limited to landing pages, other parts of the application may not be crawlable without additional effort.
  - Requires client-side rendering, which could increase initial load time for users with slow connections.
  - Some learning curve for developers unfamiliar with React or Vite.

## Alternatives Considered (optional)
- `Next.js` – Rejected because full server-side rendering (SSR) and SEO were unnecessary for the dashboard-heavy parts. only landing pages required SEO.
- `Angular` – Considered but found heavier in terms of setup and boilerplate for SPA dashboards.
- `Vue.js` – Lightweight and flexible, but the team had more experience with React and preferred its ecosystem for complex state management in dashboards.

## Date
2025-10-19

## Authors / Reviewers
Backend Team Lead
Software Architect
Senior Frontend Developer