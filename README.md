# DAYFORGE — Personal Life Management Platform
## Product Requirements Document, UX/UI Specification, Technical Architecture, Database Schema, Implementation Roadmap, and Coding-Agent Master Prompt

**Document version:** 1.0  
**Product type:** Personal productivity and life-management web application  
**Platforms:** Desktop, mobile, installable Progressive Web App (PWA)  
**Primary users:** Individuals who want to improve their use of time, financial discipline, daily routines, and long-term progress  
**Interface languages:** English, Afaan Oromoo, Amharic  
**Currency default:** Ethiopian birr (ETB), configurable  
**Accountability model:** Adaptive reminders and escalating check-ins  
**AI model:** Optional AI productivity coach

---

# Part I — Product Requirements Document

## 1. Product vision

DAYFORGE is a personal life-management platform that helps users plan their days, track their real activities, manage money, maintain routines, achieve goals, and learn from their behavior.

It combines five connected capabilities:

1. Daily planning and execution.
2. Time and activity tracking.
3. Personal finance and spending control.
4. Habit, routine, and goal management.
5. Personal analytics and AI-assisted coaching.

The product must be useful without AI, accurate without manual calculations, and simple enough to use every day.

### 1.1 Problem statement

People frequently plan their days but fail to record how they actually spend their time. Expenses are forgotten, routines become inconsistent, priorities are postponed, and long-term progress becomes difficult to measure.

DAYFORGE addresses these problems by connecting planned activities to actual records and converting those records into useful reports.

### 1.2 Product objectives

- Make daily planning and recording fast.
- Increase the completion rate of realistic daily plans.
- Show where time is spent and how much of it is tracked.
- Provide accurate income, expense, budget, and savings records.
- Improve consistency with flexible habits and routines.
- Generate meaningful daily, weekly, and monthly reports.
- Offer personalized recommendations without shaming or manipulating the user.
- Keep personal information private and allow users to export their data.
- Work well on desktop and mobile, including selected offline workflows.

### 1.3 Non-goals for the initial release

Do not include these in the initial MVP:

- Automatic bank synchronization.
- Investment trading or portfolio management.
- Social feeds, public profiles, or competitive leaderboards.
- Medical diagnosis or health recommendations.
- Unrestricted AI access to financial records or external accounts.
- Automatic deletion of tasks, transactions, or user data.
- Complex multi-user teams and enterprise administration.

The first release should focus on making the core personal workflow reliable.

## 2. Target users and use cases

### Primary persona: The self-improving individual

A person balancing study, work, personal projects, spending, and daily responsibilities.

Needs:
- Plan realistic days.
- Stay accountable without excessive pressure.
- Track time spent on productive and recreational activities.
- Know exactly where money goes.
- Review progress regularly.

### Core user journeys

**Journey A — Plan the day**
1. Open the Today dashboard.
2. Review incomplete tasks.
3. Select three priority outcomes.
4. Schedule tasks and estimate their duration.
5. Review available time and conflicts.
6. Start the day.

**Journey B — Track an activity**
1. Select an activity or task.
2. Start its timer.
3. Pause or resume when necessary.
4. Stop the timer.
5. Save the resulting activity entry.
6. Review the updated time report.

**Journey C — Record an expense**
1. Open Quick Add.
2. Select Expense.
3. Enter amount, category, account, date, and optional note.
4. Save the transaction.
5. Update the balance and budget summary.
6. View the transaction in reports.

**Journey D — Review the day**
1. Review task completion.
2. Review tracked and untracked time.
3. Review income, expenses, and budget limits.
4. Review scheduled habits.
5. Write a short reflection.
6. Generate tomorrow's starting plan.

**Journey E — Receive coaching**
1. Review a report.
2. Open the AI coach.
3. Ask for an explanation or practical improvement plan.
4. Review the evidence behind its recommendations.
5. Approve any suggested changes before they modify records.

## 3. Functional requirements

Priority definitions:
- **P0:** Required for MVP launch.
- **P1:** Important next-phase feature.
- **P2:** Advanced feature.

### FR-01 — Authentication and profile

Priority: P0

Requirements:
- Sign up, sign in, sign out, and recover access.
- Maintain authenticated sessions securely.
- Store profile settings and preferred language.
- Support a configurable time zone and currency.
- Provide data export and account deletion workflows.
- Ensure that users can access only their own private data.

Acceptance criteria:
- A registered user can sign in and recover access.
- Unauthenticated users cannot access private application routes or data.
- Changing language persists across sessions.
- All user-owned database records are protected by database-level authorization.
- Account deletion requires confirmation and follows a documented deletion policy.

### FR-02 — Daily planner and task management

Priority: P0

Requirements:
- Create, edit, complete, cancel, postpone, and reschedule tasks.
- Store title, description, priority, status, due date, planned start, estimated duration, and category.
- Support recurring tasks.
- Identify the three most important tasks of the day.
- Display tasks in list and timeline views.
- Link tasks to goals and optional time-tracking sessions.
- Provide overdue and incomplete task views.
- Preserve task history when dates or statuses change.

Acceptance criteria:
- Task changes persist after refresh.
- Completed tasks are excluded from active task lists by default.
- A postponed task is not automatically recorded as failed.
- The planner warns about overlapping scheduled tasks.
- Estimated time exceeding available time produces a clear warning, not silent deletion or automatic rescheduling.
- Recurring task occurrences can be completed independently.

### FR-03 — Time tracking

Priority: P0

Requirements:
- Start, pause, resume, and stop an activity timer.
- Link a timer to a task or create an independent activity.
- Categorize time as study, work, personal projects, exercise, travel, entertainment, rest, or custom categories.
- Allow manual entry and editing.
- Store actual start and end timestamps.
- Show daily and weekly timelines.
- Detect overlapping time entries.
- Distinguish tracked time from untracked time.
- Support timer recovery after refresh, browser restart, or device restart.

Acceptance criteria:
- The displayed duration is calculated from timestamps, not accumulated browser ticks.
- Refreshing the page does not lose a running timer.
- The system does not create duplicate sessions when a user repeatedly clicks Start.
- Paused intervals are excluded from active duration.
- Overlapping entries trigger a warning and an explicit resolution option.
- The user can correct mistakes without losing the original creation and update timestamps.
- Time tracking works even if the application is temporarily offline, with clear synchronization status.

### FR-04 — Personal finance

Priority: P0

