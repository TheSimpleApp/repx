# RepX App Structure - FlutterFlow Ready
**Simple, Mobile-First Architecture for the 4 Core RepX Systems**

---

## 📱 **App Architecture Overview**

RepX is a single-user mobile app built with FlutterFlow, focused on the new sales rep experience. The app follows a tab-based navigation with modal overlays for primary interactions.

**Target User**: New sales rep during their first 28+ days  
**Primary Goal**: Contact swiping → Recruiting game → 28-day success → Customer wins

---

## 🏗️ **Navigation Structure**

### **Primary Navigation: Bottom Tab Bar (4 Tabs)**

```
┌─────────────────────────────────────────┐
│                App Bar                   │
├─────────────────────────────────────────┤
│                                         │
│            Page Content                 │
│                                         │
├─────────────────────────────────────────┤
│  📱     🎯     📈     👤             │
│ Contacts Recruit Progress Profile      │
└─────────────────────────────────────────┘
```

#### **Tab Structure**:
1. **Contacts (📱)**: Contact swiping interface - main feature
2. **Recruit (🎯)**: Recruiting gamification tiers and progress  
3. **Progress (📈)**: 28-day ramp program and lead tracker
4. **Profile (👤)**: Settings, help, company info

### **Key Modal Overlays**
- **Contact Swipe Interface**: Full-screen swipe modal (primary interaction)
- **Prospect Type Selector**: Modal for Recruit/Customer/Both selection  
- **Achievement Celebrations**: Full-screen celebration modals
- **Task Completion**: Modal for marking tasks complete
- **Reward Claims**: Modal for claiming tier rewards

---

## 📄 **Page Structure & Components**

### **1. Contacts Page (Primary Feature)**
*The Tinder-like contact swiping interface*

#### **Layout Structure**:
```
App Bar: "RepX" Logo + Contact Count Progress
├── Import Contacts Card (if not imported)
│   ├── "Import Phone Contacts" Button
│   └── Privacy Info Text
├── Swipe Interface (Main Feature)
│   ├── Current Contact Card
│   │   ├── Contact Name (Large)
│   │   ├── Phone Number
│   │   ├── Any Available Info
│   │   └── Swipe Instructions
│   ├── Action Buttons Row
│   │   ├── Pass (Left) ❌  
│   │   ├── Super Swipe (Up) ⭐
│   │   └── Yes (Right) ✅
│   └── Progress Bar (X of Y contacts)
└── Stats Summary Card
    ├── Contacts Processed
    ├── Recruits Identified  
    └── Customers Identified
```

#### **FlutterFlow Components**:
- **AppBar**: Custom with logo and progress indicator
- **Card**: Contact display, stats, import prompt
- **GestureDetector**: Swipe gesture recognition
- **AnimatedContainer**: Smooth card transitions  
- **ProgressIndicator**: Contact progress tracking
- **BottomSheet**: Prospect type selection modal

### **2. Recruit Page (Gamification Hub)**
*6-tier recruiting game progress and rewards*

#### **Layout Structure**:
```
App Bar: "Recruiting Game" + Help Icon
├── Overall Progress Card
│   ├── Total Recruits Submitted
│   ├── Total Recruits Hired
│   └── Next Tier Progress Bar
├── Submissions Tiers Section
│   ├── "Recruits Submitted" Header
│   ├── Tier 1 Card (e.g., 5 → Work Shirt)
│   ├── Tier 2 Card (e.g., 10 → $50 Prize)  
│   └── Tier 3 Card (e.g., 15 → $500 Experience)
├── Hires Tiers Section
│   ├── "Recruits Hired" Header
│   ├── Tier 1 Card (e.g., 1 → Prize)
│   ├── Tier 2 Card (e.g., 3 → Experience)
│   └── Tier 3 Card (e.g., 5 → Company Trip)
└── Recent Recruits List
    └── Quick status of submitted recruits
```

#### **FlutterFlow Components**:
- **LinearProgressIndicator**: Tier progress bars
- **Card**: Tier display with rewards
- **Badge**: Achievement status indicators  
- **ListView**: Recent recruits with status
- **Button**: Claim reward buttons
- **Modal**: Achievement celebration screens

