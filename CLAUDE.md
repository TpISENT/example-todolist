# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a multi-user Todo List application built with Next.js. The app allows multiple users to create and manage their own todo lists. ALL instructions within this document MUST BE FOLLOWED WITHOUT EXCEPTION, THESE ARE NOT OPTIONAL. DO NOT Violate these rules, follow them exactly as is.

## IMPORTANT RULES

- No silent fallbacks that mask errors
- Explicit validation requirements
- ALWAYS fail fast if needed with clear messages
- Prioritize architecture over quick fixes
- Avoid magic values and hardcoded defaults
- ALWAYS prevent technical debt
- ALWAYS design for clarity and correctness first
- ALWAYS justify architectural decisions before implementation
- NEVER bypass TypeScript compilation or disable strict checking.
- ALWAYS enforce strict typescript checking and compilation
- ASK FOR CLARIFICATION If you are uncertain of any of thing within the document.
- DO NOT edit more code than you have to.
- DO NOT WASTE TOKENS, be succinct and concise.
- DO NOT return the code with emojies or icons
- ALWAYS return file names in lowercase using kebab-case
- ALWAYS save general documentation related ending with .md in the docs/ folder
- ALWAYS keep the root directory clean. ONLY files required to be in the root for the project must be in root
- ALWAYS Return code in plain text only.
- DO NOT return documentation with emojies or icons
- ALWAYS Return documentation in plain text only
- DO NOT include any AI-generated signatures or co-authorship references in commit messages
- DO NOT disable a feature so a test can pass
- DO NOT use emojies or icons in git commit messages.
- ALWAYS return commit messages in plain text
- DO NOT SKIP Pre-commit, pre-push and commit hooks
- ALWAYS document the conversations between you and the user in docs/scratch-pad folder inside the project directory and keep it updated
- ALWAYS write a test and run the test against your code before you commit the changes
- Its very important to keep the code structure clean and properly documented
- Code must always be written to be highly performant, highly available and highly secure
- Always follow the strict coding styles and best practices of the programming language being used
- ALWAYS document any unusual behavior, edge cases, or implementation quirks encountered during code creation
- Keep your work focused and modular to fit comfortably within the context window
- ALWAYS be granular with your to-dos. Instead of "style the navbar," do something like "change height from 60px to 80px," "reduce padding-top from 16px to 12px," "adjust background from #ffffff to rgba(255,255,255,0.95)."
- When asked to perform a task, ALWAYS PLAN and think harder before you start refactoring or writing new code
- ALWAYS Structure code into lean, focused modules that can be selectively read
- Before you commit code and push, ALWAYS check for icons and emojis in code and documentation and remove the icons and emojis.
- Before you push code, remove the Co-Authored-By line in commit messages
- ALWAYS think about potential security vulnerabilities in your code before you write and commit
- ALWAYS add JSDoc comments in your code
- If you are in doubt suggest a few ways to solve the problem and ask for my opinion.
- DON'T write code with linting errors and warnings that will fail code quality test
- ALWAYS write code that is properly linted and formatted using eslint and prettier
- ALWAYS avoid duplicate code, files and folders in nested trees
- All project related test scripts and results should ALWAYS be placed in a "test" folder

## Common Development Commands

Since this is a new project, the following commands will need to be set up:

### Initial Setup (if not already done)

```bash
npx create-next-app@latest . --typescript --tailwind --app
npm install
```

### Development

```bash
npm run dev          # Start development server on http://localhost:3000
npm run build        # Build for production
npm run start        # Start production server
npm run lint         # Run ESLint
npm run typecheck    # Run TypeScript type checking (after setup)
```

### Testing (once configured)

```bash
npm test             # Run all tests
npm run test:watch   # Run tests in watch mode
```

## Architecture & Structure

### Expected Project Structure

```text
todolist/
├── app/                    # Next.js App Router
│   ├── layout.tsx         # Root layout
│   ├── page.tsx           # Home page
│   ├── api/               # API routes
│   │   └── todos/         # Todo CRUD endpoints
│   └── [userId]/          # Dynamic user routes
│       └── todos/         # User-specific todo pages
├── components/            # React components
│   ├── TodoList.tsx      # Todo list display
│   ├── TodoItem.tsx      # Individual todo item
│   └── AddTodo.tsx       # Add new todo form
├── lib/                  # Utilities and shared code
│   ├── db.ts            # Database connection
│   └── types.ts         # TypeScript types
└── prisma/              # Database schema (if using Prisma)
    └── schema.prisma    # Database models
```

### Key Technical Decisions

1. **Framework**: Next.js 14+ with App Router
2. **Styling**: Tailwind CSS for rapid UI development
3. **Database**: Consider SQLite for development, PostgreSQL for production
4. **Authentication**: NextAuth.js for multi-user support
5. **State Management**: React Server Components with client-side hooks
6. **Type Safety**: TypeScript throughout

### Development Guidelines

1. **Component Structure**: Keep components small and focused. Use server components by default, client components only when needed.

2. **API Design**: RESTful endpoints under `/api/todos` with proper HTTP methods:
   - GET /api/todos - List todos for authenticated user
   - POST /api/todos - Create new todo
   - PUT /api/todos/[id] - Update todo
   - DELETE /api/todos/[id] - Delete todo

3. **Database Schema**: Basic todo structure should include:
   - id (unique identifier)
   - userId (for multi-user support)
   - title (todo text)
   - completed (boolean)
   - createdAt/updatedAt timestamps

4. **Authentication Flow**:
   - Use middleware to protect todo routes
   - Each user can only access their own todos
   - Consider session-based auth for simplicity

5. **Error Handling**: Implement proper error boundaries and loading states

## Code Style

- Use ES modules (import/export) syntax, not CommonJS
- Destructure imports when possible
- Follow Next.js naming conventions (page.tsx, layout.tsx, etc.)
- Use async/await over promises
- Implement proper TypeScript types for all data structures

## Testing Strategy

When tests are implemented:

- Unit tests for utility functions
- Integration tests for API routes
- Component tests for interactive elements
- End-to-end tests for critical user flows