Requirements:
- Create financial accounts, such as cash and bank accounts.
- Record income, expenses, refunds, and transfers.
- Categorize transactions.
- Store amount, currency, date, account, category, and optional note.
- Set daily, weekly, monthly, and category-specific budgets.
- Create savings goals.
- Show available balance, spending totals, remaining budget, and transaction history.
- Support transaction editing, deletion or voiding according to the audit policy.
- Support manual financial records without external bank connections.

Acceptance criteria:
- Every transaction is validated before saving.
- Transfers between two accounts do not inflate income or expenses.
- A transfer updates the source and destination balances consistently.
- Refunds are represented explicitly and reflected correctly in net expense reporting.
- Budgets use consistent definitions for the reporting period.
- A user can correct an erroneous transaction.
- Balance changes and associated transaction records remain consistent if a request fails.
- The application never claims to have verified a real bank balance.

### FR-05 — Habits and routines

Priority: P0

Requirements:
- Create habits with a name, schedule, target, and measurement type.
- Support checkbox, count, and duration-based habits.
- Schedule habits on selected weekdays or recurring patterns.
- Create named routines such as Morning Routine and Evening Review.
- Record completed, missed, skipped, and excused occurrences.
- Support optional reminders and streaks.
- Allow rest days and configurable skip policies.

Acceptance criteria:
- Only scheduled occurrences contribute to the eligible habit-completion denominator.
- Unscheduled days do not break a streak unless the configured policy explicitly requires it.
- Editing a habit does not silently rewrite historical logs.
- A skipped occurrence has a distinct status from a completed occurrence.
- Habit progress is calculated consistently in the dashboard and reports.

### FR-06 — Goals and milestones

Priority: P1

Requirements:
- Create goals with a title, description, deadline, and target.
- Break goals into milestones and tasks.
- Link habits and tasks to goals.
- Track progress and status.
- Identify overdue and at-risk goals.
- Support weekly and monthly objectives.

Acceptance criteria:
- Goal progress is derived from defined milestones or measurable targets.
- Progress does not exceed the valid range without explicit support for that goal type.
- Completing linked tasks updates relevant progress indicators.
- Deleted or archived goals do not erase historical task or time records.

### FR-07 — Reports and analytics

Priority: P0

Requirements:
- Daily, weekly, and monthly reports.
- Task completion rate.
- Estimated versus actual task duration.
- Tracked time by category.
- Time-entry coverage and missing-data indicators.
- Expense breakdown and budget utilization.
- Income, expenses, net cash flow, and savings tracking.
- Habit consistency.
- Comparison with previous periods.
- CSV export and a later PDF export feature.
- Explicit reporting-period boundaries and time-zone handling.

Acceptance criteria:
- Reports match the underlying records for the same date range.
- Transferred money is excluded from income and expense totals.
- Missing time data is never interpreted as wasted time.
- Zero denominators return a neutral or unavailable value rather than an invalid number.
- Exported records respect the selected filters and date range.
- Every metric has a documented formula.

### FR-08 — Daily journal and reflection

Priority: P1

Requirements:
- Add daily notes and end-of-day reflections.
- Optionally record mood, energy, and stress using user-defined scales.
- Record wins, challenges, and lessons.
- Display past reflections in chronological order.
- Allow users to edit and delete reflections.

Acceptance criteria:
- Journal entries are private and user-owned.
- Empty journal fields do not prevent completing the daily review.
- Reflections are excluded from AI processing unless the user enables or initiates that processing.

### FR-09 — Adaptive accountability

Priority: P0 for basic reminders; P1 for adaptive escalation.

Requirements:
- Schedule reminders for tasks, habits, and daily reviews.
- Track whether a reminder was delivered where delivery status is available.
- Escalate reminders according to user preferences.
- Suppress duplicate or excessive reminders.
- Respect quiet hours, time zone, and notification permissions.
- Allow snoozing, dismissing, and disabling reminders.
- Adapt future reminder timing based on explicit user settings and observed interactions.

Acceptance criteria:
- Quiet hours are respected.
- A completed task does not continue generating its pending reminders.
- The same reminder event is not delivered repeatedly because of a retry.
- The user can disable adaptive escalation.
- Missed tasks never trigger punitive actions, financial penalties, or irreversible changes.
- Every escalation can be explained and configured.

### FR-10 — AI coach

Priority: P1

Requirements:
- Summarize the day or week.
- Explain patterns using available records.
- Suggest realistic task schedules.
- Suggest habit improvements and budget adjustments.
- Identify overplanning and recurring postponements.
- Show which records and reporting periods support each insight.
- Offer proposed changes for user approval.
- Support the three interface languages where the configured model can reliably produce them.

Acceptance criteria:
- AI recommendations are grounded in actual user data supplied to the model.
- The coach identifies missing or insufficient data.
- The coach does not invent activities, transactions, or completed tasks.
- AI cannot directly execute destructive operations.
- Proposed schedule or budget changes require explicit confirmation.
- If the AI service fails, all core non-AI features remain available.
- The user can disable AI and control which data categories may be shared with the configured AI provider.

### FR-11 — Internationalization

Priority: P0

Requirements:
- Support English, Afaan Oromoo, and Amharic.
- Store UI strings in translation resources.
- Support Unicode and Ethiopic-script text.
- Format dates, times, and numbers using locale-aware utilities.
- Keep the user's calendar and time zone settings explicit.
- Store transaction currency separately from interface language.
- Avoid hardcoded interface text.
- Use readable fonts and suitable text spacing for all supported languages.

Acceptance criteria:
- All primary navigation, forms, validation messages, dialogs, and empty states are translated.
- Changing language does not alter stored financial values or dates.
- Long translations do not break navigation or buttons.
- Ethiopic text renders correctly on supported desktop and mobile browsers.
- Missing translations fall back predictably without displaying internal keys.

### FR-12 — PWA and offline behavior

Priority: P0 for installation; limited offline support.

Requirements:
- Provide a valid web app manifest and service worker.
- Support installation on compatible mobile and desktop browsers.
- Cache static application assets.
- Show online, offline, and synchronization states.
- Preserve local drafts during temporary disconnections.
- Queue supported user-created records for synchronization.
- Provide conflict detection for edits made on multiple devices.

Acceptance criteria:
- The app can be installed on compatible browsers.
- A refresh does not destroy an unsynchronized local draft.
- Offline edits are not falsely marked as saved to the server.
- Duplicate synchronization does not create duplicate transactions or timer entries.
- Conflicting edits are surfaced or resolved using documented rules.
- Sensitive personal data is not placed in a public or unprotected cache.