### **3. Progress Page (28-Day + Lead Tracker)**
*28-day ramp program and customer lead tracking*

#### **Layout Structure**:
```
App Bar: "My Progress" + Calendar Icon
├── 28-Day Program Card
│   ├── Current Day Indicator
│   ├── This Week's Tasks
│   ├── Progress Bar (Days Complete)
│   └── Next Milestone Info
├── Weekly Sections
│   ├── Week 1-2: Foundation Tasks
│   │   ├── Task List with Checkboxes
│   │   ├── Cash Rewards Earned
│   │   └── Completion Status
│   ├── Week 3-4: Outcome Tasks  
│   │   ├── Task List with Checkboxes
│   │   ├── Cash Rewards Earned
│   │   └── Completion Status
├── Lead Tracker Section
│   ├── "My Customer Prospects" Header
│   ├── Leads from Contact Swiping
│   ├── Opportunity Status Tracking
│   └── First Win Celebration Area
└── Fast Start Leaderboard (Optional)
    ├── "14-Day Fast Start" Header
    ├── Days Remaining Counter
    ├── Current Tier Progress
    └── Tier Rewards Preview
```

#### **FlutterFlow Components**:
- **Timeline**: Visual 28-day program progress
- **Checkbox**: Task completion tracking
- **Card**: Weekly sections and lead cards
- **ProgressIndicator**: Multiple progress tracking
- **ListView**: Tasks and leads with status
- **Button**: Mark complete, claim rewards

### **4. Profile Page (Settings & Info)**
*Simple settings and company information*

#### **Layout Structure**:
```
App Bar: "Profile"
├── User Info Card
│   ├── Rep Name
│   ├── Company Name
│   ├── Start Date
│   └── Days in Program
├── Quick Stats Card
│   ├── Total Contacts Processed
│   ├── Total Recruits Submitted
│   ├── Current 28-Day Progress
│   └── Rewards Earned
├── Settings Section
│   ├── Notification Settings
│   ├── Privacy Settings
│   └── Contact Permissions
├── Help Section
│   ├── How RepX Works
│   ├── Contact Support
│   └── Video Tutorials
└── Company Section
    ├── About [Company Name]
    ├── Manager Contact
    └── Company Resources
```

#### **FlutterFlow Components**:
- **CircleAvatar**: User profile representation
- **ListTile**: Settings and menu options
- **Switch**: Toggle settings
- **Card**: Stats and info display
- **Divider**: Section separators

---

## 🎨 **Design System**

### **Color Palette (Gamified)**
```dart
Primary Colors:
- Success Green: #10b981 (achievements, completed)
- Energy Orange: #f59e0b (action, swipe right)  
- Warning Red: #ef4444 (pass, swipe left)
- Star Gold: #fbbf24 (super swipe, premium)
- Progress Blue: #3b82f6 (progress bars, information)

Neutral Colors:
- Background: #ffffff (clean, mobile-first)
- Surface: #f9fafb (cards, containers)  
- Text Primary: #111827 (main content)
- Text Secondary: #6b7280 (helper text)
- Border: #e5e7eb (subtle separators)
```

### **Typography (Mobile-Optimized)**
```dart
Display Styles:
- Contact Name: 24px, Bold (swipe interface)
- Tier Rewards: 20px, Bold (gamification)
- Progress Headers: 18px, Medium (sections)
- Body Text: 16px, Regular (readable on mobile)
- Helper Text: 14px, Regular (secondary info)
- Button Text: 16px, Medium (clear actions)
```

### **Component Specifications**

#### **Contact Swipe Card**
```dart
Swipe Card:
- Size: 300x400px (optimal for swipe)
- Border Radius: 20px (modern, friendly)
- Shadow: Subtle elevation for depth
- Background: White with colored border (status)
- Animation: Smooth card transitions
```

#### **Tier Progress Cards**
```dart
Tier Card:
- Height: 120px (compact, scannable)  
- Border Radius: 16px
- Progress Bar: Full width, 8px height
- Colors: Green (complete), Blue (in progress), Gray (pending)
- Badge: Achievement indicator overlay
```

