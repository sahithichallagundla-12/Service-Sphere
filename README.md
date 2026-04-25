# ServiceSphere

A comprehensive SLA management and contract tracking platform that connects companies with vendors, featuring AI-based SLA generation, real-time issue tracking, and performance monitoring.

## Overview

ServiceSphere is a modern web application built with Next.js that enables seamless collaboration between service providers and clients. It automates SLA (Service Level Agreement) generation using AI, tracks service issues in real-time, and maintains vendor ratings and performance metrics.

## Features

### Core Features

- **AI-Based SLA Generation** - Intelligent SLA parameters automatically generated when issues are raised based on service type and priority
- **Real-Time Issue Tracking** - Monitor issue status instantly with live synchronization between clients and vendors
- **Contract Management** - Create, manage, and track contracts between clients and vendors
- **Performance Monitoring** - Track SLA success rates, resolution times, and vendor ratings
- **Penalty System** - Automated tracking of penalties, warnings, and rating adjustments
- **Vendor Ratings** - Dynamic rating system based on performance and issue resolution
- **Billing & Payments** - Integrated payment tracking and billing management
- **Role-Based Access** - Separate dashboards for vendors and clients with tailored interfaces

### Advanced Capabilities

- **Issue Analytics** - Comprehensive dashboards showing issue trends and patterns
- **Contract Overview** - Visual contract status and performance summaries
- **Notification System** - Real-time alerts for issues, payments, and penalties
- **SLA Trend Charts** - Historical SLA performance visualization
- **Admin Console** - Full system administration and monitoring capabilities

## Tech Stack

### Frontend

- **Framework**: Next.js 14+ (React)
- **Language**: TypeScript
- **Styling**: Tailwind CSS with PostCSS
- **UI Components**: Radix UI (comprehensive component library)
- **Form Management**: React Hook Form with Zod validation
- **State Management**: React hooks and Context API
- **Charts**: Chart.js integration
- **Animations**: Framer Motion

### Backend

- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth
- **API Routes**: Next.js API Routes
- **Server Actions**: Next.js Server Functions

### Tools & Libraries

- **AI Integration**: Google Generative AI (Gemini)
- **Date Handling**: date-fns
- **Analytics**: Vercel Analytics
- **Environment**: dotenv

## Project Structure

```
service_sphere-main/
├── app/
│   ├── api/                    # API routes
│   │   ├── contracts/         # Contract endpoints
│   │   ├── issues/            # Issue management endpoints
│   │   ├── services/          # Service endpoints
│   │   ├── sla/               # SLA endpoints
│   │   ├── ratings/           # Rating endpoints
│   │   └── cron/              # Scheduled tasks
│   ├── auth/                   # Authentication pages
│   │   ├── login/
│   │   ├── sign-up/
│   │   └── callback/
│   ├── client/                 # Client dashboard pages
│   │   ├── dashboard/
│   │   ├── contracts/
│   │   ├── issues/
│   │   ├── services/
│   │   └── notifications/
│   ├── vendor/                 # Vendor dashboard pages
│   │   ├── dashboard/
│   │   ├── contracts/
│   │   ├── issues/
│   │   ├── billing/
│   │   ├── payments/
│   │   └── penalties/
│   └── admin/                  # Admin console
├── components/
│   ├── client/                 # Client-specific components
│   ├── vendor/                 # Vendor-specific components
│   ├── shared/                 # Shared components
│   └── ui/                     # Reusable UI components
├── lib/
│   ├── actions/               # Server actions
│   ├── supabase/              # Supabase client config
│   ├── types.ts               # TypeScript type definitions
│   └── utils.ts               # Utility functions
├── hooks/                      # Custom React hooks
├── scripts/                    # Database migration scripts
└── middleware.ts              # Next.js middleware
```

## Getting Started

### Prerequisites

- Node.js 18+ or pnpm
- Supabase account
- Google Generative AI API key (for AI-based SLA generation)

### Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd service_sphere-main
   ```

2. **Install dependencies**

   ```bash
   pnpm install
   ```

3. **Environment Setup**
   Create a `.env` file in the root directory:

   ```env
   # Supabase Configuration
   NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
   SUPABASE_SERVICE_ROLE_KEY=your_service_role_key

   # Google AI API
   GOOGLE_GENERATIVE_AI_API_KEY=your_google_ai_key

   # Other Configuration
   NEXT_PUBLIC_APP_URL=http://localhost:3000
   ```

4. **Database Setup**
   Run the migration scripts in order:

   ```bash
   # Apply schemas and initial setup
   ./scripts/001_create_tables.sql
   ./scripts/002_seed_sample_data.sql
   # Additional migrations as needed
   ```

5. **Start Development Server**
   ```bash
   pnpm dev
   ```
   Open [http://localhost:3000](http://localhost:3000) in your browser.

## Usage

### For Clients

1. Sign up as a Company
2. Browse and purchase services from vendors
3. Create contracts with selected vendors
4. Raise issues when service problems occur
5. Monitor SLA compliance and vendor performance
6. Track payments and billing history

### For Vendors

1. Sign up as a Vendor
2. Create and manage service offerings
3. View client contracts and terms
4. Accept and resolve issues
5. Monitor your ratings and performance metrics
6. Manage billing and payments
7. Track penalties and rating adjustments

### For Admins

1. Access the Admin Console
2. Monitor system-wide metrics
3. Manage users and contracts
4. Review penalties and disputes
5. Oversee payments and billing

## API Endpoints

### Contracts

- `GET /api/contracts` - List contracts
- `POST /api/contracts` - Create contract
- `GET /api/contracts/[id]` - Get contract details
- `PUT /api/contracts/[id]` - Update contract

### Issues

- `GET /api/issues` - List issues
- `POST /api/issues` - Create issue (triggers AI SLA generation)
- `GET /api/issues/[id]` - Get issue details
- `PUT /api/issues/[id]` - Update issue status

### Services

- `GET /api/services` - List services
- `POST /api/services` - Create service
- `GET /api/services/[id]` - Get service details

### SLA

- `GET /api/sla` - Get SLA metrics
- `POST /api/sla` - Create/update SLA

### Ratings

- `GET /api/ratings` - Get vendor ratings
- `POST /api/ratings` - Submit rating

## Database Schema

### Key Tables

- **profiles** - User accounts (clients/vendors)
- **services** - Service offerings
- **contracts** - Service contracts
- **issues** - Support tickets with SLA tracking
- **slas** - Service level agreements
- **ratings** - Vendor performance ratings
- **penalties** - System penalties and warnings
- **payments** - Payment records
- **notifications** - User notifications

## Authentication

ServiceSphere uses Supabase Authentication with:

- Email/Password sign-up and login
- OAuth integration support
- Role-based access control (RBAC)
- Session management with JWT tokens

## Development

### Running Tests

```bash
pnpm lint
```

### Building for Production

```bash
pnpm build
pnpm start
```

### Code Style

- TypeScript for type safety
- ESLint for code quality
- Tailwind CSS for styling consistency

## Key Features Implementation

### AI-Based SLA Generation

When an issue is created, the system automatically:

1. Analyzes the issue priority and service type
2. Uses Google Generative AI to determine appropriate SLA parameters
3. Stores the AI-generated SLA with the issue
4. Tracks compliance with the generated SLA

### Real-Time Synchronization

- Uses Supabase real-time subscriptions for instant updates
- Client and vendor dashboards stay synchronized
- Notifications trigger on status changes

### Performance Tracking

- Automatic calculation of SLA success rates
- Vendor rating adjustments based on performance
- Historical trend analysis

## Contributing

1. Create a feature branch (`git checkout -b feature/amazing-feature`)
2. Commit changes (`git commit -m 'Add amazing feature'`)
3. Push to branch (`git push origin feature/amazing-feature`)
4. Open a Pull Request

## License

This project is private and proprietary.

## Support

For issues, questions, or suggestions, please contact the development team or create an issue in the repository.

---

**ServiceSphere** - Simplifying Service Management & Contract Tracking