---

# Part II — UX/UI Specification

## 4. Visual design system

### Design direction

Create a premium, focused, modern productivity interface. It should feel calm and purposeful rather than crowded or gamified.

Default theme:
- Dark charcoal background for the primary dark theme.
- Neutral surfaces and subtle borders.
- Teal or emerald for completion and positive progress.
- Indigo for focus and time.
- Amber for financial information and warnings.
- Red only for errors, destructive actions, and serious alerts.

Also provide a well-designed light theme.

### Typography
- Use a modern, readable sans-serif font.
- Select a font with reliable Latin and Ethiopic character coverage.
- Use a consistent type scale and line height.
- Never communicate status through color alone.

### Layout
- Desktop: collapsible sidebar and flexible main content area.
- Tablet: compact navigation with adaptive columns.
- Mobile: bottom navigation and single-column content.
- Quick Add: always accessible from primary application screens.
- Respect mobile safe areas and touch-target accessibility.

### Core UI components
- Buttons, icon buttons, dialogs, drawers, and menus.
- Task cards and timeline entries.
- Activity timer controls.
- Habit checkboxes and counters.
- Financial transaction forms.
- Budget progress indicators.
- Date and time pickers.
- Search, filters, and sorting.
- Charts and report tables.
- Toast notifications.
- Loading skeletons, empty states, offline banners, and error states.
- Confirmation dialogs for destructive actions.

## 5. Screen-by-screen specification

### Screen 1 — Today dashboard

Purpose: The single place to understand and act on the current day.

Sections:
1. Date, greeting, and daily-review status.
2. Daily execution summary.
3. Three priority outcomes.
4. Active timer card.
5. Today's timeline.
6. Habit checklist.
7. Spending and budget summary.
8. Daily insight or coach recommendation.
9. Quick Add action.

Primary actions:
- Add task.
- Start or stop timer.
- Log expense.
- Complete habit.
- Open daily review.

Rules:
- Avoid overwhelming the user with excessive charts.
- Show sample-free empty states for a new account.
- Clearly label data that has not yet been tracked.

### Screen 2 — Planner

Views:
- Day timeline.
- Week calendar.
- Task list.
- Unscheduled tasks.

Task creation form:
- Title.
- Description.
- Category.
- Priority.
- Planned date and time.
- Estimated duration.
- Deadline.
- Optional goal.
- Recurrence.
- Reminder.

### Screen 3 — Time tracker

Sections:
- Active timer.
- Recent activities.
- Daily timeline.
- Activity category breakdown.
- Weekly summary.

Activity entry fields:
- Activity title.
- Category.
- Linked task.
- Start time.
- End time.
- Paused duration or explicitly represented segments.
- Notes.

Allow manual corrections and overlapping-entry resolution.

### Screen 4 — Finance

Tabs:
- Overview.
- Transactions.
- Budgets.
- Accounts.
- Savings goals.

Finance overview:
- Selected account balances.
- Income and expense totals.
- Net cash flow.
- Budget usage.
- Expense-category chart.
- Recent transactions.

Transaction form:
- Transaction type.
- Amount.
- Currency.
- Account.
- Destination account for transfers.
- Category.
- Date and time.
- Optional description.

### Screen 5 — Habits and routines

Sections:
- Today's scheduled habits.
- Routine groups.
- Weekly completion grid.
- Streaks.
- Habit history.

Habit creation:
- Name.
- Schedule.
- Measurement type.
- Target.
- Reminder.
- Rest-day policy.
- Optional goal link.

### Screen 6 — Goals

Sections:
- Active goals.
- Milestones.
- Progress indicators.
- Linked tasks and habits.
- Upcoming deadlines.
- Completed goals.

### Screen 7 — Reports

Filters:
- Date range.
- Report period.
- Time category.
- Financial account.
- Transaction category.

Report sections:
- Task execution.
- Time allocation.
- Time tracking coverage.
- Spending and budget.
- Habit consistency.
- Goal progress.
- Comparison with a previous period.

### Screen 8 — Daily review

Sections:
- What was planned?
- What was completed?
- Where did time go?
- What money was spent?
- Which habits were completed?
- What went well?
- What was difficult?
- What should change tomorrow?

Allow users to complete the review in a few minutes.

### Screen 9 — AI coach

Features:
- Suggested questions.
- Daily and weekly summaries.
- Evidence-backed recommendations.
- Proposed schedule changes.
- Confirmation before changes.
- AI data-sharing settings.
- Clear indication when a response is based on incomplete records.

### Screen 10 — Settings

Groups:
- Profile.
- Language.
- Theme.
- Time zone.
- Currency.
- Notifications and quiet hours.
- AI privacy controls.
- Data export.
- Account deletion.
- Offline data management.

---

# Part III — Business Rules and Metric Definitions

## 6. Authoritative calculations

Use shared, tested domain functions rather than implementing separate formulas in multiple screens.

### Task completion rate

Completed eligible planned tasks divided by eligible planned tasks, multiplied by 100.

Define treatment of canceled, postponed, and recurring tasks explicitly. Do not classify a postponed task as failed solely because its original date passed.

### Habit consistency

Completed scheduled occurrences divided by eligible scheduled occurrences, multiplied by 100.

Exclude unscheduled days. Treat skipped or excused occurrences according to the configured policy, and make the policy visible.

### Tracked-time coverage

Tracked minutes divided by the defined available minutes, multiplied by 100.

Available time must be explicitly defined. Avoid assuming that all non-tracked time is wasted or unproductive.

### Budget utilization

Eligible net expenses for the relevant budget period divided by its limit, multiplied by 100.

A budget can exceed 100%. The UI must display overspending rather than cap the actual calculation.

### Net cash flow

Income minus expenses for the selected period.

Transfers between accounts are excluded. Refunds reduce net expenses according to the accounting rules.

### Account balance

Opening balance plus signed ledger movements, including transfers and corrections.

Use a single authoritative financial transaction model. Do not independently maintain inconsistent balances in multiple frontend components.

### Savings

Allow users to record savings goals and contributions. Distinguish recorded transfers into savings accounts from income and expenses.

A savings rate is meaningful only when its numerator and denominator are defined. If the app estimates savings as income minus expenses, label that measure clearly and do not imply that the money has actually been deposited into savings.

### Time duration