#### **Task Completion Items**
```dart
Task Item:
- Height: 56px (thumb-friendly)
- Checkbox: 24px, left-aligned
- Text: 16px, clear and actionable
- Cash Value: Bold, right-aligned
- Completion Animation: Check mark with celebration
```

---

## 🔄 **Key User Flows**

### **Primary Flow: Contact Swiping**
```
App Launch → Contacts Tab → Import Contacts → Start Swiping
│
├── Left Swipe (Pass) → Next Contact
├── Right Swipe (Yes) → Prospect Type Modal → Select Type → Next Contact  
└── Up Swipe (Super) → Prospect Type Modal → Select Type → Next Contact
```

### **Recruiting Game Flow**  
```
Contact Swiped as Recruit → Auto-Added to Submissions → Check Tiers → Progress Update
│
└── Company Confirms Hire → Auto-Added to Hires → Check Tiers → Reward Unlock
```

### **28-Day Program Flow**
```
Daily Check-in → Progress Tab → This Week's Tasks → Mark Complete → Cash Reward
│
├── Week 1-2: Foundation Tasks (Rep Control)
└── Week 3-4: Outcome Tasks (Results-Based)
```

### **Lead Tracker Flow**
```
Contact Swiped as Customer → Added to Lead Tracker → Approach Contact → Mark as Opportunity → Fast Start Progress
```

---

## 📊 **App State Management**

### **Core App State**
```dart
RepXAppState {
  // User & Company
  User currentRep
  Company companyConfig
  
  // Core Data  
  List<Contact> phoneContacts
  List<ContactSwipe> swipedContacts
  List<RecruitingTier> recruitingTiers
  List<Task28Day> programTasks
  List<CustomerLead> customerLeads
  
  // Progress Tracking
  int currentDay
  double contactProgress (%)
  int recruitsSubmitted
  int recruitsHired  
  double cashEarned
  List<Achievement> unlockedRewards
  
  // UI State
  int selectedTabIndex
  bool isSwipeMode
  Contact? currentSwipeContact
  bool isLoading
}
```

### **Data Sync Strategy**
- **Offline-First**: All swiping works offline, sync when online
- **Real-Time**: Company updates (hire confirmations) sync immediately  
- **Progressive**: Load contacts in batches for smooth performance
- **Optimistic**: UI updates immediately, server confirms later

---

## 🚀 **FlutterFlow Implementation Checklist**

### **Phase 1: Contact Swiping System**
- [ ] Contact import and permission handling
- [ ] Swipe gesture detection and animations
- [ ] Prospect type selection modal
- [ ] Progress tracking and local storage
- [ ] Contact categorization and sync

### **Phase 2: Recruiting Gamification**  
- [ ] Tier configuration from company settings
- [ ] Progress calculation and display
- [ ] Achievement unlock animations
- [ ] Reward claim workflow
- [ ] Company admin integration

### **Phase 3: 28-Day Program**
- [ ] Task configuration and display
- [ ] Progress tracking and completion
- [ ] Cash reward calculation
- [ ] Weekly milestone celebrations  
- [ ] Program completion analytics

### **Phase 4: Lead Tracker & Polish**
- [ ] Customer lead management
- [ ] Fast Start leaderboard
- [ ] Performance optimization
- [ ] User testing and refinement
- [ ] App store preparation

---

## 🔧 **Technical Architecture**

### **Database Structure** 
- **Supabase**: Primary database (user prefs + company data)
- **Local Storage**: Contact swiping and offline progress
- **Real-time**: Company updates and achievement unlocks
- **Security**: Encrypted contact storage, secure sync

### **Key Integrations**
- **Contact API**: iOS/Android contact access
- **Payment Processing**: Cash reward distribution
- **Push Notifications**: Achievement celebrations, daily reminders
- **Analytics**: User engagement and success tracking

---

**🎯 This app structure provides a focused, mobile-first RepX experience optimized for the single goal of turning new sales reps into successful recruiters while getting them their first customer win within 14 days.**
