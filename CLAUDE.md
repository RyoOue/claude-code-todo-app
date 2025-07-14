# Todo App Project Context

## Tech Stack

- **Framework**: React Router v7 (Remix framework)
- **Language**: TypeScript 5.x with strict mode
- **Database**: SQLite with Drizzle ORM
- **Styling**: Tailwind CSS 3.x
- **Testing**: Vitest for unit tests, Playwright for E2E tests
- **Runtime**: Cloudflare Workers (edge runtime)
- **Package Manager**: npm

## Project Structure

- `/app`: React Router v7 application code
  - `/routes`: Route components and loaders
  - `/components`: Reusable React components
  - `/lib`: Utilities and shared logic
  - `/db`: Database schema and queries
- `/tests`: Test files
  - `/unit`: Vitest unit tests
  - `/e2e`: Playwright E2E tests
- `/public`: Static assets
- `/functions`: Cloudflare Workers functions

## Commands

- `npm run dev`: Start development server with Vite
- `npm run build`: Build for production
- `npm run preview`: Preview production build locally
- `npm run test`: Run Vitest unit tests
- `npm run test:e2e`: Run Playwright E2E tests
- `npm run typecheck`: Run TypeScript type checking
- `npm run lint`: Run ESLint
- `npm run deploy`: Deploy to Cloudflare Workers

## Database Schema

```sql
-- todos table
CREATE TABLE todos (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  description TEXT,
  completed BOOLEAN DEFAULT FALSE,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- categories table (future feature)
CREATE TABLE categories (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL UNIQUE,
  color TEXT
);
```

## Code Style

- Use functional components with TypeScript
- Prefer named exports over default exports
- Use Remix conventions for data loading (loaders/actions)
- Follow React Router v7 file-based routing
- Use Drizzle ORM for type-safe database queries
- Implement optimistic UI updates
- Use Tailwind CSS utility classes

## Testing Requirements

- Unit test all utility functions with Vitest
- Test React components with Testing Library
- E2E test critical user flows with Playwright
- Maintain >80% code coverage for utilities
- Test database queries with in-memory SQLite

## Cloudflare Workers Configuration

- Use D1 for SQLite database
- Environment variables stored in wrangler.toml
- Use Cloudflare KV for session storage
- Enable Web Analytics
- Configure custom domains via Cloudflare

## Git Workflow

- Main branch: `main` (production)
- Feature branches: `feature/description`
- Commit format: `type: description` (feat, fix, docs, test, refactor)
- PR required for main branch
- Run tests before committing

## Security Guidelines

- Validate all user inputs
- Use prepared statements for database queries
- Implement CSRF protection
- Sanitize HTML content
- Use secure session cookies
- Never expose database credentials

## Performance Guidelines

- Implement route-level code splitting
- Use React Router's defer for non-critical data
- Optimize database queries with indexes
- Cache static assets on Cloudflare CDN
- Lazy load components when appropriate

## Do Not

- DO NOT use class components
- DO NOT access database directly from components
- DO NOT store sensitive data in localStorage
- DO NOT use any or ts-ignore without justification
- DO NOT commit .env files or secrets
- DO NOT use deprecated React Router APIs

## API Conventions

- RESTful routes via React Router actions
- Return proper HTTP status codes
- Use consistent error response format
- Implement request validation
- Document API responses with TypeScript types

## Deployment Process

1. Run tests locally
2. Build production bundle
3. Deploy to Cloudflare Workers staging
4. Run E2E tests against staging
5. Deploy to production via wrangler

## Environment Variables

- `DATABASE_URL`: D1 database binding
- `SESSION_SECRET`: For cookie signing
- `NODE_ENV`: development | production
- `PUBLIC_APP_URL`: Application URL

## Development Setup

1. Install dependencies: `npm install`
2. Initialize D1 database: `npx wrangler d1 create todos-db`
3. Run migrations: `npm run db:migrate`
4. Start dev server: `npm run dev`

## Task Completion Guidelines

- Run typecheck and lint after completing tasks and be sure they ALWAYS pass