Calculate duration from persisted timestamps or recorded time segments. Never depend on a browser interval counter as the source of truth.

---

# Part IV — Technical Architecture

## 7. Recommended stack

### Frontend
- React.
- Vite.
- TypeScript.
- Tailwind CSS.
- Accessible component primitives.
- Lucide icons.
- Recharts.
- React Hook Form.
- Zod.
- TanStack Query.
- An internationalization library such as i18next.
- A PWA plugin and service-worker tooling.

### Backend
- Supabase Auth.
- PostgreSQL.
- Row Level Security.
- Database migrations.
- Server-side functions for privileged operations.
- Scheduled jobs for reminders where supported.

### Testing
- Vitest.
- React Testing Library.
- Playwright.
- Database integration tests.
- Authorization and migration tests.

### Deployment
- GitHub for version control.
- Vercel or another compatible static frontend host.
- Supabase for the managed database and authentication.
- Automated CI checks.
- Separate development and production environments.

## 8. Logical architecture

```text
Desktop Browser / Mobile Browser / Installed PWA
                       |
                       v
              React + TypeScript
                       |
          UI Components and Routes
                       |
          Domain Services and Queries
                       |
             Supabase Client SDK
                       |
           Authenticated API Access
                       |
                       v
                PostgreSQL
       +---------------+---------------+
       |               |               |
    RLS Policies   Constraints      Indexes
       |               |               |
       +---------------+---------------+
                       |
              Trusted Server Functions
                       |
          +------------+-------------+
          |            |             |
       Reminders     AI Coach     Exports
```

### Architecture principles

1. Separate UI components from business logic.
2. Keep financial and time calculations in shared domain services.
3. Enforce ownership in the database, not only in React.
4. Use database transactions for operations that must succeed or fail together.
5. Treat the browser as untrusted.
6. Make AI an optional service, not a dependency of the core product.
7. Use explicit loading, failure, offline, and synchronization states.
8. Prefer small, testable modules over a single large application component.

## 9. Suggested project structure

```text
dayforge/
├── public/
│   ├── icons/
│   ├── manifest.webmanifest
│   └── locales/
├── src/
│   ├── app/
│   │   ├── router.tsx
│   │   ├── providers.tsx
│   │   └── query-client.ts
│   ├── components/
│   │   ├── ui/
│   │   ├── layout/
│   │   └── feedback/
│   ├── features/
│   │   ├── auth/
│   │   ├── dashboard/
│   │   ├── tasks/
│   │   ├── planner/
│   │   ├── time-tracking/
│   │   ├── finance/
│   │   ├── habits/
│   │   ├── goals/
│   │   ├── reports/
│   │   ├── journal/
│   │   ├── reminders/
│   │   ├── ai-coach/
│   │   └── settings/
│   ├── domain/
│   │   ├── finance/
│   │   ├── time/
│   │   ├── tasks/
│   │   ├── habits/
│   │   └── reports/
│   ├── hooks/
│   ├── lib/
│   ├── i18n/
│   ├── types/
│   ├── styles/
│   └── test/
├── supabase/
│   ├── migrations/
│   ├── functions/
│   └── seed.sql
├── e2e/
├── docs/
├── .env.example
├── package.json
├── vite.config.ts
└── README.md
```

This structure is a starting point, not a requirement to create empty folders. Each module should contain real functionality, tests, and clear interfaces.

---

# Part V — Database Schema

## 10. Data model

Use PostgreSQL with UUID primary keys, UTC timestamps, explicit ownership, foreign keys, constraints, and database indexes.

Core tables:
- profiles
- tasks
- activity_entries
- activity_segments
- habits
- habit_logs
- routines
- routine_habits
- financial_accounts
- transactions
- budgets
- goals
- goal_milestones
- daily_reviews
- reminders
- ai_conversations, only if persistent AI chat is enabled

For the MVP, keep recurring task and habit schedules simple. Add more advanced recurrence rules only when the first version is stable.

## 11. Initial PostgreSQL migration

The following SQL is a baseline schema for the core application. Run it through version-controlled Supabase migrations, then add and test the remaining tables, policies, and functions before production deployment.

