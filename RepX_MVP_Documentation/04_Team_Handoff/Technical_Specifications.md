# Technical Specifications - RepX MVP

## 🏗️ **System Architecture Overview**

### **High-Level Architecture**
```
┌─────────────────────────────────────────────────────────────┐
│                    RepX Mobile Apps                         │
│                  (iOS & Android)                           │
└─────────────────┬───────────────────────────────────────────┘
                  │
                  │ HTTPS/WSS
                  │
┌─────────────────▼───────────────────────────────────────────┐
│                  API Gateway                                │
│              (Supabase Edge Functions)                      │
└─────────────────┬───────────────────────────────────────────┘
                  │
    ┌─────────────┼─────────────┬─────────────────────────────┐
    │             │             │                             │
┌───▼────┐ ┌─────▼─────┐ ┌─────▼─────┐ ┌─────────────────▼─────┐
│Database│ │   Auth    │ │Real-time  │ │   External Services   │
│(Postgres)│ │ Service   │ │Subscriptions│ │                       │
│Supabase│ │(Supabase) │ │(Supabase) │ │• Stripe (Payments)    │
└────────┘ └───────────┘ └───────────┘ │• Twilio (SMS)         │
                                       │• SendGrid (Email)     │
                                       │• AWS S3 (File Storage)│
                                       └───────────────────────┘
```

---

## 📱 **Frontend Specifications**

### **Mobile Application Stack**
- **Framework**: Flutter (FlutterFlow for rapid development)
- **Language**: Dart
- **Target Platforms**: iOS 13+, Android 8+ (API Level 26+)
- **Architecture Pattern**: MVVM with Provider/Riverpod state management
- **Navigation**: Go Router for declarative navigation

### **Key Dependencies**
```yaml
dependencies:
  flutter: ^3.16.0
  supabase_flutter: ^2.0.0
  provider: ^6.1.1
  go_router: ^12.1.3
  shared_preferences: ^2.2.2
  contacts_service: ^0.6.3
  geolocator: ^10.1.0
  image_picker: ^1.0.4
  permission_handler: ^11.1.0
  flutter_local_notifications: ^16.3.0
  connectivity_plus: ^5.0.2
  cached_network_image: ^3.3.0
  flutter_animate: ^4.3.0
  confetti: ^0.7.0
```

### **Screen Structure**
```
lib/
├── main.dart
├── app/
│   ├── app.dart
│   ├── router.dart
│   └── theme.dart
├── core/
│   ├── constants/
│   ├── services/
│   ├── utils/
│   └── extensions/
├── features/
│   ├── auth/
│   │   ├── screens/
│   │   ├── widgets/
│   │   └── providers/
│   ├── onboarding/
│   │   ├── screens/
│   │   ├── widgets/
│   │   └── providers/
│   ├── contacts/
│   │   ├── screens/
│   │   ├── widgets/
│   │   └── providers/
│   ├── tasks/
│   │   ├── screens/
│   │   ├── widgets/
│   │   └── providers/
│   └── rewards/
│       ├── screens/
│       ├── widgets/
│       └── providers/
└── shared/
    ├── widgets/
    ├── models/
    └── services/
```

### **State Management Architecture**
```dart
// Example Provider Structure
class ContactsProvider extends ChangeNotifier {
  final SupabaseService _supabaseService;
  final ContactsService _contactsService;
  
  List<Contact> _contacts = [];
  List<UserContact> _processedContacts = [];
  bool _isLoading = false;
  String? _error;
  
  // Getters
  List<Contact> get contacts => _contacts;
  List<UserContact> get processedContacts => _processedContacts;
  bool get isLoading => _isLoading;
  String? get error => _error;
  
  // Methods
  Future<void> importContacts() async { /* Implementation */ }
  Future<void> swipeContact(String contactId, SwipeDirection direction) async { /* Implementation */ }
  Future<void> categorizeContact(String contactId, ContactCategory category, int tier) async { /* Implementation */ }
}
```

