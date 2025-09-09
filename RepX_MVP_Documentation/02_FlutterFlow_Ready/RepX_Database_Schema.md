# RepX Database Schema - Clean & Focused
**Optimized for the 4 Core RepX Systems**

---

## 🗄️ **Database Architecture Overview**

**Database Choice**: Supabase PostgreSQL (FlutterFlow recommended)  
**Focus**: Single user type (new sales rep), company-customizable systems  
**Security**: Row Level Security (RLS) for data isolation

---

## 📋 **Core Entity Relationships**

```
Company (1) ←→ (Many) Users
Company (1) ←→ (Many) RecruitingTiers  
Company (1) ←→ (Many) RampTasks
User (1) ←→ (Many) Contacts
User (1) ←→ (Many) ContactSwipes
User (1) ←→ (Many) CustomerLeads
User (1) ←→ (Many) TaskProgress
```

---

## 🏢 **1. Company Configuration Tables**

### **companies**
*Company settings and customization*
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
  
  -- Timestamps
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### **recruiting_tiers**
*Company-customizable recruiting gamification tiers*
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
  
  -- Status
  is_active BOOLEAN DEFAULT true,
  
  -- Timestamps
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  
  UNIQUE(company_id, tier_type, tier_number)
);
```

### **ramp_tasks**
*Company-customizable 28-day program tasks*
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
  
  -- Timestamps
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

---

## 👤 **2. User & Rep Tables**

### **users**
*Sales rep user accounts*
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
  
  -- Account status
  is_active BOOLEAN DEFAULT true,
  last_login TIMESTAMP WITH TIME ZONE,
  
  -- Timestamps
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### **rep_progress**
*Overall progress tracking for each rep*
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
  
  -- Timestamps
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

---

## 📱 **3. Contact Management Tables**

### **contacts**
*Imported phone contacts (encrypted)*
```sql
CREATE TABLE contacts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  
  -- Contact info (encrypted)
  name_encrypted BYTEA NOT NULL,
  phone_encrypted BYTEA,
  email_encrypted BYTEA,
  
  -- Contact metadata
  has_phone BOOLEAN DEFAULT false,
  has_email BOOLEAN DEFAULT false,
  contact_source VARCHAR(50) DEFAULT 'phone', -- 'phone', 'manual'
  
  -- Processing status
  is_processed BOOLEAN DEFAULT false,
  processed_at TIMESTAMP WITH TIME ZONE,
  
  -- Timestamps
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### **contact_swipes**
*Contact swiping decisions and categorization*
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
  contact_method VARCHAR(50), -- 'call', 'text', 'email'
  contact_date DATE,
  response_status VARCHAR(20), -- 'interested', 'not_interested', 'no_response'
  
  -- Timestamps
  swiped_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  
  UNIQUE(user_id, contact_id)
);
```

---

## 🎯 **4. Recruiting Game Tables**

### **recruit_submissions**
*Tracking submitted recruiting prospects*
```sql
CREATE TABLE recruit_submissions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  contact_swipe_id UUID REFERENCES contact_swipes(id),
  
  -- Submission details
  prospect_name_encrypted BYTEA NOT NULL,
  prospect_phone_encrypted BYTEA,
  prospect_email_encrypted BYTEA,
  submission_method VARCHAR(50) DEFAULT 'app', -- 'app', 'manual'
  
  -- Company processing
  company_status VARCHAR(20) DEFAULT 'submitted', 
  -- 'submitted', 'contacted', 'interview_scheduled', 'hired', 'not_hired'
  status_updated_by UUID REFERENCES users(id),
  status_updated_at TIMESTAMP WITH TIME ZONE,
  status_notes TEXT,
  
  -- Hire details (if hired)
  hire_date DATE,
  hire_position VARCHAR(100),
  
  -- Timestamps
  submitted_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### **recruiting_rewards**
