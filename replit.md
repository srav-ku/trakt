# Employee Task Tracker

## Overview

The Employee Task Tracker is a fullstack web application designed as an internal tool for managing employee tasks within a company. It provides a clean, productivity-focused interface for tracking task assignments, status updates, and employee workloads.

**Tech Stack:**
- **Frontend:** React with TypeScript, Wouter (routing), TanStack Query (data fetching)
- **UI Framework:** Shadcn UI components with Tailwind CSS
- **Backend:** Express.js with TypeScript
- **Database:** SQLite with better-sqlite3
- **ORM:** Drizzle ORM
- **Build:** Vite (frontend), esbuild (backend)

**Purpose:** Enable small to medium-sized companies to efficiently manage and track employee task assignments with a modern, intuitive interface.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Component Strategy:**
- Utilizes Shadcn UI's "New York" variant for a modern, professional aesthetic
- Component-based architecture with React functional components and hooks
- Atomic design pattern with reusable UI primitives in `/client/src/components/ui`

**Routing:**
- Uses Wouter for lightweight client-side routing
- Three main routes: Dashboard (`/`), Employees (`/employees`), Tasks (`/tasks`)
- Sidebar navigation with active route highlighting

**State Management:**
- TanStack Query (React Query) for server state management
- Custom query client configured with specific refetch behaviors
- Local component state via React hooks

**Styling Approach:**
- Tailwind CSS utility-first approach
- CSS custom properties for theming (supports light/dark modes)
- Design system with defined spacing scale (2, 3, 4, 6, 8, 12, 16)
- Typography using Inter font family with System UI fallback
- Consistent border radius: lg (9px), md (6px), sm (3px)

**Design Philosophy:**
- Inspired by Linear, Notion, and Asana's clean, functional interfaces
- Professional and efficiency-focused with reduced cognitive load
- Material Design principles with productivity-focused adaptations

### Backend Architecture

**API Structure:**
- RESTful API design with Express.js
- Route registration in `/server/routes.ts`
- API endpoints prefixed with `/api`
- Health check endpoint at `/api/health`

**Data Access Layer:**
- Storage abstraction through `IStorage` interface in `/server/storage.ts`
- `SQLiteStorage` implementation provides CRUD operations for employees and tasks
- Methods for complex queries like dashboard statistics and filtered task retrieval

**Database Design:**
- Two main tables: `employees` and `tasks`
- Foreign key relationship: tasks.employee_id → employees.id with CASCADE delete
- Indexes on frequently queried fields (email, department, status, due_date)
- Schema defined in `/shared/schema.ts` using Drizzle ORM

**Data Validation:**
- Zod schemas for runtime validation
- Schema generation from Drizzle tables using `drizzle-zod`
- Validation at API endpoint level before database operations

**Request Processing:**
- JSON body parsing with raw body preservation for webhooks
- URL-encoded form data support
- Logging middleware tracking request duration and responses
- Error handling with appropriate HTTP status codes

### Database Schema

**Employees Table:**
- `id` (auto-increment primary key)
- `name`, `email` (unique), `department`, `position`
- `created_at` (timestamp)

**Tasks Table:**
- `id` (auto-increment primary key)
- `title`, `description`, `status` (enum: pending, in-progress, completed)
- `employee_id` (foreign key to employees)
- `due_date`, `priority` (enum: low, medium, high)
- `created_at`, `updated_at` (timestamps)

**Rationale for SQLite:**
- Zero configuration - no separate database server required
- Single file database perfect for edge deployments (Cloudflare, Vercel)
- Sufficient performance for small-medium company workloads
- Easy backup and version control
- Faster development iteration

### Development Workflow

**Build Process:**
- Client builds via Vite with React plugin
- Server bundles with esbuild, selective dependency bundling for cold start optimization
- Development mode uses Vite middleware for HMR
- Production serves static files from Express

**Development Mode:**
- Hot Module Replacement (HMR) via Vite
- TypeScript checking without emit
- Source map support for debugging
- Replit-specific plugins for error overlays and dev banners

**Database Management:**
- Automatic migrations on server start via `runMigrations()`
- Seed data insertion for development (`seedDatabase()`)
- Drizzle Kit for schema management and migrations

### Static File Serving

**Production:**
- Express serves static assets from `dist/public`
- SPA fallback to `index.html` for client-side routing
- Build validation ensures dist directory exists

## External Dependencies

### Core Framework Dependencies

**Frontend:**
- `react`, `react-dom` - UI framework
- `wouter` - Lightweight routing
- `@tanstack/react-query` - Server state management
- `vite` - Build tool and dev server
- `@vitejs/plugin-react` - React integration for Vite

**Backend:**
- `express` - Web server framework
- `better-sqlite3` - SQLite database driver
- `drizzle-orm` - TypeScript ORM
- `tsx` - TypeScript execution for development

### UI Component Library

**Shadcn UI (Radix-based):**
- `@radix-ui/*` - Primitive components (dialog, dropdown, select, etc.)
- `class-variance-authority` - Component variant utilities
- `tailwind-merge`, `clsx` - Conditional class management
- `lucide-react` - Icon library

### Validation & Forms

- `zod` - Schema validation
- `drizzle-zod` - Schema generation from Drizzle tables
- `react-hook-form` - Form state management
- `@hookform/resolvers` - Zod integration with react-hook-form

### Styling

- `tailwindcss` - Utility-first CSS framework
- `autoprefixer` - CSS vendor prefixing
- `postcss` - CSS transformation

### Development Tools

- `typescript` - Type checking
- `@types/*` - Type definitions
- `@replit/*` - Replit-specific development plugins
- `drizzle-kit` - Database migration CLI

### Database Note

The application currently uses better-sqlite3 for local SQLite databases. The presence of `@neondatabase/serverless` and PostgreSQL configuration in `drizzle.config.ts` suggests potential support for PostgreSQL deployment (likely Neon) in production environments. The storage layer is abstracted to allow switching between database implementations.