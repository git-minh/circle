# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Circle is a Linear-inspired project management interface built with Next.js, TypeScript, and shadcn/ui. It provides issue tracking, project management, and team collaboration features with a modern, responsive design.

## Development Commands

- **Development server**: `pnpm dev` (runs with Turbopack for faster builds)
- **Build**: `pnpm build`
- **Production server**: `pnpm start`
- **Linting**: `pnpm lint`
- **Formatting**: `pnpm format`
- **Convex backend**: `npx convex dev` (starts local Convex development server)

## Core Architecture

### Application Structure

- **App Router**: Uses Next.js 15 App Router with dynamic organization-based routing
- **Layout Pattern**: Centralized layout system via `MainLayout` component with configurable headers
- **Organization Routing**: All main routes are scoped under `[orgId]` (e.g., `/lndev-ui/projects`)
- **Default Route**: Root organization redirects to `lndev-ui/team/CORE/all`

### State Management Architecture

- **Zustand**: Primary state management using multiple specialized stores
- **Store Pattern**: Domain-specific stores (issues, filters, notifications, search, view)
- **Mock Data**: Currently uses static mock data from `/mock-data` directory
- **State Structure**: Each store handles its own domain with actions, filters, and getters

### Key Stores:

- `issues-store.ts`: Central issue management with CRUD operations, filtering, and status updates
- `filter-store.ts`: UI filter state management
- `notifications-store.ts`: Notification system state
- `create-issue-store.ts`: Issue creation flow state

### UI Component Architecture

- **shadcn/ui**: Foundation UI library with Radix primitives
- **Component Hierarchy**:
   - `/ui`: Base shadcn components
   - `/common`: Business logic components organized by domain
   - `/layout`: Layout and navigation components
- **Styling**: TailwindCSS with CSS variables for theming
- **Design System**: Uses `class-variance-authority` for component variants

### Data Models

Issues use a sophisticated ranking system:

- **LexoRank Algorithm**: Uses `@kayron013/lexorank` for issue ordering (similar to Jira)
- **Issue Interface**: Comprehensive model with status, priority, assignee, labels, projects
- **Mock Data**: Structured mock data with relationships between users, projects, teams, issues

### Navigation & Layout

- **Sidebar**: Persistent sidebar with organization switcher, navigation, and issue creation
- **Dynamic Headers**: Configurable headers per route with navigation and filtering
- **Responsive Design**: Mobile-first approach with adaptive layouts
- **Theme System**: Dark theme by default with `next-themes` integration

### Technology Stack Specifics

- **React 19**: Latest React with new features
- **Next.js 15**: App Router, TailwindCSS 4, TypeScript 5.9
- **Convex**: Real-time backend (configured but not fully integrated with UI yet)
- **Form Handling**: `react-hook-form` with Zod validation
- **Drag & Drop**: `react-dnd` for issue reordering
- **Date Handling**: `react-day-picker` v9 with custom Chevron components
- **Animations**: `motion` (Framer Motion) for UI animations

## Development Patterns

### Component Organization

Components are organized by domain rather than type:

- Issue-related components in `/common/issues/`
- Project components in `/common/projects/`
- Layout components in `/layout/`

### Mock Data Integration

The application currently runs on mock data with realistic relationships:

- Issues reference users, projects, labels, and statuses
- Mock data includes proper TypeScript interfaces
- Data generation includes LexoRank for proper ordering

### State Management Patterns

- Stores encapsulate both data and business logic
- Actions include complex filtering and relationship management
- State updates maintain data consistency across related entities

### Styling Conventions

- Uses Tailwind utility classes extensively
- Custom CSS variables for theming defined in `globals.css`
- Component variants managed through `class-variance-authority`
- Responsive design with mobile-first approach

## Important Notes

### Convex Integration

- Convex is configured (`CONVEX_DEPLOYMENT` and `NEXT_PUBLIC_CONVEX_URL` in `.env.local`)
- Backend schema exists in `/convex/_generated/`
- Real-time features are set up but UI currently uses mock data

### Calendar Component

The calendar component uses react-day-picker v9 API:

- Custom icons use the `Chevron` component with `orientation` prop
- Breaking change from v8 where `IconLeft`/`IconRight` were separate components

### Performance Considerations

- Uses Turbopack for faster development builds
- Next.js Image optimization recommended over regular `<img>` tags
- Bundle size optimization through proper imports and code splitting
