# VectorFly Monorepo

This is a monorepo for the VectorFly platform, managed with [Turborepo](https://turbo.build) and npm workspaces. second deploy

## Structure

### Apps
- `apps/web`: User-facing web application (Next.js)
- `apps/contributor`: Contributor portal (Next.js)
- `apps/admin`: Admin panel (Next.js)
- `apps/api`: Backend API (NestJS)

### Packages
- `packages/ui`: Shared UI component library (Tailwind + ShadCN)
- `packages/database`: Prisma ORM and database client
- `packages/config`: Shared configuration (TSConfig, ESLint)
- `packages/types`: Shared TypeScript definitions
- `packages/api-client`: Shared API client
- `packages/env`: Environment variable validation
- `packages/logger`: Shared logging utility
- `packages/storage`: Storage abstraction
- `packages/queue`: Queue abstraction
- `packages/feature-flags`: Feature flags
- `packages/metrics`: Metrics collection

## Usage

### Install Dependencies
```bash
npm install
```

### Development
```bash
npm run dev
```

### Build
```bash
npm run build
```

### Database
```bash
npm run db:reset
```
