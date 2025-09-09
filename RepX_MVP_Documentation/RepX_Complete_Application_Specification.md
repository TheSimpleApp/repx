# RepX - Complete Application Specification
**The Definitive Guide to Building RepX MVP - Mobile-First Sales Rep Success Platform**

---

# 📖 Table of Contents

1. [App Overview & Vision](#app-overview--vision)
2. [Core Systems Architecture](#core-systems-architecture) 
3. [User Personas & Stories](#user-personas--stories)
4. [Database Schema & Data Models](#database-schema--data-models)
5. [UI/UX Design Guidelines](#uiux-design-guidelines)
6. [Screen Specifications](#screen-specifications)
7. [User Flows & Interactions](#user-flows--interactions)
8. [Technical Architecture](#technical-architecture)
9. [Sample Data & Scenarios](#sample-data--scenarios)
10. [Implementation Guidelines](#implementation-guidelines)

---

# 🎯 App Overview & Vision

## Product Name: RepX
**Tagline**: "Turn every new hire into a successful recruiter"

## Core Mission
RepX is a mobile-first app that uses Tinder-like contact swiping to turn new sales reps' personal networks into recruits and customers, while delivering 89% retention through a gamified 28-day onboarding program that gets reps their first win within 14 days.

## Value Proposition
- **Contact Mining**: Transform overwhelming contact lists into structured business opportunities
- **89% Retention**: Increase from industry standard 60% to 89% through first customer wins
- **Automated Recruiting**: Turn every new rep's personal contacts into business value
- **Structured Success**: 28-day gamified program with immediate cash rewards

## Target Market
- **Primary**: Direct-to-door (D2D) sales companies with high turnover
- **Company Size**: 10-500 sales reps  
- **Industry**: Solar, home improvement, security, telecommunications
- **Pain Point**: $15,000+ cost per failed new hire, 60% first-year turnover

## Business Model
- **SaaS Pricing**: $99-199 per rep per month
- **Value Replacement**: Replaces traditional recruiting costs ($15K → $3K per hire)
- **ROI**: 5x improvement in training cost effectiveness
- **Growth**: Network effects as each rep brings 500+ contacts

---

# 🏗️ Core Systems Architecture

RepX consists of **4 integrated systems** working together to transform new sales reps:

## System 1: Contact Swiping System (Primary Feature)
**Purpose**: Tinder-like interface to mine personal contacts for business opportunities

### Core Features:
- **Contact Import**: Secure sync of phone contacts (iOS/Android)
- **Swipe Interface**: 
  - Left Swipe (❌): Pass/Skip contact
  - Right Swipe (✅): Yes/Interested → Select prospect type
  - Up Swipe (⭐): Super Swipe/Star → High potential → Select prospect type
- **Prospect Type Selection**: Modal with 3 options:
  - **Recruit**: Potential new team member
  - **Customer**: Potential sale opportunity  
  - **Both**: Could be either/both
- **Progress Tracking**: Visual progress through contact list (X of Y processed)
- **Session Management**: Batch processing with break points

### Key Metrics:
- Target: 95% of contacts processed within 30 days
- Average: 30-50 contacts per session
- Conversion: 15% of contacts become prospects

## System 2: Recruiting Gamification (6 Tiers Total)
**Purpose**: Gamify the recruiting process with company-customizable rewards

### Tier Structure:
#### 3 Tiers for Recruits Submitted:
- **Tier 1**: 5 submits → Premium Work Shirt (example)
- **Tier 2**: 10 submits → $50 Gift Card (example)
- **Tier 3**: 15 submits → $500 Exclusive Experience (example)

#### 3 Tiers for Recruits Hired:
- **Tier 1**: 1 hire → [Company Custom Reward]
- **Tier 2**: 3 hires → [Experience/Premium Item]
- **Tier 3**: 5 hires → Access to Annual Company Trip

### Company Customization:
- Companies set BOTH the quantity thresholds AND the reward types
- Rewards can be: Cash bonuses, physical items, experiences, access/privileges
- Fully configurable tier progression and requirements

### Core Features:
- **Auto-Submission**: Contacts swiped as "Recruit" automatically create submissions
- **Status Tracking**: Company updates recruit status (Submitted → Contacted → Interview → Hired)
- **Achievement Celebrations**: Full-screen celebrations when tiers are achieved
- **Progress Visualization**: Clear progress bars toward next tier
- **Reward Claiming**: Workflow for claiming and receiving rewards

## System 3: 28-Day Ramp Program (Structured Success)
**Purpose**: Guide new reps through critical first 28 days with cash rewards

### Program Structure:
#### Weeks 1-2: Foundation Tasks (Rep Has Full Control)
- Tasks completely within rep's control to build confidence
- Examples: Door knocks, training completion, meeting attendance
- **Reward Type**: Points OR cash for each task completion
- **Success Rate**: Target 90%+ completion

#### Weeks 3-4: Outcome Tasks (Results-Based)
- Tasks based on business outcomes and opportunities created
- Examples: Demos scheduled, inspections set, referrals generated
- **Reward Type**: Higher points OR cash values
- **Success Rate**: Target 75%+ completion

### Task Configuration:
- **Company Customizable**: Each company designs their own 28-day program
- **Task Examples** (from user's data):
  - Tier 1 ($500): 100 contacts, Course 1-3, Pitch, 1 inspection
  - Tier 2 ($500): 500 contacts, Course 4-6, Presentation, 3 inspections, Attend Install
  - Tier 3 ($1000): 1000 contacts, Course 7-10, Closing, 7 inspections, Read ABC's of Closing

### Core Features:
- **Daily Task Management**: Checkbox-style task completion
- **Verification Methods**: Self-report, photo upload, GPS verification, manager confirm
- **Progress Tracking**: Visual progress through 4-week program
- **Cash Rewards**: Immediate cash payments for task completion
- **Weekly Milestones**: Celebrations for week completion
- **Program Completion**: Major celebration for 28-day completion

## System 4: Lead Tracker & Fast Start (Customer Development)
**Purpose**: Convert contact prospects into customers for retention success

### Lead Tracker Features:
- **Auto-Creation**: Contacts swiped as "Customer" become leads
- **Status Management**: Prospect → Contacted → Opportunity → Customer
- **Contact Methods**: Call, text, email tracking
- **Opportunity Scheduling**: Demo, inspection, consultation scheduling
- **Conversion Tracking**: First customer win celebration (89% retention trigger)

### 14-Day Fast Start Program (Optional):
- **Time Limit**: Only valid for first 14 days of new rep
- **Focus**: Opportunities created (demos, inspections, consultations)
- **5 Tiers**: Company-customizable tier system for speed achievements
- **Leaderboard**: Permanent leaderboard showing Fast Start graduates
- **Rewards**: Points OR cash tied to tier achievements

### Key Success Metric:
- **Target**: 75% of reps get first customer within 14 days
- **Impact**: Achieving first customer win = 89% retention rate
- **Method**: Systematic approach to personal contact conversion

---

# 👥 User Personas & Stories

## Primary User: New Sales Representative
RepX focuses on ONE user type - new sales reps during their critical first 28+ days. No complex multi-user systems, HR dashboards, or manager interfaces in MVP.

### Persona 1: John Mitchell (Week 3 Rep)
- **Profile**: 25-year-old, new to D2D solar sales, tech-comfortable
- **Company**: ABC Solar (mid-size company, 50 reps)
- **Program Status**: Day 18 of 28-day program, Week 3 (outcome tasks)
- **Contact Progress**: 347/523 contacts swiped (66% complete)
  - 89 potential customers identified
  - 67 potential recruits submitted
- **Recruiting Game**: 
  - Tier 1 achieved (5 submits) - received company shirt
  - Tier 2 progress: 7/10 submits (70% toward $50 gift card)
  - 1 recruit hired (achieved first hire tier)
- **28-Day Program**:
  - Week 1-2: All foundation tasks completed ($350 earned)
  - Week 3: 2/4 outcome tasks complete ($125 earned, $150 pending)
  - Total cash: $475 earned
- **Customer Success**: First customer (Mike Chen) signed yesterday - major celebration
- **Behavior**: Consistent daily app usage, processes 30-50 contacts per session
- **Goals**: Complete 28-day program, reach Tier 2 recruiting reward, get 2nd customer

### Persona 2: Maria Santos (Week 1 Rep)
- **Profile**: 32-year-old, new to sales, switching from retail management
- **Company**: XYZ Home Security (smaller company, 15 reps)
- **Program Status**: Day 5 of 28-day program, Week 1 (foundation tasks)
- **Contact Progress**: 89/456 contacts swiped (19% complete)
  - 23 potential customers identified  
  - 18 potential recruits submitted
- **Recruiting Game**:
  - Working toward Tier 1 (3/5 submits needed)
  - No hires yet
- **28-Day Program**:
  - Week 1: 3/5 foundation tasks complete ($85 earned)
  - Current tasks: Training modules, door knocking quotas
- **Customer Success**: 2 customer leads contacted, 1 demo scheduled
- **Behavior**: Learning the system, processing 20-30 contacts daily
- **Goals**: Complete first week, achieve first tier, schedule first demo

### User Story Examples:

#### Contact Swiping Stories:
- **US-01**: As a new rep, I want to import my phone contacts so I can identify business opportunities from my personal network
- **US-02**: As a new rep, I want to swipe through contacts like a dating app so I can quickly categorize them as prospects
- **US-03**: As a new rep, I want to select prospect type (recruit/customer/both) so I can properly categorize opportunities
- **US-04**: As a new rep, I want to see my progress through contact processing so I stay motivated to complete the task
- **US-05**: As a new rep, I want to super-swipe high-potential contacts so I can prioritize my best opportunities

#### Recruiting Game Stories:
- **US-06**: As a new rep, I want to see my recruiting tier progress so I know how close I am to earning rewards
- **US-07**: As a new rep, I want full-screen celebrations when I achieve tiers so I feel recognized for my efforts
- **US-08**: As a new rep, I want to track my submitted recruits' status so I know their progress through hiring
- **US-09**: As a new rep, I want to claim my tier rewards easily so I can receive what I've earned
- **US-10**: As a new rep, I want to see recent recruiting activity so I stay engaged with the process

#### 28-Day Program Stories:
- **US-11**: As a new rep, I want to see my current week's tasks so I know what to focus on today
- **US-12**: As a new rep, I want to mark tasks complete and earn cash immediately so I get instant gratification
- **US-13**: As a new rep, I want to track my cash earnings so I see the financial benefit of the program
- **US-14**: As a new rep, I want weekly milestone celebrations so I feel accomplished for completing phases
- **US-15**: As a new rep, I want to see my overall program progress so I understand how much I've accomplished

#### Lead Tracker Stories:
- **US-16**: As a new rep, I want customer prospects automatically created from my swipes so I don't lose opportunities
- **US-17**: As a new rep, I want to track my customer lead status so I can follow up systematically
- **US-18**: As a new rep, I want to schedule opportunities (demos/inspections) so I can convert leads
- **US-19**: As a new rep, I want a major celebration when I win my first customer so I feel successful
- **US-20**: As a new rep, I want to participate in Fast Start competition so I can achieve quick wins

---

# 🗄️ Database Schema & Data Models

## Database Choice: Supabase PostgreSQL
- **Reason**: FlutterFlow integration, real-time capabilities, row-level security
- **Architecture**: Single-tenant with company isolation via Row Level Security (RLS)

## Core Entity Relationships:
```
Company (1) ←→ (Many) Users
Company (1) ←→ (Many) RecruitingTiers  
Company (1) ←→ (Many) RampTasks
User (1) ←→ (Many) Contacts
User (1) ←→ (Many) ContactSwipes
User (1) ←→ (Many) CustomerLeads
User (1) ←→ (Many) TaskProgress
```

## Table Specifications:

### companies
```sql
CREATE TABLE companies (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  industry VARCHAR(100),
  
  -- Contact swiping settings
  enable_contact_import BOOLEAN DEFAULT true,
  contact_privacy_policy TEXT,
  
  -- Program settings
  program_duration_days INTEGER DEFAULT 28,
  enable_fast_start BOOLEAN DEFAULT true,
  fast_start_duration_days INTEGER DEFAULT 14,
  
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### users (Sales Reps)
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  company_id UUID REFERENCES companies(id) ON DELETE CASCADE,
  
  -- User info
  email VARCHAR(255) UNIQUE NOT NULL,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  phone VARCHAR(20),
  
  -- Rep-specific info  
  hire_date DATE NOT NULL,
  manager_email VARCHAR(255),
  territory VARCHAR(100),
  
  -- Program progress
  program_start_date DATE DEFAULT CURRENT_DATE,
  current_program_day INTEGER DEFAULT 1,
  program_completed BOOLEAN DEFAULT false,
  program_completion_date DATE,
  
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### contacts (Encrypted Personal Contacts)
```sql
CREATE TABLE contacts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  
  -- Contact info (encrypted for privacy)
  name_encrypted BYTEA NOT NULL,
  phone_encrypted BYTEA,
  email_encrypted BYTEA,
  
  -- Contact metadata
  has_phone BOOLEAN DEFAULT false,
  has_email BOOLEAN DEFAULT false,
  contact_source VARCHAR(50) DEFAULT 'phone',
  
  is_processed BOOLEAN DEFAULT false,
  processed_at TIMESTAMP WITH TIME ZONE,
  
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### contact_swipes (Swipe Decisions)
```sql
CREATE TABLE contact_swipes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  contact_id UUID REFERENCES contacts(id) ON DELETE CASCADE,
  
  -- Swipe action
  swipe_direction VARCHAR(10) NOT NULL, -- 'left', 'right', 'up'
  swipe_result VARCHAR(10) NOT NULL, -- 'pass', 'yes', 'super'
  
  -- Prospect categorization (if not 'pass')
  prospect_type VARCHAR(20), -- 'recruit', 'customer', 'both'
  quality_rating INTEGER, -- 1-5 (for super swipes)
  
  -- Follow-up tracking
  contacted BOOLEAN DEFAULT false,
  contact_method VARCHAR(50),
  contact_date DATE,
  response_status VARCHAR(20), -- 'interested', 'not_interested', 'no_response'
  
  swiped_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  
  UNIQUE(user_id, contact_id)
);
```

### recruiting_tiers (Company-Customizable Tiers)
```sql
CREATE TABLE recruiting_tiers (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  company_id UUID REFERENCES companies(id) ON DELETE CASCADE,
  
  -- Tier configuration
  tier_type VARCHAR(20) NOT NULL, -- 'submissions' or 'hires'
  tier_number INTEGER NOT NULL, -- 1, 2, 3
  quantity_required INTEGER NOT NULL,
  
  -- Reward configuration
  reward_title VARCHAR(255) NOT NULL, -- "Premium Work Shirt", "$50 Gift Card"
  reward_description TEXT,
  reward_value_usd DECIMAL(10,2),
  reward_type VARCHAR(50), -- 'physical', 'cash', 'experience', 'access'
  
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  
  UNIQUE(company_id, tier_type, tier_number)
);
```

### recruit_submissions (Recruiting Prospects)
```sql
CREATE TABLE recruit_submissions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  contact_swipe_id UUID REFERENCES contact_swipes(id),
  
  -- Submission details
  prospect_name_encrypted BYTEA NOT NULL,
  prospect_phone_encrypted BYTEA,
  prospect_email_encrypted BYTEA,
  
  -- Company processing
  company_status VARCHAR(20) DEFAULT 'submitted', 
  -- 'submitted', 'contacted', 'interview_scheduled', 'hired', 'not_hired'
  status_updated_at TIMESTAMP WITH TIME ZONE,
  status_notes TEXT,
  
  -- Hire details (if hired)
  hire_date DATE,
  hire_position VARCHAR(100),
  
  submitted_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### ramp_tasks (28-Day Program Tasks)
```sql
CREATE TABLE ramp_tasks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  company_id UUID REFERENCES companies(id) ON DELETE CASCADE,
  
  -- Task configuration
  title VARCHAR(255) NOT NULL,
  description TEXT,
  week_number INTEGER NOT NULL, -- 1, 2, 3, 4
  task_type VARCHAR(20) NOT NULL, -- 'foundation' (weeks 1-2), 'outcome' (weeks 3-4)
  
  -- Completion requirements
  quantity_required INTEGER DEFAULT 1,
  verification_method VARCHAR(50), -- 'self_report', 'photo', 'gps', 'manager_confirm'
  
  -- Reward configuration  
  cash_reward_usd DECIMAL(10,2) DEFAULT 0,
  points_reward INTEGER DEFAULT 0,
  
  -- Task settings
  is_required BOOLEAN DEFAULT true,
  is_active BOOLEAN DEFAULT true,
  sort_order INTEGER DEFAULT 0,
  
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### task_progress (Individual Task Completion)
```sql
CREATE TABLE task_progress (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  ramp_task_id UUID REFERENCES ramp_tasks(id),
  
  -- Completion details
  quantity_completed INTEGER DEFAULT 0,
  is_completed BOOLEAN DEFAULT false,
  completed_at TIMESTAMP WITH TIME ZONE,
  
  -- Verification
  verification_data JSONB, -- photos, GPS, etc.
  verification_status VARCHAR(20) DEFAULT 'pending',
  verified_at TIMESTAMP WITH TIME ZONE,
  
  -- Reward payout
  reward_status VARCHAR(20) DEFAULT 'pending', -- 'pending', 'paid', 'cancelled'  
  reward_paid_at TIMESTAMP WITH TIME ZONE,
  reward_amount_usd DECIMAL(10,2),
  
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  
  UNIQUE(user_id, ramp_task_id)
);
```

### customer_leads (Customer Prospects & Opportunities)
```sql
CREATE TABLE customer_leads (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  contact_swipe_id UUID REFERENCES contact_swipes(id),
  
  -- Lead details
  lead_name_encrypted BYTEA NOT NULL,
  lead_phone_encrypted BYTEA,
  lead_email_encrypted BYTEA,
  
  -- Lead status  
  status VARCHAR(20) DEFAULT 'prospect', 
  -- 'prospect', 'contacted', 'opportunity', 'customer', 'lost'
  
  -- Opportunity tracking
  opportunity_type VARCHAR(100), -- 'demo', 'inspection', etc.
  opportunity_date DATE,
  opportunity_notes TEXT,
  
  -- Customer conversion
  became_customer BOOLEAN DEFAULT false,
  customer_date DATE,
  customer_value_usd DECIMAL(10,2),
  
  -- Fast start tracking
  counts_for_fast_start BOOLEAN DEFAULT true,
  fast_start_day INTEGER, -- Which day of program this was created
  
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### rep_progress (Overall Progress Tracking)
```sql
CREATE TABLE rep_progress (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  
  -- Contact swiping progress
  contacts_imported INTEGER DEFAULT 0,
  contacts_processed INTEGER DEFAULT 0,
  contacts_total INTEGER DEFAULT 0,
  
  -- Recruiting progress
  recruits_submitted INTEGER DEFAULT 0,
  recruits_hired INTEGER DEFAULT 0,
  
  -- Customer progress
  customers_identified INTEGER DEFAULT 0,
  opportunities_created INTEGER DEFAULT 0,
  first_customer_won BOOLEAN DEFAULT false,
  first_customer_date DATE,
  
  -- Program progress
  tasks_completed INTEGER DEFAULT 0,
  cash_earned DECIMAL(10,2) DEFAULT 0,
  points_earned INTEGER DEFAULT 0,
  
  -- Fast start progress
  fast_start_opportunities INTEGER DEFAULT 0,
  fast_start_tier INTEGER DEFAULT 0,
  
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

---

# 🎨 UI/UX Design Guidelines

## Core Design Principles

### Mobile-First Philosophy
- **Target Device**: iPhone/Android smartphones (primary usage)
- **Field Environment**: Designed for use outdoors, in cars, various lighting
- **One-Handed Usage**: All primary actions within thumb reach
- **Portrait Optimization**: Vertical layout for mobile comfort
- **Offline-First**: Core features work without internet connection

### Gamification-Focused Design
- **Immediate Gratification**: Instant visual feedback for every action
- **Achievement Celebrations**: Full-screen celebrations with animations
- **Progress Visualization**: Multiple progress bars and completion metrics
- **Success Reinforcement**: 89% retention messaging throughout
- **Reward Emphasis**: Cash values and rewards prominently displayed

### Tinder-Like Interaction Model
- **Swipe-First**: Contact swiping as primary interface pattern
- **Card-Based UI**: Contact cards, tier cards, task cards
- **Gesture-Heavy**: Swipe, tap, hold interactions
- **Visual Feedback**: Immediate response to swipe gestures

## Color System (Gamified)

### Primary Colors:
```css
/* Success & Achievement */
--repx-success: #16a34a        /* Green - completed, wins */
--repx-tier-gold: #eab308      /* Gold - tier achievements, stars */
--repx-cash-green: #059669     /* Money green - cash rewards */

/* Action Colors */  
--repx-swipe-right: #16a34a    /* Green - yes/recruit/customer */
--repx-swipe-left: #dc2626     /* Red - pass/no */
--repx-super-swipe: #eab308    /* Gold - star/super swipe */

/* System Colors */
--repx-primary: #2563eb        /* Blue - primary actions */
--repx-progress: #3b82f6       /* Light blue - progress bars */
--repx-background: #ffffff     /* White - clean background */
--repx-surface: #f8fafc        /* Very light gray - cards */
--repx-border: #e2e8f0         /* Light gray - borders */

/* Status Colors */
--repx-pending: #d97706        /* Amber - pending/in-progress */
--repx-error: #dc2626          /* Red - errors/failed */
--repx-muted: #94a3b8          /* Gray - disabled/inactive */
```

## Typography Scale (Mobile-Optimized)

### Font Hierarchy:
```css
/* Contact Names (Swipe Interface) */
.text-contact-name: 24px, font-weight: 600, line-height: 1.4

/* Tier Rewards & Cash Amounts */
.text-reward: 20px, font-weight: 700, line-height: 1.3

/* Task Titles & Section Headers */
.text-section: 18px, font-weight: 500, line-height: 1.4

/* Body Text & Descriptions */
.text-body: 16px, font-weight: 400, line-height: 1.5

/* Helper Text & Labels */
.text-helper: 14px, font-weight: 400, line-height: 1.4

/* Button Text */
.text-button: 16px, font-weight: 500, line-height: 1.2
```

## Spacing System (Thumb-Friendly)

### Base Grid: 8px system
```css
/* Touch Targets */
.touch-min: 56px          /* Minimum touch target size */
.touch-preferred: 64px    /* Preferred touch target size */

/* Content Spacing */
.space-xs: 4px           /* Tight spacing */
.space-sm: 8px           /* Small spacing */
.space-md: 16px          /* Default spacing */
.space-lg: 24px          /* Large spacing */
.space-xl: 32px          /* Extra large spacing */

/* Container Padding */
.container-padding: 16px  /* Minimum screen padding */
.card-padding: 24px      /* Internal card padding */

/* Navigation */
.tab-height: 80px        /* Bottom tab bar height */
.swipe-button: 64px      /* Swipe action button size */
```

## Component Specifications

### Contact Swipe Cards
```css
.contact-card {
  width: 100% - 32px;      /* Full width minus margins */
  height: 400px;           /* Fixed height for consistency */
  border-radius: 20px;     /* Rounded corners */
  background: white;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  padding: 24px;
  margin: 16px;
}

.contact-name {
  font-size: 24px;
  font-weight: 600;
  text-align: center;
  margin-bottom: 8px;
}

.contact-phone {
  font-size: 16px;
  color: #6b7280;
  text-align: center;
}
```

### Swipe Action Buttons
```css
.swipe-buttons {
  display: flex;
  justify-content: center;
  gap: 32px;
  margin-top: 24px;
}

.swipe-btn-pass {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  background: #dc2626;
  color: white;
}

.swipe-btn-super {
  width: 72px;
  height: 72px;
  border-radius: 50%;
  background: #eab308;
  color: white;
}

.swipe-btn-yes {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  background: #16a34a;
  color: white;
}
```

### Recruiting Tier Cards
```css
.tier-card {
  background: linear-gradient(90deg, #f8fafc 0%, #ffffff 100%);
  border-left: 4px solid #eab308;
  border-radius: 12px;
  padding: 20px;
  margin-bottom: 12px;
}

.tier-achieved {
  border-left-color: #16a34a;
  background: linear-gradient(90deg, #dcfce7 0%, #ffffff 100%);
}

.tier-progress-bar {
  height: 12px;
  background: #e2e8f0;
  border-radius: 6px;
  overflow: hidden;
}

.tier-progress-fill {
  height: 100%;
  background: #eab308;
  transition: width 0.3s ease;
}
```

### Task Completion Cards
```css
.task-card {
  border: 1px solid #e2e8f0;
  border-left: 4px solid #3b82f6;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 12px;
}

.task-completed {
  border-left-color: #16a34a;
  background: #f0f9f4;
}

.cash-reward {
  font-size: 18px;
  font-weight: 600;
  color: #059669;
}
```

### Bottom Navigation
```css
.bottom-nav {
  height: 80px;
  background: white;
  border-top: 1px solid #e2e8f0;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 100;
}

.tab-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 56px;
}

.tab-icon {
  width: 24px;
  height: 24px;
  margin-bottom: 4px;
}

.tab-label {
  font-size: 12px;
  font-weight: 500;
}
```

---

# 📱 Screen Specifications

## Navigation Structure: 4-Tab System

```
┌─────────────────────────────────────────┐
│              RepX App Bar                │
├─────────────────────────────────────────┤
│                                         │
│            Screen Content               │
│                                         │
├─────────────────────────────────────────┤
│  📱      🎯      📈      👤           │
│Contacts Recruit Progress Profile       │
└─────────────────────────────────────────┘
```

## Screen 1: Contacts Tab (Primary Feature)

### Purpose: 
Tinder-like contact swiping interface where reps categorize personal contacts

### Layout:
```
┌─────────────────────────────────────┐
│  RepX Logo    147/523    Import     │ ← App Bar
├─────────────────────────────────────┤
│  ┌─────────────────────────────┐   │ ← Contact Card
│  │                             │   │
│  │      Sarah Johnson          │   │ ← Name (24px, bold)
│  │    (555) 123-4567          │   │ ← Phone
│  │                             │   │
│  │   Known from: College       │   │ ← Context
│  │                             │   │
│  │     Swipe or tap below      │   │ ← Instructions
│  │                             │   │
│  └─────────────────────────────┘   │
│                                     │
│     ❌        ⭐        ✅        │ ← Action Buttons
│    Pass     Super      Yes        │   (56-72px)
│                                     │
│  Progress: ████████░░░ 28%         │ ← Progress Bar
│                                     │
│  Today: 23 processed               │ ← Session Stats
│  • 6 Customers • 4 Recruits       │
│                                     │
├─────────────────────────────────────┤
│  📱  🎯  📈  👤                  │ ← Bottom Nav
└─────────────────────────────────────┘
```

### Key Interactions:
1. **Left Swipe/❌**: Pass contact → Next contact loads
2. **Right Swipe/✅**: Opens Prospect Type Modal
3. **Up Swipe/⭐**: Opens Prospect Type Modal (high priority)

### Prospect Type Modal:
```
┌─────────────────────────────────────┐
│  What type of prospect is Sarah?    │
├─────────────────────────────────────┤
│  ┌─────────────┐ ┌─────────────┐   │
│  │   🎯        │ │   🛍️        │   │
│  │ RECRUIT     │ │ CUSTOMER    │   │
│  └─────────────┘ └─────────────┘   │
│                                     │
│  ┌───────────────────────────────┐ │
│  │         🎯🛍️ BOTH            │ │
│  └───────────────────────────────┘ │
│        [Cancel] [Select]            │
└─────────────────────────────────────┘
```

## Screen 2: Recruit Tab (Gamification Hub)

### Purpose:
6-tier recruiting game showing progress and achievements

### Layout:
```
┌─────────────────────────────────────┐
│  Recruiting Game           🏆       │ ← App Bar
├─────────────────────────────────────┤
│  ┌─────────────────────────────┐   │ ← Progress Card
│  │  7 Submitted  •  1 Hired    │   │ ← Key Numbers
│  │                             │   │
│  │  Next: 3 more for $50       │   │ ← Next Reward
│  │  ██████████░░░░ 70%         │   │ ← Progress
│  └─────────────────────────────┘   │
│                                     │
│  RECRUIT SUBMISSIONS               │ ← Section
│  ┌─────────────────────────────┐   │
│  │ ✅ TIER 1 - Work Shirt      │   │ ← Achieved
│  │    5/5 submits • DONE!      │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ ⏳ TIER 2 - $50 Gift Card   │   │ ← In Progress
│  │    7/10 submits             │   │
│  │    ████████░░░░░░░░░ 70%    │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ 🔒 TIER 3 - $500 Experience │   │ ← Locked
│  │    0/15 submits             │   │
│  └─────────────────────────────┘   │
│                                     │
│  RECRUIT HIRES                     │ ← Section
│  ┌─────────────────────────────┐   │
│  │ ✅ TIER 1 - Bonus           │   │ ← Achieved Hire
│  │    1/1 hire • DONE!         │   │
│  └─────────────────────────────┘   │
│                                     │
│  Recent: John Smith hired! 🎉      │ ← Activity
│                                     │
├─────────────────────────────────────┤
│  📱  🎯  📈  👤                  │ ← Bottom Nav
└─────────────────────────────────────┘
```

### Achievement Modal:
```
┌─────────────────────────────────────┐
│        🎉 TIER 2 ACHIEVED! 🎉       │ ← Celebration
│                                     │
│            🏆                       │ ← Trophy (large)
│                                     │
│         $50 Gift Card               │ ← Reward
│         UNLOCKED!                   │
│                                     │
│  ┌───────────────────────────────┐ │
│  │      Claim Your Reward        │ │ ← CTA
│  └───────────────────────────────┘ │
└─────────────────────────────────────┘
```

## Screen 3: Progress Tab (28-Day Program & Leads)

### Purpose:
Track 28-day program tasks and customer lead development

### Layout:
```
┌─────────────────────────────────────┐
│  My Progress     Day 18/28    📅    │ ← App Bar
├─────────────────────────────────────┤
│  ┌─────────────────────────────┐   │ ← Program Card
│  │  Week 3 of 4 - Outcomes     │   │ ← Status
│  │  ████████████░░░░░░░ 64%    │   │
│  │                             │   │
│  │  💰 $475 earned so far      │   │ ← Cash (prominent)
│  │  $150 pending this week     │   │
│  └─────────────────────────────┘   │
│                                     │
│  THIS WEEK'S TASKS                 │ ← Section
│  ┌─────────────────────────────┐   │
│  │ ✅ Set 3 demos      +$50    │   │ ← Complete
│  │    Completed yesterday      │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ ⏳ Get 2 referrals  +$40    │   │ ← In Progress
│  │    1/2 complete             │   │
│  │    [Mark Complete]          │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ 📝 5 inspections    +$75    │   │ ← Pending
│  │    [Mark Complete]          │   │
│  └─────────────────────────────┘   │
│                                     │
│  MY CUSTOMER LEADS                 │ ← Section  
│  ┌─────────────────────────────┐   │
│  │ ⭐ Mike Chen (CUSTOMER!)    │   │ ← First Win!
│  │    WON! Signed yesterday    │   │
│  │    Your first customer! 🎉  │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ 🛍️ Sarah Johnson           │   │ ← Active Lead
│  │    Demo scheduled Thu 2pm   │   │
│  └─────────────────────────────┘   │
│                                     │
│  ⚡ FAST START COMPLETE             │ ← Fast Start
│  Tier 2 achieved in 14 days!       │
│                                     │
├─────────────────────────────────────┤
│  📱  🎯  📈  👤                  │ ← Bottom Nav
└─────────────────────────────────────┘
```

### First Customer Celebration:
```
┌─────────────────────────────────────┐
│      🎊 YOUR FIRST CUSTOMER! 🎊     │ ← Major Achievement
│                                     │
│              💰                     │ ← Large Icon
│                                     │
│         Mike Chen signed!           │ ← Customer Name
│                                     │
│  You're now part of the 89% who     │ ← Success Message
│  stay with the company long-term!   │
│                                     │
│  This changes everything!           │ ← Motivational
│                                     │
│  ┌───────────────────────────────┐ │
│  │     Celebrate! 🎉            │ │ ← CTA
│  └───────────────────────────────┘ │
└─────────────────────────────────────┘
```

## Screen 4: Profile Tab (Settings & Info)

### Purpose:
Profile management, stats, settings, and help

### Layout:
```
┌─────────────────────────────────────┐
│  Profile                    ⚙️      │ ← App Bar
├─────────────────────────────────────┤
│  ┌─────────────────────────────┐   │ ← User Card
│  │     👤 John Mitchell        │   │
│  │                             │   │
│  │  Sales Rep • ABC Solar      │   │
│  │  Started: March 15, 2024    │   │
│  │  Program Day: 18 of 28      │   │
│  └─────────────────────────────┘   │
│                                     │
│  ┌─────────────────────────────┐   │ ← Stats Card
│  │  📊 Your RepX Stats         │   │
│  │                             │   │
│  │  347 Contacts processed     │   │
│  │  7 Recruits submitted       │   │
│  │  1 Recruit hired           │   │
│  │  $475 Cash earned          │   │
│  │  1 Customer won 🎉         │   │
│  └─────────────────────────────┘   │
│                                     │
│  SETTINGS                          │ ← Section
│  📔 Notifications              >    │
│  🔒 Privacy & Contacts         >    │
│                                     │
│  HELP & SUPPORT                    │ ← Section
│  ❓ How RepX Works             >    │
│  📞 Contact Support            >    │
│  🎥 Video Tutorials            >    │
│                                     │
│  COMPANY INFO                      │ ← Section
│  🏢 About ABC Solar            >    │
│  👨‍💼 Manager: Sarah Smith       >    │
│                                     │
│  ┌─────────────────────────────┐   │
│  │         Sign Out            │   │ ← Sign Out
│  └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

---

# 🔄 User Flows & Interactions

## Flow 1: Contact Swiping Session

### Initial Setup Flow:
```
App Launch (First Time)
│
├─ User Registration
│  └─ Company assignment with custom tiers/tasks
│
├─ Contact Import Permission
│  ├─ "RepX needs access to contacts"
│  ├─ Privacy explanation modal
│  └─ Grant permission → Import contacts
│
├─ Tutorial: Swipe Interface
│  ├─ Show demo contact card
│  ├─ Explain gestures (←, →, ↑)
│  ├─ Demo prospect type selection
│  └─ "Ready to start!"
│
└─ Begin Contact Swiping
```

### Daily Swiping Session:
```
Contacts Tab Selected
│
├─ Check Contact Import Status
│  ├─ If no contacts: Show import CTA
│  └─ If imported: Show current contact
│
├─ Display Contact Card
│  ├─ Contact name (large, prominent)
│  ├─ Phone number
│  ├─ Any available context info
│  └─ Swipe instructions
│
├─ User Swipe Action:
│  │
│  ├─ LEFT SWIPE (Pass)
│  │  ├─ Card slides left with animation
│  │  ├─ Brief "Passed" feedback
│  │  ├─ Auto-load next contact
│  │  └─ Update progress (148/523)
│  │
│  ├─ RIGHT SWIPE (Yes)
│  │  ├─ Card slides right with checkmark
│  │  ├─ Prospect Type Modal appears:
│  │  │  ├─ "What type of prospect?"
│  │  │  ├─ [Recruit] [Customer] [Both]
│  │  │  └─ User selection
│  │  ├─ Brief "Added!" animation
│  │  ├─ Update prospect counts
│  │  ├─ Auto-load next contact
│  │  └─ Check for tier achievements
│  │
│  └─ UP SWIPE (Super)
│     ├─ Card flies up with star animation
│     ├─ "High Potential!" message
│     ├─ Prospect Type Modal (same as right)
│     ├─ Higher priority marking
│     ├─ Special "⭐ Super Prospect" status
│     └─ Auto-load next contact
│
├─ Session Progress Tracking
│  ├─ Update progress bar
│  ├─ Running totals: "12 Recruits, 8 Customers"
│  ├─ Session milestones: "Great job! 25 processed"
│  └─ Break suggestion after 50 contacts
│
└─ Session Complete / Continue Decision
```

## Flow 2: Recruiting Game Achievement

### Recruit Submission Process:
```
Contact Swiped as "Recruit"
│
├─ Auto-Create Recruit Submission
│  ├─ Store encrypted contact data
│  ├─ Set status: "submitted"
│  ├─ Timestamp submission
│  └─ Update user's submission count
│
├─ Check Tier Thresholds
│  ├─ Query user's total submissions
│  ├─ Compare to tier requirements
│  └─ If threshold met → Trigger achievement
│
├─ Tier Achievement Flow (if applicable)
│  │
│  ├─ Achievement Detection
│  │  └─ User reaches tier threshold
│  │
│  ├─ Full-Screen Celebration Modal
│  │  ├─ "🎉 TIER 2 ACHIEVED! 🎉"
│  │  ├─ Confetti animation
│  │  ├─ Reward display: "$50 Gift Card"
│  │  ├─ Achievement description
│  │  └─ "Claim Reward" CTA
│  │
│  ├─ Reward Claim Process
│  │  ├─ Update tier status to "achieved"
│  │  ├─ Mark reward as "earned"
│  │  ├─ Instructions for claiming
│  │  └─ Notification to manager
│  │
│  └─ Update Progress Display
│     ├─ Mark tier as complete
│     ├─ Show next tier progress
│     └─ Update overall progress
│
└─ Ongoing Tracking
   ├─ Company updates recruit status
   ├─ Push notifications for status changes
   ├─ Hire confirmations trigger hire tiers
   └─ Continuous progress updates
```

### Hire Confirmation Flow:
```
Company Admin Action (Background)
├─ Mark recruit as "hired"
├─ Update recruit_submissions table
└─ Trigger user notification

Push Notification Received
├─ "Great news! John Smith was hired! 🎉"
├─ User opens app
└─ Navigate to Recruit tab

Hire Tier Check
├─ Update user's hire count
├─ Check hire tier thresholds  
├─ If tier achieved → Full celebration
└─ Update progress displays

Hire Tier Celebration
├─ "🎉 FIRST HIRE ACHIEVED! 🎉"
├─ Custom company reward display
├─ Motivation messaging
└─ Progress toward next hire tier
```

## Flow 3: 28-Day Program Task Completion

### Daily Task Management:
```
Progress Tab Selected
│
├─ Program Status Display
│  ├─ Current day: "Day 18 of 28"
│  ├─ Current week: "Week 3 - Outcomes"
│  ├─ Overall progress bar
│  └─ Cash earned summary
│
├─ This Week's Tasks Section
│  ├─ Query tasks for current week
│  ├─ Show completion status
│  ├─ Display cash rewards
│  └─ Highlight pending tasks
│
├─ Task Completion Flow
│  │
│  ├─ User Taps "Mark Complete"
│  │
│  ├─ Task Completion Modal
│  │  ├─ Task title and description
│  │  ├─ Quantity input (if applicable)
│  │  ├─ Verification method selection:
│  │  │  ├─ Self-report: "I completed this"
│  │  │  ├─ Photo: Camera upload
│  │  │  ├─ GPS: Location verification
│  │  │  └─ Manager: Pending approval
│  │  └─ [Cancel] [Complete Task]
│  │
│  ├─ Task Completion Processing
│  │  ├─ Update task_progress table
│  │  ├─ Mark task as completed
│  │  ├─ Process cash reward
│  │  ├─ Update overall progress
│  │  └─ Check for milestones
│  │
│  ├─ Completion Celebration
│  │  ├─ Checkmark animation
│  │  ├─ "+$50 Cash Earned!" notification
│  │  ├─ Confetti or celebration effect
│  │  └─ Update running totals
│  │
│  └─ Progress Updates
│     ├─ Mark task complete in UI
│     ├─ Update week progress
│     ├─ Update cash earnings
│     └─ Check week completion
│
└─ Weekly Milestone Check
   ├─ If all week tasks complete
   ├─ Weekly completion celebration
   ├─ Unlock next week's tasks
   └─ Progress toward program completion
```

### Program Completion Flow:
```
Final Task Completion
├─ Detect 28-day program completion
├─ Calculate total cash earned
└─ Trigger completion celebration

Program Completion Celebration
├─ "🎊 28-DAY PROGRAM COMPLETE! 🎊"
├─ Total earnings summary: "$875"
├─ Success rate message: "Part of 89%!"
├─ Program graduate badge
└─ Transition to ongoing rep mode

Post-Program State
├─ Hide 28-day program interface
├─ Show program completion badge
├─ Continue contact swiping
├─ Continue recruiting game
└─ Focus on ongoing success
```

## Flow 4: Customer Lead Development

### Lead Creation & Management:
```
Contact Swiped as "Customer"
│
├─ Auto-Create Customer Lead
│  ├─ Store encrypted lead data
│  ├─ Set status: "prospect"
│  ├─ Check Fast Start eligibility
│  └─ Add to lead pipeline
│
├─ Lead Development Actions
│  │
│  ├─ Contact Lead
│  │  ├─ Select contact method
│  │  ├─ Log contact attempt
│  │  ├─ Update status: "contacted"
│  │  └─ Set follow-up reminders
│  │
│  ├─ Create Opportunity
│  │  ├─ Lead shows interest
│  │  ├─ Schedule demo/inspection
│  │  ├─ Set opportunity date
│  │  ├─ Status: "opportunity"
│  │  └─ Count for Fast Start
│  │
│  └─ Win Customer
│     ├─ Opportunity converts
│     ├─ Status: "customer"
│     ├─ Record customer value
│     ├─ Set win date
│     └─ Trigger first win check
│
├─ First Customer Win Detection
│  ├─ Check if first customer for rep
│  ├─ If yes → Major celebration
│  ├─ Update retention probability
│  └─ Mark success milestone
│
├─ First Customer Celebration
│  ├─ "🎊 YOUR FIRST CUSTOMER! 🎊"
│  ├─ "89% retention rate!" message  
│  ├─ Customer details display
│  ├─ Major achievement recognition
│  └─ Motivational messaging
│
└─ Fast Start Program Integration
   ├─ Count opportunities for Fast Start
   ├─ Update Fast Start tier progress
   ├─ 14-day time limit tracking
   └─ Leaderboard position updates
```

---

# ⚙️ Technical Architecture

## Platform: FlutterFlow + Supabase

### Frontend: FlutterFlow
- **Framework**: Flutter/Dart cross-platform mobile development
- **Platform**: Native iOS and Android applications
- **UI Builder**: FlutterFlow visual development environment
- **State Management**: FlutterFlow App State + local state
- **Navigation**: Bottom tab navigation + modal overlays
- **Offline**: Local storage with sync capabilities

### Backend: Supabase
- **Database**: PostgreSQL with Row Level Security (RLS)
- **Authentication**: Supabase Auth with email/password
- **Real-time**: Supabase real-time subscriptions for live updates
- **Storage**: Supabase Storage for file uploads (verification photos)
- **Security**: Encrypted contact data, secure API endpoints

### Key Integrations:
- **Contact Access**: iOS Contacts Framework / Android ContactsContract
- **Payment Processing**: Stripe for cash reward distribution
- **Push Notifications**: Firebase Cloud Messaging
- **Analytics**: FlutterFlow Analytics + custom tracking
- **Encryption**: AES encryption for personal contact data

## Data Flow Architecture

### Contact Swiping Flow:
```
Mobile Contacts API → Local Encryption → Supabase Storage
│
├─ Swipe Action → Local State Update → UI Animation
├─ Prospect Selection → Database Insert → Progress Update
└─ Achievement Check → Celebration Trigger → Notification
```

### Real-time Updates:
```
Company Admin Action → Supabase Database Update
│
├─ Real-time Subscription → App State Update
├─ Push Notification → User Alert
└─ UI Refresh → Progress Display Update
```

### Offline Capability:
```
Online State:
├─ Immediate sync to Supabase
├─ Real-time subscriptions active
└─ Live progress updates

Offline State:
├─ Store actions locally
├─ Queue API calls
├─ Show cached data
└─ Sync when reconnected
```

## Security Architecture

### Contact Data Protection:
- **Encryption at Rest**: AES-256 encryption for all contact data
- **Encryption in Transit**: HTTPS/TLS for all API communications  
- **Key Management**: Secure key storage using platform keychain
- **Data Minimization**: Only store necessary contact information
- **Consent Management**: Clear opt-in/opt-out for contact sharing

### Database Security:
- **Row Level Security**: Users only access their own data
- **Company Isolation**: Company data separated via RLS policies
- **API Security**: JWT tokens for authenticated requests
- **Audit Trail**: Log all data access and modifications
- **GDPR Compliance**: Right to deletion and data portability

## Performance Optimization

### Mobile Performance:
- **Lazy Loading**: Load contact data in batches of 50
- **Image Optimization**: Compress and cache verification photos
- **State Management**: Minimize unnecessary widget rebuilds
- **Memory Management**: Dispose resources properly
- **Battery Optimization**: Efficient background processing

### Database Performance:
- **Indexes**: Optimized indexes on frequently queried fields
- **Connection Pooling**: Efficient database connection management
- **Query Optimization**: Optimized SQL queries and joins
- **Caching**: Redis cache for frequently accessed data
- **Pagination**: Limit query results and implement pagination

---

# 🎭 Sample Data & Scenarios

## Sample Company: ABC Solar

### Company Configuration:
```json
{
  "id": "abc-solar-uuid",
  "name": "ABC Solar Solutions",
  "industry": "Solar Sales",
  "program_duration_days": 28,
  "enable_fast_start": true,
  "fast_start_duration_days": 14
}
```

### Recruiting Tiers (Submissions):
```json
[
  {
    "tier_number": 1,
    "tier_type": "submissions", 
    "quantity_required": 5,
    "reward_title": "ABC Solar Premium Polo Shirt",
    "reward_type": "physical",
    "reward_value_usd": 35.00
  },
  {
    "tier_number": 2,
    "tier_type": "submissions",
    "quantity_required": 10, 
    "reward_title": "$50 Amazon Gift Card",
    "reward_type": "cash",
    "reward_value_usd": 50.00
  },
  {
    "tier_number": 3,
    "tier_type": "submissions",
    "quantity_required": 15,
    "reward_title": "Dinner for Two at Prime Restaurant", 
    "reward_type": "experience",
    "reward_value_usd": 200.00
  }
]
```

### Recruiting Tiers (Hires):
```json
[
  {
    "tier_number": 1,
    "tier_type": "hires",
    "quantity_required": 1,
    "reward_title": "$250 First Hire Bonus",
    "reward_type": "cash", 
    "reward_value_usd": 250.00
  },
  {
    "tier_number": 2,
    "tier_type": "hires", 
    "quantity_required": 3,
    "reward_title": "Weekend Getaway Experience",
    "reward_type": "experience",
    "reward_value_usd": 500.00
  },
  {
    "tier_number": 3,
    "tier_type": "hires",
    "quantity_required": 5, 
    "reward_title": "Annual Company Retreat Access",
    "reward_type": "access",
    "reward_value_usd": 1500.00
  }
]
```

### 28-Day Program Tasks:

#### Week 1 (Foundation):
```json
[
  {
    "title": "Complete Solar 101 Training Course",
    "description": "Finish online training modules 1-3",
    "week_number": 1,
    "task_type": "foundation",
    "quantity_required": 3,
    "verification_method": "self_report",
    "cash_reward_usd": 25.00
  },
  {
    "title": "Make 50 Door Contacts",
    "description": "Visit 50 residential properties",
    "week_number": 1, 
    "task_type": "foundation",
    "quantity_required": 50,
    "verification_method": "gps",
    "cash_reward_usd": 75.00
  },
  {
    "title": "Attend Team Meeting",
    "description": "Participate in weekly team meeting",
    "week_number": 1,
    "task_type": "foundation", 
    "quantity_required": 1,
    "verification_method": "manager_confirm",
    "cash_reward_usd": 15.00
  },
  {
    "title": "Submit 5 Recruit Prospects", 
    "description": "Identify 5 potential team members",
    "week_number": 1,
    "task_type": "foundation",
    "quantity_required": 5,
    "verification_method": "self_report", 
    "cash_reward_usd": 50.00
  }
]
```

#### Week 3 (Outcomes):
```json
[
  {
    "title": "Schedule 3 Solar Consultations",
    "description": "Book 3 in-home solar consultations", 
    "week_number": 3,
    "task_type": "outcome",
    "quantity_required": 3,
    "verification_method": "self_report",
    "cash_reward_usd": 100.00
  },
  {
    "title": "Generate 2 Customer Referrals",
    "description": "Get 2 referrals from existing customers",
    "week_number": 3,
    "task_type": "outcome", 
    "quantity_required": 2,
    "verification_method": "manager_confirm",
    "cash_reward_usd": 75.00
  },
  {
    "title": "Complete 1 Solar Installation",
    "description": "Participate in a solar installation",
    "week_number": 3,
    "task_type": "outcome",
    "quantity_required": 1, 
    "verification_method": "photo",
    "cash_reward_usd": 125.00
  }
]
```

## Sample User Data

### John Mitchell (Week 3 Rep):
```json
{
  "user_id": "john-mitchell-uuid",
  "first_name": "John",
  "last_name": "Mitchell", 
  "email": "john.mitchell@abcsolar.com",
  "company_id": "abc-solar-uuid",
  "hire_date": "2024-03-15",
  "program_start_date": "2024-03-15",
  "current_program_day": 18,
  "program_completed": false
}
```

### John's Progress Data:
```json
{
  "contacts_imported": 523,
  "contacts_processed": 347,
  "contacts_total": 523,
  "recruits_submitted": 7,
  "recruits_hired": 1,
  "customers_identified": 12,
  "opportunities_created": 4,
  "first_customer_won": true,
  "first_customer_date": "2024-03-28",
  "tasks_completed": 8,
  "cash_earned": 475.00,
  "fast_start_opportunities": 4,
  "fast_start_tier": 2
}
```

### John's Recent Contact Swipes:
```json
[
  {
    "contact_name": "Sarah Johnson", 
    "swipe_result": "yes",
    "prospect_type": "customer",
    "swiped_at": "2024-04-01T14:30:00Z"
  },
  {
    "contact_name": "Mike Chen",
    "swipe_result": "super", 
    "prospect_type": "both",
    "swiped_at": "2024-04-01T14:25:00Z"
  },
  {
    "contact_name": "Lisa Wang",
    "swipe_result": "yes",
    "prospect_type": "recruit", 
    "swiped_at": "2024-04-01T14:20:00Z"
  }
]
```

### John's Customer Leads:
```json
[
  {
    "lead_name": "Mike Chen",
    "status": "customer", 
    "became_customer": true,
    "customer_date": "2024-03-28",
    "customer_value_usd": 25000.00,
    "opportunity_type": "solar_consultation"
  },
  {
    "lead_name": "Sarah Johnson",
    "status": "opportunity",
    "opportunity_type": "solar_consultation",
    "opportunity_date": "2024-04-03"
  },
  {
    "lead_name": "Tom Wilson", 
    "status": "contacted",
    "contact_method": "phone",
    "contact_date": "2024-04-01"
  }
]
```

## Sample UI State Data

### Contacts Tab State:
```json
{
  "current_contact": {
    "id": "contact-uuid-123",
    "name": "Sarah Johnson", 
    "phone": "(555) 123-4567",
    "context": "Known from: College"
  },
  "progress": {
    "processed": 347,
    "total": 523,
    "percentage": 66.3
  },
  "session_stats": {
    "contacts_today": 23,
    "customers_today": 6,
    "recruits_today": 4
  },
  "is_swiping": true,
  "prospect_modal_open": false
}
```

### Recruit Tab State:
```json
{
  "overall_stats": {
    "submitted": 7,
    "hired": 1
  },
  "submission_tiers": [
    {
      "tier_number": 1,
      "required": 5,
      "current": 7,
      "achieved": true,
      "reward": "ABC Solar Polo Shirt"
    },
    {
      "tier_number": 2, 
      "required": 10,
      "current": 7,
      "achieved": false,
      "progress_percent": 70,
      "reward": "$50 Amazon Gift Card"
    }
  ],
  "hire_tiers": [
    {
      "tier_number": 1,
      "required": 1, 
      "current": 1,
      "achieved": true,
      "reward": "$250 First Hire Bonus"
    }
  ],
  "recent_activity": [
    "John Smith - Hired! 🎉",
    "Lisa Wang - Interview scheduled",
    "Mike Chen - Contacted by HR"
  ],
  "show_achievement": false
}
```

## Sample Interaction Scenarios

### Scenario 1: First Time User Setup
```
Day 1 - New Rep John Mitchell:
1. Downloads RepX app
2. Creates account with company email
3. Grants contact permissions
4. Imports 523 phone contacts 
5. Completes swipe tutorial
6. Processes first 25 contacts
7. Identifies 6 customers, 4 recruits
8. Completes first foundation task
9. Earns first $25 cash reward
10. Celebrates first day success
```

### Scenario 2: Tier Achievement Flow
```
Day 8 - John reaches recruit submission milestone:
1. Swipes contact "Alex Thompson" 
2. Selects "Recruit" prospect type
3. System detects: 5 total submissions
4. Triggers Tier 1 achievement
5. Full-screen celebration appears
6. "🎉 TIER 1 ACHIEVED! Premium Polo Shirt!"
7. User claims reward
8. Progress updates to show Tier 2 (3/10)
9. Notification sent to manager
10. Continues swiping with motivation boost
```

### Scenario 3: First Customer Win
```
Day 14 - John wins first customer:
1. Customer lead "Mike Chen" shows interest
2. John schedules solar consultation
3. Consultation converts to sale
4. John marks lead as "Customer Won"
5. System detects: First customer achievement
6. Major celebration modal appears
7. "🎊 YOUR FIRST CUSTOMER! 89% SUCCESS RATE!"
8. Achievement badge added to profile
9. Manager notified of success
10. Retention probability updated
```

---

# ⚙️ Implementation Guidelines

## FlutterFlow Development Setup

### Project Configuration:
1. **Create FlutterFlow Project**
   - Template: Blank mobile app
   - Platform: iOS + Android
   - Authentication: Supabase Auth
   - Database: Supabase PostgreSQL

2. **Configure Supabase Integration** 
   - Project URL: Configure in FlutterFlow settings
   - Anonymous key: Add to app constants
   - Service key: For backend operations
   - Enable Row Level Security on all tables

3. **App State Variables**
   ```dart
   // User & Progress
   User? currentUser
   RepProgress? userProgress
   
   // Current Session
   Contact? currentContact
   List<Contact> contactsQueue
   int sessionContactsProcessed
   
   // Navigation & UI
   int selectedTabIndex
   bool isSwipeMode
   bool showAchievementModal
   String? achievementType
   
   // Cache & Sync
   DateTime lastSyncTime
   List<PendingAction> offlineActions
   bool isOnline
   ```

### Key FlutterFlow Components:

#### Bottom Navigation:
```dart
BottomNavigationBar(
  currentIndex: selectedTabIndex,
  type: BottomNavigationBarType.fixed,
  selectedItemColor: Color(0xFF2563EB),
  unselectedItemColor: Color(0xFF6B7280),
  items: [
    BottomNavigationBarItem(
      icon: Icon(Icons.phone_android),
      label: 'Contacts'
    ),
    BottomNavigationBarItem(
      icon: Icon(Icons.emoji_events), 
      label: 'Recruit'
    ),
    BottomNavigationBarItem(
      icon: Icon(Icons.trending_up),
      label: 'Progress'
    ),
    BottomNavigationBarItem(
      icon: Icon(Icons.person),
      label: 'Profile'
    )
  ]
)
```

#### Contact Swipe Card:
```dart
GestureDetector(
  onPanUpdate: (details) {
    // Handle swipe gestures
    final deltaX = details.localPosition.dx;
    // Update card position and visual feedback
  },
  onPanEnd: (details) {
    final velocity = details.velocity.pixelsPerSecond.dx;
    if (velocity.abs() > 500) {
      // Process swipe based on direction
      if (velocity > 0) {
        handleSwipe('right');
      } else {
        handleSwipe('left');
      }
    }
  },
  child: Card(
    child: Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text(
          contactName,
          style: TextStyle(
            fontSize: 24,
            fontWeight: FontWeight.w600
          )
        ),
        Text(
          contactPhone,
          style: TextStyle(
            fontSize: 16,
            color: Colors.grey[600]
          )
        )
      ]
    )
  )
)
```

#### Achievement Modal:
```dart
Dialog(
  backgroundColor: Colors.transparent,
  child: Container(
    decoration: BoxDecoration(
      gradient: LinearGradient(
        begin: Alignment.topCenter,
        end: Alignment.bottomCenter,
        colors: [
          Color(0xFFEAB308).withOpacity(0.2),
          Colors.white
        ]
      ),
      borderRadius: BorderRadius.circular(20)
    ),
    child: Column(
      mainAxisSize: MainAxisSize.min,
      children: [
        // Trophy icon with animation
        AnimatedScale(
          scale: celebrationScale,
          duration: Duration(milliseconds: 600),
          child: Icon(
            Icons.emoji_events,
            size: 80,
            color: Color(0xFFEAB308)
          )
        ),
        // Achievement text
        Text(
          '🎉 TIER 2 ACHIEVED! 🎉',
          style: TextStyle(
            fontSize: 24,
            fontWeight: FontWeight.bold,
            color: Color(0xFFEAB308)
          )
        ),
        // Reward details
        Text(
          rewardTitle,
          style: TextStyle(
            fontSize: 20,
            fontWeight: FontWeight.w600
          )
        ),
        // Claim button
        ElevatedButton(
          onPressed: () => claimReward(),
          style: ElevatedButton.styleFrom(
            backgroundColor: Color(0xFFEAB308),
            minimumSize: Size(200, 48)
          ),
          child: Text('Claim Your Reward')
        )
      ]
    )
  )
)
```

## Database Implementation

### Supabase Setup Script:
```sql
-- Enable Row Level Security
ALTER TABLE companies ENABLE ROW LEVEL SECURITY;
ALTER TABLE users ENABLE ROW LEVEL SECURITY;
ALTER TABLE contacts ENABLE ROW LEVEL SECURITY;
ALTER TABLE contact_swipes ENABLE ROW LEVEL SECURITY;
ALTER TABLE recruiting_tiers ENABLE ROW LEVEL SECURITY;
ALTER TABLE recruit_submissions ENABLE ROW LEVEL SECURITY;
ALTER TABLE ramp_tasks ENABLE ROW LEVEL SECURITY;
ALTER TABLE task_progress ENABLE ROW LEVEL SECURITY;
ALTER TABLE customer_leads ENABLE ROW LEVEL SECURITY;
ALTER TABLE rep_progress ENABLE ROW LEVEL SECURITY;

-- RLS Policies
CREATE POLICY "Users can only access their own data" ON users
FOR ALL USING (auth.uid() = id);

CREATE POLICY "Users can only access their own contacts" ON contacts  
FOR ALL USING (user_id = auth.uid());

CREATE POLICY "Users can access their company's tiers" ON recruiting_tiers
FOR SELECT USING (
  company_id IN (
    SELECT company_id FROM users WHERE id = auth.uid()
  )
);

-- Functions for contact encryption
CREATE OR REPLACE FUNCTION encrypt_contact_data(data TEXT)
RETURNS BYTEA AS $$
BEGIN
  RETURN encrypt(data::BYTEA, 'repx_encryption_key', 'aes');
END;
$$ LANGUAGE plpgsql;

CREATE OR REPLACE FUNCTION decrypt_contact_data(encrypted_data BYTEA)
RETURNS TEXT AS $$
BEGIN
  RETURN convert_from(decrypt(encrypted_data, 'repx_encryption_key', 'aes'), 'UTF8');
END;
$$ LANGUAGE plpgsql;
```

### Key Supabase Queries:

#### Get Current Contact for Swiping:
```sql
SELECT id, 
       decrypt_contact_data(name_encrypted) as name,
       decrypt_contact_data(phone_encrypted) as phone
FROM contacts 
WHERE user_id = $1 
  AND is_processed = false 
ORDER BY created_at 
LIMIT 1;
```

#### Check Tier Achievement:
```sql
SELECT rt.*, 
       COALESCE(rs.submission_count, 0) as current_count
FROM recruiting_tiers rt
LEFT JOIN (
  SELECT COUNT(*) as submission_count 
  FROM recruit_submissions 
  WHERE user_id = $1
) rs ON true
WHERE rt.company_id = (
  SELECT company_id FROM users WHERE id = $1
)
AND rt.tier_type = 'submissions'
AND rt.quantity_required <= COALESCE(rs.submission_count, 0)
AND rt.id NOT IN (
  SELECT recruiting_tier_id 
  FROM recruiting_rewards 
  WHERE user_id = $1
);
```

#### Update Rep Progress:
```sql
INSERT INTO rep_progress (
  user_id, contacts_processed, recruits_submitted, 
  cash_earned, updated_at
) VALUES (
  $1, $2, $3, $4, NOW()
)
ON CONFLICT (user_id) DO UPDATE SET
  contacts_processed = $2,
  recruits_submitted = $3,
  cash_earned = $4,
  updated_at = NOW();
```

## Mobile Development Best Practices

### Performance Optimization:
1. **Lazy Loading**: Load contacts in batches of 50
2. **Image Optimization**: Compress verification photos to <1MB
3. **State Management**: Use Provider pattern for global state
4. **Memory Management**: Dispose controllers and streams
5. **Battery Optimization**: Minimize background processing

### Security Implementation:
1. **Contact Encryption**: Encrypt all personal data before storage
2. **Secure Storage**: Use flutter_secure_storage for sensitive data
3. **API Security**: Include JWT tokens in all requests  
4. **Certificate Pinning**: Pin SSL certificates for API endpoints
5. **Biometric Auth**: Optional fingerprint/face unlock

### Offline Capability:
1. **Local Database**: SQLite for offline contact storage
2. **Sync Queue**: Queue actions when offline
3. **Conflict Resolution**: Handle sync conflicts gracefully
4. **Cache Management**: Smart caching with TTL
5. **Progressive Sync**: Sync critical data first

## Testing Strategy

### Unit Tests:
```dart
// Test swipe logic
testWidgets('Contact swipe right creates prospect', (tester) async {
  final contact = Contact(name: 'John Doe', phone: '555-1234');
  final swipeController = SwipeController();
  
  await swipeController.handleSwipe(contact, SwipeDirection.right);
  
  expect(swipeController.pendingProspect, isNotNull);
  expect(swipeController.pendingProspect.contact, equals(contact));
});

// Test tier achievement
test('Tier achievement triggers celebration', () {
  final tierController = TierController();
  tierController.submissionCount = 5;
  
  final result = tierController.checkTierAchievement();
  
  expect(result.achieved, isTrue);
  expect(result.tier.tier_number, equals(1));
});
```

### Integration Tests:
```dart
// Test complete swipe flow
testWidgets('Complete swipe flow with prospect selection', (tester) async {
  await tester.pumpWidget(RepXApp());
  
  // Navigate to contacts tab
  await tester.tap(find.byIcon(Icons.phone_android));
  await tester.pumpAndSettle();
  
  // Swipe right on contact
  await tester.drag(find.byType(ContactCard), Offset(300, 0));
  await tester.pumpAndSettle();
  
  // Select prospect type
  await tester.tap(find.text('RECRUIT'));
  await tester.pumpAndSettle();
  
  // Verify progress update
  expect(find.text('148/523'), findsOneWidget);
});
```

### User Acceptance Tests:
1. **New User Onboarding**: Complete first-time user flow
2. **Contact Import**: Test contact permission and import
3. **Swipe Session**: Complete 50-contact swipe session
4. **Achievement Flow**: Trigger and claim tier achievement
5. **Task Completion**: Complete 28-day program task
6. **First Customer**: Win first customer and see celebration
7. **Offline Mode**: Test offline functionality and sync

## Deployment & Operations

### App Store Requirements:
1. **Privacy Policy**: Clear contact data usage policy
2. **Permissions**: Justify contact access necessity  
3. **Content Rating**: Business/Productivity rating
4. **Screenshots**: Show main features and benefits
5. **App Description**: Focus on 89% retention value prop

### Analytics & Monitoring:
1. **User Engagement**: Track daily active users, session length
2. **Feature Usage**: Monitor swipe rates, task completion
3. **Business Metrics**: Track retention rates, tier achievements
4. **Performance**: Monitor app crashes, load times
5. **Conversion**: Track new user to active user conversion

### Support & Documentation:
1. **In-App Help**: Contextual help throughout app
2. **Video Tutorials**: Short videos for key features
3. **FAQ**: Common questions and troubleshooting  
4. **Support Chat**: In-app support for technical issues
5. **User Guides**: Detailed guides for managers and reps

---

**🎯 This complete specification provides everything needed to build RepX MVP - a mobile-first platform that transforms new sales rep onboarding through systematic contact mining, gamified recruiting, structured task progression, and customer development, ultimately achieving 89% retention rates through first customer wins within 14 days.**

**Key Success Metrics:**
- 95% contact processing completion
- 90% foundation task completion  
- 75% outcome task completion
- 75% first customer within 14 days
- 89% first-year retention rate

**Technical Stack:**
- FlutterFlow + Supabase
- Native iOS/Android
- Encrypted contact storage
- Real-time progress sync
- Offline-first design

**Business Impact:**
- 5x improvement in training ROI
- $15K → $3K cost per successful hire  
- Network effects through contact mining
- Scalable SaaS revenue model