*Tracking earned recruiting tier rewards*
```sql
CREATE TABLE recruiting_rewards (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  recruiting_tier_id UUID REFERENCES recruiting_tiers(id),
  
  -- Reward details
  tier_type VARCHAR(20) NOT NULL, -- 'submissions' or 'hires'
  tier_number INTEGER NOT NULL,
  quantity_achieved INTEGER NOT NULL,
  
  -- Reward status
  reward_status VARCHAR(20) DEFAULT 'earned', -- 'earned', 'claimed', 'delivered'
  claimed_at TIMESTAMP WITH TIME ZONE,
  delivered_at TIMESTAMP WITH TIME ZONE,
  delivery_notes TEXT,
  
  -- Timestamps
  earned_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

---

## 📈 **5. 28-Day Program Tables**

### **task_progress**
*Individual task completion tracking*
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
  verification_status VARCHAR(20) DEFAULT 'pending', -- 'pending', 'verified', 'rejected'
  verified_by UUID REFERENCES users(id),
  verified_at TIMESTAMP WITH TIME ZONE,
  
  -- Reward payout
  reward_status VARCHAR(20) DEFAULT 'pending', -- 'pending', 'paid', 'cancelled'  
  reward_paid_at TIMESTAMP WITH TIME ZONE,
  reward_amount_usd DECIMAL(10,2),
  
  -- Progress notes
  notes TEXT,
  
  -- Timestamps
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  
  UNIQUE(user_id, ramp_task_id)
);
```

---

## 🛍️ **6. Customer & Lead Tables**

### **customer_leads**
*Customer prospects from contact swiping*
```sql
CREATE TABLE customer_leads (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  contact_swipe_id UUID REFERENCES contact_swipes(id),
  
  -- Lead details
  lead_name_encrypted BYTEA NOT NULL,
  lead_phone_encrypted BYTEA,
  lead_email_encrypted BYTEA,
  lead_source VARCHAR(50) DEFAULT 'contact_swipe',
  
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
  
  -- Timestamps
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### **fast_start_leaderboard**
*14-day Fast Start program tracking*
```sql
CREATE TABLE fast_start_leaderboard (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  
  -- Fast Start period
  start_date DATE NOT NULL,
  end_date DATE NOT NULL,
  program_day INTEGER NOT NULL, -- 1-14
  
  -- Daily metrics
  opportunities_created_today INTEGER DEFAULT 0,
  opportunities_total INTEGER DEFAULT 0,
  
  -- Tier progress
  current_tier INTEGER DEFAULT 0,
  tier_1_date DATE,
  tier_2_date DATE,
  tier_3_date DATE,
  tier_4_date DATE,
  tier_5_date DATE,
  
  -- Daily snapshot
  recorded_date DATE DEFAULT CURRENT_DATE,
  
  -- Timestamps
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  
  UNIQUE(user_id, program_day)
);
```

---

## 🔐 **7. Security & Encryption**

### **Row Level Security (RLS)**
```sql
-- Enable RLS on all tables
ALTER TABLE companies ENABLE ROW LEVEL SECURITY;
ALTER TABLE users ENABLE ROW LEVEL SECURITY;
ALTER TABLE contacts ENABLE ROW LEVEL SECURITY;
-- ... (all other tables)

-- Example RLS Policy: Users can only see their own data
CREATE POLICY "Users can only access their own data" ON contacts
FOR ALL USING (user_id = auth.uid());

-- Company admins can see their company's configuration
CREATE POLICY "Company access" ON recruiting_tiers
FOR ALL USING (
  company_id IN (
    SELECT company_id FROM users WHERE id = auth.uid()
  )
);
```

### **Encryption Functions**
```sql
-- Contact data encryption/decryption functions
CREATE OR REPLACE FUNCTION encrypt_contact_data(data TEXT)
RETURNS BYTEA AS $$
BEGIN
  -- Use Supabase's built-in encryption or custom solution
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

---

## 📊 **8. Database Views & Analytics**

### **rep_dashboard_view**
*Complete rep progress summary*
```sql
CREATE VIEW rep_dashboard_view AS
SELECT 
  u.id as user_id,
  u.first_name,
  u.last_name,
  u.current_program_day,
  rp.contacts_processed,
  rp.recruits_submitted,
  rp.recruits_hired,
  rp.customers_identified,
  rp.opportunities_created,
  rp.first_customer_won,
  rp.cash_earned,
  rp.points_earned,
  
  -- Tier progress calculations
  (SELECT COUNT(*) FROM recruiting_rewards WHERE user_id = u.id AND tier_type = 'submissions') as submission_tiers_earned,
  (SELECT COUNT(*) FROM recruiting_rewards WHERE user_id = u.id AND tier_type = 'hires') as hire_tiers_earned,
  
  -- Task completion
  (SELECT COUNT(*) FROM task_progress WHERE user_id = u.id AND is_completed = true) as tasks_completed,
  (SELECT COUNT(*) FROM ramp_tasks WHERE company_id = u.company_id AND is_active = true) as tasks_total
  
FROM users u
LEFT JOIN rep_progress rp ON u.id = rp.user_id
WHERE u.is_active = true;
```