```sql
create extension if not exists pgcrypto;

create type public.task_status as enum (
  'todo',
  'in_progress',
  'completed',
  'postponed',
  'cancelled'
);

create type public.transaction_type as enum (
  'income',
  'expense',
  'refund',
  'transfer'
);

create type public.habit_log_status as enum (
  'completed',
  'missed',
  'skipped',
  'excused'
);

create table public.profiles (
  id uuid primary key references auth.users(id) on delete cascade,
  display_name text,
  preferred_language text not null default 'en'
    check (preferred_language in ('en', 'om', 'am')),
  timezone text not null default 'Africa/Addis_Ababa',
  currency char(3) not null default 'ETB',
  theme text not null default 'system'
    check (theme in ('light', 'dark', 'system')),
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create table public.goals (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  title text not null check (length(trim(title)) between 1 and 200),
  description text,
  status text not null default 'active'
    check (status in ('active', 'completed', 'paused', 'archived')),
  target_value numeric(18,4),
  current_value numeric(18,4) not null default 0,
  unit text,
  start_date date,
  due_date date,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),
  check (due_date is null or start_date is null or due_date >= start_date)
);

create table public.tasks (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  goal_id uuid references public.goals(id) on delete set null,
  title text not null check (length(trim(title)) between 1 and 250),
  description text,
  category text,
  priority smallint not null default 3 check (priority between 1 and 5),
  status public.task_status not null default 'todo',
  planned_start timestamptz,
  due_at timestamptz,
  estimated_minutes integer check (estimated_minutes is null or estimated_minutes > 0),
  actual_minutes integer check (actual_minutes is null or actual_minutes >= 0),
  is_daily_priority boolean not null default false,
  recurrence_rule text,
  completed_at timestamptz,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create index tasks_user_due_idx
  on public.tasks(user_id, due_at);

create index tasks_user_status_idx
  on public.tasks(user_id, status);

create table public.activity_entries (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  task_id uuid references public.tasks(id) on delete set null,
  title text not null check (length(trim(title)) between 1 and 250),
  category text not null,
  started_at timestamptz not null,
  ended_at timestamptz,
  status text not null default 'stopped'
    check (status in ('running', 'paused', 'stopped')),
  notes text,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),
  check (ended_at is null or ended_at >= started_at)
);

create index activity_user_start_idx
  on public.activity_entries(user_id, started_at desc);

create table public.activity_segments (
  id uuid primary key default gen_random_uuid(),
  activity_id uuid not null references public.activity_entries(id) on delete cascade,
  user_id uuid not null references auth.users(id) on delete cascade,
  started_at timestamptz not null,
  ended_at timestamptz,
  created_at timestamptz not null default now(),
  check (ended_at is null or ended_at >= started_at)
);

create table public.habits (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  title text not null check (length(trim(title)) between 1 and 200),
  description text,
  measurement_type text not null default 'boolean'
    check (measurement_type in ('boolean', 'count', 'duration')),
  target_value numeric(12,3),
  target_unit text,
  schedule jsonb not null default '{"days":[1,2,3,4,5,6,7]}'::jsonb,
  is_active boolean not null default true,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create table public.habit_logs (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  habit_id uuid not null references public.habits(id) on delete cascade,
  occurrence_date date not null,
  status public.habit_log_status not null,
  measured_value numeric(12,3),
  note text,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),
  unique (habit_id, occurrence_date)
);

create table public.financial_accounts (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  name text not null check (length(trim(name)) between 1 and 100),
  currency char(3) not null default 'ETB',
  opening_balance_minor bigint not null default 0,
  is_active boolean not null default true,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),
  unique (id, user_id)
);

create table public.transactions (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  account_id uuid not null,
  destination_account_id uuid,
  type public.transaction_type not null,
  amount_minor bigint not null check (amount_minor > 0),
  currency char(3) not null default 'ETB',
  category text,
  description text,
  occurred_at timestamptz not null default now(),
  transfer_group_id uuid,
  voided_at timestamptz,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),

  foreign key (account_id, user_id)
    references public.financial_accounts(id, user_id),

  foreign key (destination_account_id, user_id)
    references public.financial_accounts(id, user_id),

  check (
    (type = 'transfer'
      and destination_account_id is not null
      and destination_account_id <> account_id)
    or
    (type <> 'transfer' and destination_account_id is null)
  )
);

create index transactions_user_date_idx
  on public.transactions(user_id, occurred_at desc);

create index transactions_user_category_idx
  on public.transactions(user_id, category);

create table public.budgets (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  name text not null,
  category text,
  amount_minor bigint not null check (amount_minor > 0),
  currency char(3) not null default 'ETB',
  period text not null
    check (period in ('daily', 'weekly', 'monthly', 'custom')),
  starts_on date not null,
  ends_on date not null,
  alert_threshold numeric(5,2) not null default 80
    check (alert_threshold > 0 and alert_threshold <= 100),
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),
  check (ends_on >= starts_on)
);

create table public.goal_milestones (
  id uuid primary key default gen_random_uuid(),
  goal_id uuid not null references public.goals(id) on delete cascade,
  user_id uuid not null references auth.users(id) on delete cascade,
  title text not null,
  due_date date,
  completed_at timestamptz,
  sort_order integer not null default 0,
  created_at timestamptz not null default now()
);

create table public.daily_reviews (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  review_date date not null,
  wins text,
  challenges text,
  lessons text,
  tomorrow_priority text,
  mood smallint check (mood between 1 and 5),
  energy smallint check (energy between 1 and 5),
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),
  unique (user_id, review_date)
);

create table public.reminders (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  task_id uuid references public.tasks(id) on delete cascade,
  habit_id uuid references public.habits(id) on delete cascade,
  title text not null,
  scheduled_at timestamptz not null,
  status text not null default 'pending'
    check (status in ('pending', 'sent', 'dismissed', 'cancelled')),
  escalation_level smallint not null default 0
    check (escalation_level between 0 and 5),
  idempotency_key text not null,
  created_at timestamptz not null default now(),
  unique (user_id, idempotency_key)
);
```

### Important schema implementation requirements

This migration is a starting point, not a complete production database. Before release:

1. Add and test Row Level Security policies for every user-owned table.
2. Create a profile initialization trigger or server-side provisioning workflow.
3. Add shared `updated_at` handling.
4. Validate ownership of task and goal relationships, including `goal_id`.
5. Enforce one active timer per user with a partial unique index or an equivalent concurrency-safe design.
6. Add database constraints and transactional functions for activity segments and financial transfers.
7. Define how refunds, voids, and transfer reversals affect ledger calculations.
8. Validate that all related financial accounts use compatible currencies for a transfer.
9. Add schedule validation for habits and recurring tasks.
10. Add appropriate deletion, archival, and audit policies.
11. Create migration and integration tests.
12. Use integer minor units for money, with a documented currency-precision policy.

For financial accounts, derive balances from the opening balance and valid ledger movements or maintain a transactionally updated balance with reconciliation checks. Do not let client-side calculations become the authoritative ledger.

---

# Part VI — Security, Privacy, and Reliability

## 12. Security requirements

### Authentication
- Use the managed authentication provider.
- Never store plaintext passwords.
- Use secure session handling and refresh behavior.
- Protect private routes and API operations.
- Configure appropriate redirect URLs and authentication policies.

### Database authorization
- Enable RLS on all tables exposed through the application API.
- Scope reads, inserts, updates, and deletes to the authenticated user's identity.
- Validate ownership of referenced records.
- Use least-privilege database and service credentials.
- Never expose a privileged service-role key in frontend code.

### Financial integrity
- Use integer minor units for monetary amounts.
- Use database transactions for linked financial operations.
- Validate transfers, refunds, and corrections.
- Prevent duplicate requests from generating duplicate ledger records.
- Keep a clear history of material financial changes.

### AI privacy
- Do not send personal data to an AI provider without an explicit product policy and appropriate user consent.
- Send only the information necessary for the request.
- Exclude secrets, credentials, and unnecessary identifying information.
- Never let an AI model directly issue arbitrary SQL.
- Require user approval for changes to plans, budgets, tasks, and habits.
- Allow users to disable AI and remove stored AI conversation history.

### Data protection
- Provide account export and deletion.
- Use HTTPS in production.
- Keep secrets in managed environment variables.
- Avoid logging financial details, journal content, access tokens, or sensitive AI prompts.
- Define backup retention and test restoration.
- Document how offline data is protected and synchronized.

## 13. Reliability and observability

The product should include:
- Structured error logging.
- Error monitoring without sensitive payloads.
- Performance monitoring.
- Health checks for critical backend services.
- Migration verification.
- Backup and restoration procedures.
- Clear user-facing failure states.
- A mechanism to report incorrect calculations.
- An operational runbook for failed deployments and data recovery.