### **Offline Capability**
```dart
class OfflineService {
  static const String _offlineActionsKey = 'offline_actions';
  
  // Queue actions when offline
  Future<void> queueAction(OfflineAction action) async {
    final prefs = await SharedPreferences.getInstance();
    final actions = await getQueuedActions();
    actions.add(action);
    await prefs.setString(_offlineActionsKey, jsonEncode(actions));
  }
  
  // Sync when back online
  Future<void> syncOfflineActions() async {
    final actions = await getQueuedActions();
    for (final action in actions) {
      try {
        await _executeAction(action);
        await _removeFromQueue(action);
      } catch (e) {
        // Handle sync errors
      }
    }
  }
}
```

---

## 🔧 **Backend Specifications**

### **Database Architecture (Supabase/PostgreSQL)**

#### **Core Tables**
```sql
-- Users (New Sales Reps)
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email TEXT UNIQUE NOT NULL,
    password_hash TEXT NOT NULL,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    company_id UUID REFERENCES companies(id),
    phone TEXT NOT NULL,
    hire_date DATE NOT NULL,
    onboarding_start_date DATE NOT NULL,
    current_week INTEGER DEFAULT 1,
    is_active BOOLEAN DEFAULT TRUE,
    retention_status TEXT DEFAULT 'active',
    first_customer_date DATE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Companies
CREATE TABLE companies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name TEXT NOT NULL,
    domain TEXT UNIQUE NOT NULL,
    industry TEXT DEFAULT 'door_to_door',
    logo_url TEXT,
    onboarding_program_id UUID REFERENCES onboarding_programs(id),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- User Contacts
CREATE TABLE user_contacts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    contact_name TEXT NOT NULL,
    phone_number TEXT,
    email TEXT,
    contact_source TEXT DEFAULT 'phone_sync',
    category TEXT CHECK (category IN ('customer', 'recruit', 'skip')),
    tier_level INTEGER CHECK (tier_level IN (1, 2, 3)),
    is_starred BOOLEAN DEFAULT FALSE,
    is_processed BOOLEAN DEFAULT FALSE,
    swipe_date TIMESTAMP WITH TIME ZONE,
    approach_status TEXT DEFAULT 'not_contacted',
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Weekly Tasks
CREATE TABLE weekly_tasks (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    program_id UUID REFERENCES onboarding_programs(id),
    week_number INTEGER NOT NULL CHECK (week_number BETWEEN 1 AND 4),
    task_name TEXT NOT NULL,
    task_description TEXT NOT NULL,
    task_type TEXT NOT NULL CHECK (task_type IN ('control_based', 'outcome_based')),
    acceptance_criteria TEXT NOT NULL,
    reward_amount DECIMAL(10,2) NOT NULL,
    is_required BOOLEAN DEFAULT TRUE,
    sort_order INTEGER NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Task Completions
CREATE TABLE task_completions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    task_id UUID REFERENCES weekly_tasks(id),
    completion_status TEXT DEFAULT 'not_started' CHECK (
        completion_status IN ('not_started', 'in_progress', 'completed', 'verified')
    ),
    completion_date TIMESTAMP WITH TIME ZONE,
    verification_data JSONB,
    reward_amount DECIMAL(10,2),
    reward_paid BOOLEAN DEFAULT FALSE,
    reward_paid_date TIMESTAMP WITH TIME ZONE,
    notes TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Reward Transactions
CREATE TABLE reward_transactions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    transaction_type TEXT NOT NULL CHECK (
        transaction_type IN ('contact_tier', 'task_completion', 'bonus_achievement')
    ),
    reference_id UUID,
    amount DECIMAL(10,2) NOT NULL,
    description TEXT NOT NULL,
    status TEXT DEFAULT 'pending' CHECK (
        status IN ('pending', 'approved', 'paid', 'cancelled')
    ),
    payment_method TEXT DEFAULT 'cash',
    payment_reference TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    processed_at TIMESTAMP WITH TIME ZONE
);
```

#### **Indexes for Performance**
```sql
-- Critical indexes for app performance
CREATE INDEX idx_user_contacts_user_processed ON user_contacts(user_id, is_processed);
CREATE INDEX idx_user_contacts_category ON user_contacts(user_id, category);
CREATE INDEX idx_task_completions_user_task ON task_completions(user_id, task_id);
CREATE INDEX idx_weekly_tasks_program_week ON weekly_tasks(program_id, week_number);
CREATE INDEX idx_reward_transactions_user_date ON reward_transactions(user_id, created_at);
CREATE INDEX idx_users_company_active ON users(company_id, is_active);
```