### **company_analytics_view**
*Company-wide performance metrics*
```sql
CREATE VIEW company_analytics_view AS
SELECT 
  c.id as company_id,
  c.name as company_name,
  COUNT(u.id) as total_reps,
  COUNT(CASE WHEN u.program_completed = true THEN 1 END) as completed_reps,
  AVG(rp.contacts_processed) as avg_contacts_processed,
  SUM(rp.recruits_submitted) as total_recruits_submitted,
  SUM(rp.recruits_hired) as total_recruits_hired,
  SUM(rp.opportunities_created) as total_opportunities,
  COUNT(CASE WHEN rp.first_customer_won = true THEN 1 END) as reps_with_customers,
  
  -- Retention calculation (simplified)
  ROUND(
    (COUNT(CASE WHEN u.program_completed = true THEN 1 END)::FLOAT / 
     NULLIF(COUNT(u.id), 0) * 100), 2
  ) as retention_rate_percent

FROM companies c
LEFT JOIN users u ON c.id = u.company_id
LEFT JOIN rep_progress rp ON u.id = rp.user_id
WHERE u.is_active = true
GROUP BY c.id, c.name;
```

---

## 🔧 **FlutterFlow Integration**

### **Supabase Configuration**
```dart
// supabase_config.dart
class SupabaseConfig {
  static const String url = 'your-supabase-url';
  static const String anonKey = 'your-supabase-anon-key';
  
  // Table names for FlutterFlow
  static const String companies = 'companies';
  static const String users = 'users';
  static const String contacts = 'contacts';
  static const String contactSwipes = 'contact_swipes';
  static const String recruitSubmissions = 'recruit_submissions';
  static const String taskProgress = 'task_progress';
  static const String customerLeads = 'customer_leads';
}
```

### **Key Queries for FlutterFlow**
```sql
-- Get current rep progress
SELECT * FROM rep_dashboard_view WHERE user_id = $1;

-- Get recruiting tiers for company  
SELECT * FROM recruiting_tiers 
WHERE company_id = (SELECT company_id FROM users WHERE id = $1)
ORDER BY tier_type, tier_number;

-- Get current week's tasks
SELECT rt.*, tp.is_completed, tp.quantity_completed
FROM ramp_tasks rt
LEFT JOIN task_progress tp ON rt.id = tp.ramp_task_id AND tp.user_id = $1
WHERE rt.company_id = (SELECT company_id FROM users WHERE id = $1)
AND rt.week_number = $2
ORDER BY rt.sort_order;

-- Get unprocessed contacts for swiping
SELECT * FROM contacts 
WHERE user_id = $1 AND is_processed = false 
ORDER BY created_at 
LIMIT 1;
```

---

## 🚀 **Implementation Notes**

### **Data Migration Strategy**
1. **Phase 1**: Core tables (companies, users, contacts)
2. **Phase 2**: Swiping and recruiting (contact_swipes, recruit_submissions)  
3. **Phase 3**: 28-day program (ramp_tasks, task_progress)
4. **Phase 4**: Lead tracking (customer_leads, fast_start_leaderboard)

### **Performance Optimizations**
- **Indexes**: On foreign keys, frequently queried fields
- **Partitioning**: Large tables by company_id or date ranges
- **Caching**: Frequent queries in application layer
- **Batch Operations**: Process contact imports in batches

### **Backup & Recovery**
- **Daily Backups**: Automated Supabase backups
- **Contact Encryption**: Separate key storage for contact data
- **Audit Trail**: Track all data changes for compliance

---

**🎯 This database schema is optimized for the RepX MVP, focusing on the 4 core systems while maintaining simplicity, security, and FlutterFlow compatibility.**