---

# Part VII — Testing Strategy

## 14. Required tests

### Unit tests

Test:
- Task completion calculations.
- Habit consistency and streak rules.
- Activity duration and pause/resume calculations.
- Time-zone and date-range boundaries.
- Budget utilization.
- Transaction balances and transfers.
- Refund and void behavior.
- Savings calculations.
- Report aggregation.
- Locale-aware date and currency formatting.

### Integration tests

Test:
- Authentication and profile initialization.
- Database ownership policies.
- Task and goal relationships.
- Timer creation and recovery.
- Activity segment persistence.
- Financial transfers and transaction rollback.
- Habit occurrence uniqueness.
- Reminder idempotency.
- Report queries against seeded records.
- Data export and deletion.

### End-to-end tests

At minimum, automate these journeys:

1. Sign up and complete profile setup.
2. Create a task and complete it.
3. Start a timer, pause, resume, and stop.
4. Refresh while a timer is running and recover it.
5. Record income and expenses.
6. Transfer money between two accounts.
7. Create a budget and verify utilization.
8. Create a recurring habit and record an occurrence.
9. Complete the daily review.
10. Switch between English, Afaan Oromoo, and Amharic.
11. Install and use the PWA on a supported browser.
12. Go offline, create a supported draft, reconnect, and verify synchronization.
13. Verify one account cannot access another account's records.
14. Export data and verify the exported records.

### Essential edge cases

- Midnight crossings.
- Daylight-saving transitions in time zones that observe them.
- Ethiopian local time and date formatting.
- Empty datasets.
- Zero income.
- Overspent budgets.
- Duplicate timer requests.
- Concurrent updates from multiple devices.
- Missing translations.
- Invalid or excessively long input.
- Network interruption during financial operations.
- Expired sessions.
- AI provider failure.
- Browser storage exhaustion.

### Release gates

A production release must not proceed if:
- Cross-user access is possible.
- Financial balances are inconsistent.
- Timer records are duplicated or irrecoverably lost.
- Critical calculations are untested.
- Database migrations fail.
- Authentication secrets are exposed.
- Backup restoration has not been validated.

---

# Part VIII — Deployment and Delivery

## 15. Environments

Maintain separate environments:

**Development**
- Local development server.
- Development database.
- Seeded sample data.
- Automated tests.

**Staging**
- Production-like configuration.
- Test accounts.
- Migration validation.
- End-to-end tests.
- PWA and responsive-layout checks.

**Production**
- Restricted production database access.
- Production authentication configuration.
- HTTPS.
- Automated backups.
- Error monitoring.
- Documented recovery procedures.

## 16. Environment variables

Create `.env.example` with placeholders, not real credentials.

Typical frontend variables:

```dotenv
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
VITE_APP_ENV=development
```

Use the current Supabase publishable-key configuration appropriate to the project. A public client key is not a substitute for RLS policies.

Server-side secrets must be configured only in the trusted server environment. Never prefix privileged secrets with `VITE_`.

## 17. CI/CD pipeline

On every pull request:
1. Install dependencies from the lockfile.
2. Run formatting and lint checks.
3. Run TypeScript checks.
4. Run unit tests.
5. Run integration tests where configured.
6. Build the production bundle.
7. Validate database migrations.
8. Run security and dependency checks.

On an approved production deployment:
1. Verify the target environment.
2. Back up or verify the current recovery point.
3. Apply reviewed migrations in a controlled order.
4. Deploy the frontend.
5. Run smoke tests.
6. Check authentication, dashboard, finance, and timer flows.
7. Monitor errors.
8. Roll back the frontend or execute the documented database recovery process if necessary.

Database rollback should not be treated as automatically safe after user data has been written. Prefer forward-compatible migrations and tested recovery procedures.

---

# Part IX — Phased Implementation Plan

## 18. Phase 0: Product foundation

Deliverables:
- Finalized product requirements.
- Wireframes and design tokens.
- Repository structure.
- Database schema and migrations.
- Authentication configuration.
- RLS policies.
- CI setup.
- Seed data and initial tests.

Exit criteria:
- The application builds.
- Users can authenticate.
- Private data is correctly isolated.
- Database migrations run reliably.

## 19. Phase 1: Core MVP

Implement:
- Today dashboard.
- Task management.
- Activity timer and manual entries.
- Financial accounts and transactions.
- Budgets.
- Habit tracking.
- Basic reports.
- English, Afaan Oromoo, and Amharic UI foundations.
- Responsive layout and installable PWA.
- Essential offline draft handling.

Exit criteria:
- A user can plan and complete a full day.
- Timer records survive refresh.
- Financial calculations match database records.
- Core journeys pass automated tests.
- Mobile and desktop layouts work.

## 20. Phase 2: Accountability and reporting

Implement:
- Reminder scheduling.
- Quiet hours and notification settings.
- Adaptive escalation rules.
- Daily and weekly reviews.
- Improved reporting and comparisons.
- CSV export.
- Synchronization conflict handling.
- Expanded integration tests.

Exit criteria:
- Completed work suppresses pending reminders.
- Quiet hours are enforced.
- Reports match the underlying records.
- Offline changes synchronize without silent data loss.

## 21. Phase 3: Goals and AI coaching

Implement:
- Goal and milestone management.
- AI summaries.
- Evidence-backed recommendations.
- Schedule proposals.
- User-approved changes.
- AI privacy controls.
- AI failure handling and usage limits.

Exit criteria:
- AI outputs are traceable to supplied data.
- AI cannot bypass authorization or modify records without approval.
- Core app functionality works with AI disabled.

## 22. Phase 4: Production hardening

Implement:
- Accessibility audit.
- Performance improvements.
- Security review.
- Backup restoration test.
- Data export and deletion verification.
- Deployment runbook.
- Monitoring and incident procedures.
- User documentation.

Exit criteria:
- All critical tests pass.
- No known cross-user authorization failures.
- Financial and timer integrity tests pass.
- Production recovery procedures are documented and validated.

---

# Part X — Master Prompt for a Coding Agent

Copy the following prompt into Codex or another capable coding agent in the project repository.

## CODING AGENT PROMPT

You are the senior software architect, senior full-stack engineer, database engineer, security engineer, and UI/UX implementation lead responsible for building DAYFORGE.

Your assignment is to implement a complete, reliable, maintainable personal life management web application using the requirements below.