#### **Row Level Security (RLS)**
```sql
-- Enable RLS on all tables
ALTER TABLE users ENABLE ROW LEVEL SECURITY;
ALTER TABLE user_contacts ENABLE ROW LEVEL SECURITY;
ALTER TABLE task_completions ENABLE ROW LEVEL SECURITY;
ALTER TABLE reward_transactions ENABLE ROW LEVEL SECURITY;

-- Users can only access their own data
CREATE POLICY "Users can view own data" ON users FOR SELECT USING (auth.uid() = id);
CREATE POLICY "Users can update own data" ON users FOR UPDATE USING (auth.uid() = id);

-- Users can only access their own contacts
CREATE POLICY "Users can manage own contacts" ON user_contacts 
    FOR ALL USING (auth.uid() = user_id);

-- Users can only access their own task completions
CREATE POLICY "Users can manage own task completions" ON task_completions 
    FOR ALL USING (auth.uid() = user_id);

-- Users can only view their own reward transactions
CREATE POLICY "Users can view own rewards" ON reward_transactions 
    FOR SELECT USING (auth.uid() = user_id);
```

### **API Endpoints (Supabase Edge Functions)**

#### **Authentication Endpoints**
```typescript
// POST /auth/signup
interface SignupRequest {
  email: string;
  password: string;
  firstName: string;
  lastName: string;
  phone: string;
  companyDomain: string;
}

// POST /auth/signin
interface SigninRequest {
  email: string;
  password: string;
}

// POST /auth/refresh
interface RefreshRequest {
  refreshToken: string;
}
```

#### **Contact Management Endpoints**
```typescript
// POST /contacts/import
interface ImportContactsRequest {
  contacts: Array<{
    name: string;
    phoneNumber?: string;
    email?: string;
  }>;
}

// POST /contacts/swipe
interface SwipeContactRequest {
  contactId: string;
  direction: 'left' | 'right' | 'super_up';
  category?: 'customer' | 'recruit';
  tierLevel?: 1 | 2 | 3;
  isStarred?: boolean;
}

// GET /contacts/unprocessed
interface UnprocessedContactsResponse {
  contacts: UserContact[];
  totalCount: number;
  processedCount: number;
}
```

#### **Task Management Endpoints**
```typescript
// GET /tasks/weekly/:week
interface WeeklyTasksResponse {
  tasks: Array<{
    id: string;
    taskName: string;
    description: string;
    acceptanceCriteria: string;
    rewardAmount: number;
    completionStatus: string;
    completionDate?: string;
  }>;
}

// POST /tasks/complete
interface CompleteTaskRequest {
  taskId: string;
  verificationData?: {
    photos?: string[];
    gpsCoordinates?: Array<{lat: number; lng: number; timestamp: string}>;
    notes?: string;
  };
}

// GET /tasks/progress
interface TaskProgressResponse {
  currentWeek: number;
  weeklyProgress: Array<{
    week: number;
    tasksCompleted: number;
    tasksTotal: number;
    completionPercentage: number;
    earningsThisWeek: number;
  }>;
}
```

#### **Rewards & Payments Endpoints**
```typescript
// GET /rewards/transactions
interface RewardTransactionsResponse {
  transactions: Array<{
    id: string;
    transactionType: string;
    amount: number;
    description: string;
    status: string;
    createdAt: string;
  }>;
  totalEarned: number;
  totalPaid: number;
  pendingAmount: number;
}

// POST /rewards/request-payment
interface RequestPaymentRequest {
  amount: number;
  paymentMethod: 'stripe' | 'paypal';
  accountDetails: Record<string, any>;
}
```

---

## 🔌 **External Integrations**

