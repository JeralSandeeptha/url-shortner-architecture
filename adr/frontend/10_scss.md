# ADR 10: Use SCSS for Supplemental Styling

## Status
Accepted

## Context
While Tailwind CSS serves as the primary styling framework for our frontend applications (see ADR 12), there are certain use cases where SCSS (Sass) provides additional flexibility and maintainability.

These use cases include:
- Complex or reusable styles that would result in overly verbose Tailwind class structures.
- Fine-tuned styling for specific third-party components or legacy UI parts not easily adapted to Tailwind utilities.
- Use of CSS features like nesting, variables, mixins, or functions for modular design patterns.
- Situations where component styles need to be maintained separately for readability or easier overrides.

The secondary use of SCSS aims to complement Tailwind CSS, not replace it. It provides a balance between utility-first styling and structured, maintainable CSS for special scenarios.

## Decision
We will adopt SCSS as a secondary styling mechanism for cases where Tailwind utilities are insufficient, inefficient, or reduce code clarity.

Implementation guidelines:

Tailwind CSS remains the default choice for most styling needs.
- SCSS should be used selectively for:
  - Complex component layouts or animations not easily handled by Tailwind.
  - Styling legacy components during gradual migration to Tailwind.
  - Global or theme-level overrides (e.g., scrollbar styles, external component tweaks).
- SCSS files will be co-located with their respective components using a .module.scss naming convention to avoid global scope pollution.
- Shared SCSS utilities (variables, mixins, etc.) can be defined in a centralized styles/ directory.

The build pipeline will continue to use PostCSS, which integrates with Sass via the existing React/Next.js configuration.

## Consequences
Positive
- `Flexibility`: Allows fine-grained control for styles that are hard to express with Tailwind utilities.
- `Improved readability`: Keeps JSX cleaner in complex UI components by moving intricate styling logic to SCSS files.
- `Ease of transition`: Supports a gradual migration from legacy CSS/SCSS to Tailwind without breaking existing designs.
- `Powerful features`: SCSS variables, nesting, and mixins improve maintainability for custom or complex styles.

Negative
- `Increased complexity`: Having two styling approaches may confuse developers if not clearly documented.
- `Maintenance overhead`: Styles spread across Tailwind utilities and SCSS files require discipline to maintain consistency.
- `Potential duplication`: Some design tokens (e.g., colors, spacing) may need to be defined both in Tailwind config and SCSS variables if not properly synchronized.

## Alternatives Considered (optional)
`Using only Tailwind CSS`: Simplifies the stack but makes certain complex styling patterns verbose or impractical.
`Using only SCSS`: Offers full control but lacks the rapid, consistent utility-first approach provided by Tailwind.
`CSS-in-JS (Styled Components, Emotion)`: Provides component scoping and dynamic styling but introduces runtime overhead and larger bundles.

## Date
2025-11-11

## Authors / Reviewers
Frontend Team Lead
UI/UX Designer
Software Architect