Do not deliver only a mockup, a static dashboard, or a proposal. Build a working application with a real database, authentication, tested business logic, responsive screens, and documented deployment steps.

### A. Product objective

Build DAYFORGE, a personal productivity and finance platform that allows users to:
- Plan and execute daily tasks.
- Track time with start/pause/resume/stop controls.
- Record manual income and expenses.
- Manage financial accounts, budgets, and savings goals.
- Track habits and routines.
- Set long-term goals.
- Review daily, weekly, and monthly performance.
- Receive configurable accountability reminders.
- Use an optional AI coach.
- Use the application in English, Afaan Oromoo, and Amharic.
- Install the application on compatible desktop and mobile browsers.

### B. Technology requirements

Use:
- React.
- Vite.
- TypeScript.
- Tailwind CSS.
- An accessible component library or accessible reusable primitives.
- Lucide icons.
- React Hook Form.
- Zod.
- TanStack Query.
- Recharts.
- An internationalization library.
- Supabase Auth.
- Supabase PostgreSQL.
- Supabase migrations.
- Vitest.
- React Testing Library.
- Playwright.
- PWA support.

Use stable, mutually compatible dependency versions. Commit the lockfile. Avoid unnecessary dependencies.

Do not switch to a different stack without documenting a concrete technical blocker.

### C. Implementation workflow

Work in these stages.

**Stage 1 — Inspect and plan**
1. Inspect the repository and existing files.
2. Identify the framework, installed dependencies, and current application state.
3. Preserve useful existing work.
4. Write a concise implementation plan and architecture notes.
5. Identify environment variables and external setup requirements.
6. Create or update the project documentation.

**Stage 2 — Foundation**
1. Configure the application entry point, routing, layouts, and providers.
2. Implement the design tokens, typography, themes, and reusable components.
3. Configure environment validation.
4. Set up Supabase authentication.
5. Create version-controlled database migrations.
6. Implement RLS policies and test them.
7. Configure testing and CI checks.

**Stage 3 — Domain logic**
Implement shared, independently tested services for:
- Task status transitions.
- Activity timer duration and segment calculations.
- Time-zone-aware reporting periods.
- Financial ledger movements.
- Transfers, refunds, and voids.
- Budget utilization.
- Habit schedules and streaks.
- Task and habit completion rates.
- Daily and weekly report aggregation.

Keep domain calculations separate from presentation components.

**Stage 4 — Feature implementation**
Implement in this order:
1. Authentication and profile.
2. Today dashboard.
3. Task management and planner.
4. Timer and activity history.
5. Accounts and transactions.
6. Budgets.
7. Habits and routines.
8. Reports and exports.
9. Goals and daily review.
10. Reminders and adaptive accountability.
11. AI coach.
12. PWA and offline synchronization improvements.

For every feature, complete its database changes, validation, UI, loading/error/empty states, authorization, and tests before treating it as finished.

**Stage 5 — Quality assurance**
1. Run formatting, linting, TypeScript, and unit tests.
2. Run integration and end-to-end tests.
3. Test authentication and cross-user isolation.
4. Test financial calculations and timer recovery.
5. Test responsive layouts and all three languages.
6. Fix errors instead of hiding them.
7. Document any remaining limitations honestly.

**Stage 6 — Delivery**
Provide:
- Working source code.
- Database migrations.
- RLS policies.
- `.env.example`.
- Seed data suitable for development only.
- Setup instructions.
- Test commands.
- Deployment instructions.
- Architecture documentation.
- Known limitations and next steps.

Do not claim that external services are connected, migrations are deployed, tests pass, or production is live unless you have actually verified those facts.

### D. Design requirements

Create a premium, minimal, responsive interface.

Desktop:
- Collapsible sidebar.
- Main content area.
- Consistent page headers.
- Appropriate multi-column layouts.

Mobile:
- Bottom navigation.
- Touch-friendly controls.
- Single-column layouts where appropriate.
- A visible Quick Add action.
- No horizontal overflow.

Provide dark, light, and system themes.

Use restrained colors:
- Teal for successful completion.
- Indigo for time and focus.
- Amber for financial information.
- Red for errors and destructive actions.
- Neutral surfaces for ordinary content.

Use consistent spacing, typography, border radius, icon sizing, and responsive breakpoints.

Every screen must include proper loading, error, empty, and success states.

Do not use decorative statistics as if they were real data. Any sample data must be clearly marked and must never appear as actual user records.

### E. Required screens

Implement:
1. Authentication.
2. Onboarding and profile preferences.
3. Today dashboard.
4. Daily and weekly planner.
5. Task creation and editing.
6. Time tracker and activity history.
7. Finance overview.
8. Transaction creation and editing.
9. Financial account management.
10. Budget management.
11. Habit and routine management.
12. Goals and milestones.
13. Reports and analytics.
14. Daily review.
15. AI coach.
16. Notification settings.
17. Language and theme settings.
18. Data export and account deletion.

Use a consistent application shell and route structure.

### F. Database and authorization

Use PostgreSQL as the source of truth for persisted records.

Create migrations for:
- Profiles.
- Tasks.
- Activity entries and segments.
- Habits and logs.
- Routines and habit associations.
- Financial accounts.
- Transactions.
- Budgets.
- Goals and milestones.
- Daily reviews.
- Reminders.
- Optional AI conversation history.

Requirements:
- UUID primary keys.
- Foreign keys and appropriate constraints.
- Ownership fields on private records.
- RLS on every user-accessible table.
- Indexes for common query paths.
- Consistent timestamp handling.
- Safe database functions for operations requiring atomicity.
- Explicit archival and deletion behavior.

Do not rely solely on frontend filtering for security.

Validate ownership of every linked record. A task ID, goal ID, account ID, or habit ID supplied by a client must never grant access to another user's record.

Never expose privileged database credentials to the browser.

### G. Timer requirements

Implement a robust timer state model.

The browser's interval counter is for display only. Persist start timestamps and time segments so the correct duration can be reconstructed after refresh or restart.

Handle:
- Start.
- Pause.
- Resume.
- Stop.
- Edit.
- Recover after reload.
- Duplicate-click prevention.
- Concurrent requests.
- Offline state.
- Overlap detection.

Use a concurrency-safe backend or database constraint to prevent more than one active timer per user if that is the selected product rule.

Do not silently discard time entries when overlaps are detected. Present an explicit resolution workflow.

### H. Finance requirements