### **Payment Processing (Stripe)**
```typescript
// Stripe Integration Service
class StripeService {
  private stripe: Stripe;
  
  constructor(secretKey: string) {
    this.stripe = new Stripe(secretKey, { apiVersion: '2023-10-16' });
  }
  
  async createPayoutToRep(repId: string, amount: number): Promise<void> {
    // Create connected account for rep if not exists
    const account = await this.getOrCreateConnectedAccount(repId);
    
    // Create payout
    await this.stripe.transfers.create({
      amount: amount * 100, // Convert to cents
      currency: 'usd',
      destination: account.id,
    });
  }
  
  async getOrCreateConnectedAccount(repId: string): Promise<Stripe.Account> {
    // Implementation for creating Stripe connected accounts
  }
}
```

### **SMS Notifications (Twilio)**
```typescript
// Twilio Integration Service
class TwilioService {
  private client: Twilio;
  
  constructor(accountSid: string, authToken: string) {
    this.client = new Twilio(accountSid, authToken);
  }
  
  async sendTaskReminder(phoneNumber: string, taskName: string): Promise<void> {
    await this.client.messages.create({
      body: `RepX Reminder: Complete "${taskName}" to earn your reward! 💰`,
      from: process.env.TWILIO_PHONE_NUMBER,
      to: phoneNumber,
    });
  }
  
  async sendRewardNotification(phoneNumber: string, amount: number): Promise<void> {
    await this.client.messages.create({
      body: `🎉 Congratulations! You've earned $${amount} in RepX rewards!`,
      from: process.env.TWILIO_PHONE_NUMBER,
      to: phoneNumber,
    });
  }
}
```

### **Email Service (SendGrid)**
```typescript
// SendGrid Integration Service
class EmailService {
  private sgMail: MailService;
  
  constructor(apiKey: string) {
    this.sgMail = new MailService();
    this.sgMail.setApiKey(apiKey);
  }
  
  async sendWeeklyProgress(email: string, progressData: WeeklyProgress): Promise<void> {
    const msg = {
      to: email,
      from: 'noreply@repx.app',
      templateId: 'd-weekly-progress-template',
      dynamicTemplateData: {
        firstName: progressData.firstName,
        weekNumber: progressData.weekNumber,
        tasksCompleted: progressData.tasksCompleted,
        tasksTotal: progressData.tasksTotal,
        earningsThisWeek: progressData.earningsThisWeek,
      },
    };
    
    await this.sgMail.send(msg);
  }
}
```

---

## 📊 **Analytics & Monitoring**

### **Application Monitoring**
```typescript
// Analytics Service
class AnalyticsService {
  async trackUserEvent(userId: string, eventName: string, properties: Record<string, any>): Promise<void> {
    // Track user events for product analytics
    await supabase
      .from('user_events')
      .insert({
        user_id: userId,
        event_name: eventName,
        properties,
        timestamp: new Date().toISOString(),
      });
  }
  
  async trackContactSwipe(userId: string, swipeDirection: string, category?: string): Promise<void> {
    await this.trackUserEvent(userId, 'contact_swiped', {
      swipe_direction: swipeDirection,
      category,
      timestamp: new Date().toISOString(),
    });
  }
  
  async trackTaskCompletion(userId: string, taskId: string, rewardAmount: number): Promise<void> {
    await this.trackUserEvent(userId, 'task_completed', {
      task_id: taskId,
      reward_amount: rewardAmount,
      timestamp: new Date().toISOString(),
    });
  }
}
```

### **Performance Metrics**
- **App Performance**: Monitor app launch time, screen load times, crash rates
- **API Performance**: Track response times, error rates, throughput
- **User Engagement**: Daily/monthly active users, session duration, feature usage
- **Business Metrics**: Contact processing rates, task completion rates, retention rates

---

## 🔒 **Security Specifications**

### **Data Protection**
```typescript
// Encryption Service
class EncryptionService {
  private readonly algorithm = 'aes-256-gcm';
  private readonly keyLength = 32;
  
  encrypt(text: string, key: Buffer): { encrypted: string; iv: string; tag: string } {
    const iv = crypto.randomBytes(16);
    const cipher = crypto.createCipher(this.algorithm, key, iv);
    
    let encrypted = cipher.update(text, 'utf8', 'hex');
    encrypted += cipher.final('hex');
    
    const tag = cipher.getAuthTag();
    
    return {
      encrypted,
      iv: iv.toString('hex'),
      tag: tag.toString('hex'),
    };
  }
  
