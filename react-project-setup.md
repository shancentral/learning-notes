1. I need to create a Project with Vite + React + Typescript + React Router + Zustand + Tanstack Query + Material UI + Tailwind CSS + Vitest.
2. Use Material UI only for Components and use Tailwind CSS for Layouts, Grids and all other CSS Utility classes.
3. NEVER use `sx` for Material UI & inline styles.
4. ALWAYS prefer SCSS over CSS.
5. ALWAYS obey DRY and SOLID patterns when generating code.
6. ALWAYS use fetch for API calls.
7. PREFER feature based organisation over technical organisation. Shared code MUST ONLY exist in shared folder.
8. ALWAYS use Light theme background and Maintain good color contrast ratio.
9. ALWAYS follow Modern and Enterprise grade UX guidelines when creating Layouts & Components.
10. Never run any tests, accessibility checks, linting unless requested.
11. Use pnpm for Package Management

Based on the above requirements create necessary Agents, Skills & AGENT.md files. Additionally make sure to create separate Agents and their required Skills for Testing, Accessibility validation & Linting. Place the Agents & Skill files in an optimal folder location to work seamlessly with Github Copilot.

Create 3 pages as follows:

1. Login Page: Public route. Show page heading and a button to toggle between login & logout states.
2. Data Explorer Page: Protected route. Only show page heading.
3. Data Table Page: Protected route. Only show page heading.