Implement a consistent ledger model.

Support:
- Income.
- Expenses.
- Refunds.
- Transfers.
- Account balances.
- Opening balances.
- Budgets.
- Category-based spending.
- Savings goals.

Store monetary amounts in integer minor units and apply a documented currency-precision policy.

Use database transactions for related financial operations.

Do not count transfers as income or expenses. Ensure refund, void, and reversal behavior is consistent across account balances and reports.

Do not use JavaScript floating-point arithmetic as the authoritative financial calculation method.

### I. Reporting requirements

Create tested shared calculation functions.

Report:
- Completed tasks and completion rates.
- Estimated versus actual duration.
- Time allocation.
- Time tracking coverage.
- Expenses by category.
- Budget utilization.
- Income and expenses.
- Net cash flow.
- Habit consistency.
- Goal progress.

Define reporting-period boundaries using the user's time zone.

Distinguish zero values from missing values. Do not infer productivity or waste from untracked time.

Allow filtering by date range and exporting applicable data.

### J. Accountability requirements

Implement user-configurable reminders.

Support:
- Task reminders.
- Habit reminders.
- Daily review reminders.
- Quiet hours.
- Snoozing and dismissal.
- Duplicate suppression.
- Escalation limits.
- Completion-aware cancellation.

Escalation should increase the usefulness or salience of a reminder, not become punitive.

Do not create financial penalties, shame-based messaging, or irreversible consequences for missed tasks.

### K. AI coach requirements

Build the AI coach as a separately configured, optional service.

Use a trusted server-side integration for model API calls. Keep provider credentials out of the frontend.

Features:
- Daily and weekly summaries.
- Evidence-based recommendations.
- Schedule proposals.
- Habit suggestions.
- Budget suggestions.
- Explanations of patterns in recorded data.

Pass only the necessary data for the user's request.

Return structured recommendations where practical, with evidence references and proposed actions.

Require explicit confirmation before changing user records.

Do not allow arbitrary SQL execution, unrestricted tool use, or direct destructive actions by the model.

Provide loading, failure, cancellation, privacy, and usage-limit handling.

When no AI credentials are configured, the rest of the application must still run correctly. Clearly label the AI feature as unconfigured rather than pretending it works.

### L. Multilingual requirements

Provide English (`en`), Afaan Oromoo (`om`), and Amharic (`am`).

Use translation resource files. Never scatter hardcoded user-facing strings across components.

Translate:
- Navigation.
- Forms.
- Validation.
- Buttons.
- Empty states.
- Notifications.
- Reports.
- Settings.
- Critical error messages.

Support Ethiopic-script text and locale-aware formatting.

Keep date storage, timestamps, currencies, and translated labels separate.

Do not fabricate translations for complex financial or legal language. Keep translations consistent and reviewable.

### M. PWA and offline requirements

Implement:
- Valid manifest.
- Application icons and install metadata.
- Service-worker caching of static assets.
- Offline status indication.
- Draft persistence.
- Explicit synchronization state.
- Safe retry behavior.
- Duplicate prevention.
- Conflict detection.

Never tell the user that data is saved to the server while it exists only locally.

Avoid caching sensitive private API responses in an unprotected shared cache.

### N. Required automated tests

At minimum, test:
- Domain calculations.
- Task status transitions.
- Timer pause/resume and reload recovery.
- Duplicate timer requests.
- Financial transfers.
- Refunds and voids.
- Budget boundaries.
- Habit scheduling.
- Report date ranges.
- Authentication.
- RLS and cross-user isolation.
- Reminder idempotency.
- Locale switching.
- Offline draft synchronization.
- AI failure handling.

Create Playwright flows for the most important user journeys.

Use deterministic test fixtures. Do not rely on real financial accounts or production data.

### O. Coding standards

- Use strict TypeScript.
- Avoid `any` unless explicitly justified.
- Keep components focused and reusable.
- Avoid giant page components.
- Separate domain logic from UI.
- Validate external and user-provided data.
- Use accessible semantic elements.
- Avoid hardcoded secrets and production sample records.
- Provide meaningful error messages.
- Keep dependencies and configuration understandable.
- Document non-obvious business rules.
- Do not suppress TypeScript or lint errors to make a build pass.
- Do not leave critical features as nonfunctional placeholder buttons.

### P. Definition of done

The project is not complete merely because the home page renders.

A feature is complete only when:
1. Its UI works.
2. Its data model and persistence work.
3. Authorization is enforced.
4. Validation is implemented.
5. Loading, empty, and error states exist.
6. Important edge cases are handled.
7. Relevant automated tests pass.
8. The feature works on desktop and mobile.
9. Translations are present.
10. Documentation is updated.

At the end of each implementation phase, report:
- What was implemented.
- Which files were created or modified.
- Database migrations added.
- Tests run and their actual results.
- Commands needed to run the application.
- Required environment variables.
- Remaining blockers and known limitations.

Begin by inspecting the repository and preparing the implementation plan. Then proceed with the first working vertical slice: authentication, protected dashboard, database migrations, RLS, task creation, and reliable time tracking.

Implement the real application incrementally. Do not stop after writing a plan or generating a static UI. Do not claim successful deployment without verification.

## END OF CODING AGENT PROMPT

---

# Final delivery checklist

Before calling DAYFORGE ready for personal use, verify the following:

- [ ] A user can register and sign in.
- [ ] The Today dashboard displays real database records.
- [ ] Tasks can be created, edited, completed, and postponed.
- [ ] Timers survive page refresh and produce accurate durations.
- [ ] Manual income, expenses, refunds, and transfers work.
- [ ] Account balances and budget calculations are consistent.
- [ ] Habit schedules and logs work correctly.
- [ ] Reports match the underlying records.
- [ ] English, Afaan Oromoo, and Amharic interfaces work.
- [ ] The application installs on supported desktop and mobile browsers.
- [ ] Offline behavior and synchronization are clearly communicated.
- [ ] RLS prevents access to other users' data.
- [ ] AI recommendations require approval before modifying records.
- [ ] Critical tests pass.
- [ ] Backups and restoration procedures are verified.
- [ ] The deployment instructions are reproducible.

**Recommended first milestone:** Build authentication, the Today dashboard, task management, the activity timer, and manual expense logging. Once these five workflows are reliable, expand into budgets, habits, reporting, adaptive accountability, and AI coaching. This keeps the project achievable while preserving the architecture needed for the complete product.