  decrypt(encryptedData: { encrypted: string; iv: string; tag: string }, key: Buffer): string {
    const decipher = crypto.createDecipher(
      this.algorithm,
      key,
      Buffer.from(encryptedData.iv, 'hex')
    );
    
    decipher.setAuthTag(Buffer.from(encryptedData.tag, 'hex'));
    
    let decrypted = decipher.update(encryptedData.encrypted, 'hex', 'utf8');
    decrypted += decipher.final('utf8');
    
    return decrypted;
  }
}
```

### **Authentication & Authorization**
- **JWT Tokens**: Short-lived access tokens (15 minutes) with refresh tokens (7 days)
- **Multi-Factor Authentication**: SMS-based 2FA for sensitive operations
- **Role-Based Access Control**: Rep, Manager, Admin roles with different permissions
- **API Rate Limiting**: Prevent abuse with rate limiting on all endpoints

### **Privacy Compliance**
- **GDPR Compliance**: Data deletion, export, and consent management
- **CCPA Compliance**: California privacy law compliance
- **Data Retention**: Automatic deletion of contact data after program completion
- **Audit Logging**: Complete audit trail of all data access and modifications

---

## 📱 **Mobile-Specific Requirements**

### **iOS Requirements**
- **Minimum Version**: iOS 13.0+
- **Permissions**: Contacts, Location, Camera, Notifications
- **App Store Guidelines**: Compliance with App Store Review Guidelines
- **TestFlight**: Beta testing distribution

### **Android Requirements**
- **Minimum SDK**: API Level 26 (Android 8.0)
- **Target SDK**: API Level 34 (Android 14)
- **Permissions**: READ_CONTACTS, ACCESS_FINE_LOCATION, CAMERA, RECEIVE_BOOT_COMPLETED
- **Google Play**: Compliance with Google Play Developer Policy

### **Cross-Platform Considerations**
- **Responsive Design**: Adapt to different screen sizes and orientations
- **Platform-Specific UI**: Follow iOS Human Interface Guidelines and Material Design
- **Performance Optimization**: 60fps animations, efficient memory usage
- **Battery Optimization**: Background task management, efficient location services

---

## 🚀 **Deployment & DevOps**

### **CI/CD Pipeline**
```yaml
# GitHub Actions Workflow
name: RepX Mobile CI/CD

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.16.0'
      - run: flutter pub get
      - run: flutter test
      - run: flutter analyze

  build-ios:
    runs-on: macos-latest
    needs: test
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
      - run: flutter build ios --release --no-codesign

  build-android:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
      - run: flutter build apk --release
      - run: flutter build appbundle --release
```

### **Environment Management**
- **Development**: Local development with Supabase local instance
- **Staging**: Staging environment for testing with production-like data
- **Production**: Production environment with monitoring and alerting

### **Monitoring & Alerting**
- **Application Monitoring**: Sentry for error tracking and performance monitoring
- **Infrastructure Monitoring**: Supabase built-in monitoring and custom dashboards
- **Business Metrics**: Custom dashboards for retention rates, revenue, user engagement
- **Alerting**: PagerDuty for critical alerts, Slack for non-critical notifications

---

## 📋 **Development Timeline**

### **Phase 1: Foundation (Weeks 1-4)**
- **Week 1**: Project setup, authentication, basic UI framework
- **Week 2**: Contact import and basic swiping interface
- **Week 3**: Database schema, basic task management
- **Week 4**: Reward system foundation, payment integration

### **Phase 2: Core Features (Weeks 5-8)**
- **Week 5**: Complete contact categorization system
- **Week 6**: 28-day program structure and task completion
- **Week 7**: Progress tracking and analytics dashboard
- **Week 8**: Reward distribution and payment processing

### **Phase 3: Polish & Launch (Weeks 9-12)**
- **Week 9**: UI/UX refinement, animations, gamification
- **Week 10**: Testing, bug fixes, performance optimization
- **Week 11**: App store submission, documentation
- **Week 12**: Launch preparation, monitoring setup

---

**🎯 These technical specifications provide the complete blueprint for building RepX MVP with all necessary components for frontend, backend, integrations, and deployment.**
