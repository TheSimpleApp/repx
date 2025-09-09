# RepX Screen Specifications - MVP Prototype
**Complete Screen-by-Screen Breakdown for RepX's 4 Core Systems**

---

## 📱 **Navigation Overview: 4-Tab System**

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

**Tab Structure:**
1. **Contacts (📱)** - Tinder-like contact swiping interface
2. **Recruit (🎯)** - 6-tier recruiting gamification system  
3. **Progress (📈)** - 28-day program + lead tracker
4. **Profile (👤)** - Settings and company info

---

## 🏠 **Screen 1: Contacts Tab - Primary Feature**

### **Purpose & Context**
The heart of RepX - where new reps swipe through their personal contacts to identify potential recruits and customers. Designed like Tinder for maximum engagement and ease of use.

### **Layout Structure**
```
┌─────────────────────────────────────┐
│  RepX Logo    47 / 247    Import    │ ← App Bar with progress
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────┐   │ ← Contact Card (Main)
│  │                             │   │
│  │      Sarah Johnson          │   │ ← Contact Name (24px)
│  │    (555) 123-4567          │   │ ← Phone Number  
│  │                             │   │
│  │   Known from: College       │   │ ← Context (if available)
│  │                             │   │
│  │                             │   │
│  │     Swipe or tap below      │   │ ← Helper text
│  │                             │   │
│  └─────────────────────────────┘   │
│                                     │
│     ❌        ⭐        ✅        │ ← Swipe Action Buttons
│    Pass     Super      Yes        │   (56px+ touch targets)
│                                     │
│  Progress: █████████░░░ 19%        │ ← Progress Bar
│                                     │
│  Stats This Session:               │ ← Session Summary
│  • 12 Contacts processed           │
│  • 3 Potential customers          │
│  • 2 Potential recruits           │
│                                     │
├─────────────────────────────────────┤
│  📱  🎯  📈  👤                  │ ← Bottom Navigation
└─────────────────────────────────────┘
```

### **Key Interactive Elements**

#### **Contact Card Gestures:**
- **Left Swipe/❌ Button**: Pass (skip contact)
- **Right Swipe/✅ Button**: Interested → Opens Prospect Type Modal
- **Up Swipe/⭐ Button**: Super Swipe (high potential) → Opens Prospect Type Modal

#### **Prospect Type Modal:**
```
┌─────────────────────────────────────┐
│  What type of prospect is Sarah?    │ ← Modal Header
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────┐ ┌─────────────┐   │
│  │   🎯        │ │   🛍️        │   │ ← Option Cards
│  │ RECRUIT     │ │ CUSTOMER    │   │
│  │ New team    │ │ Potential   │   │
│  │ member      │ │ sale        │   │
│  └─────────────┘ └─────────────┘   │
│                                     │
│  ┌───────────────────────────────┐ │
│  │         🎯🛍️ BOTH            │ │ ← Combined Option  
│  │    Could be either/both       │ │
│  └───────────────────────────────┘ │
│                                     │
│        [Cancel] [Select]            │ ← Action Buttons
└─────────────────────────────────────┘
```

### **Empty States**

#### **No Contacts Imported:**
```
┌─────────────────────────────────────┐
│          📱 Import Contacts          │ ← Icon
│                                     │
│     Get started by importing        │
│     your phone contacts             │
│                                     │
│  ┌───────────────────────────────┐ │
│  │      Import Phone Contacts    │ │ ← Primary CTA
│  └───────────────────────────────┘ │
│                                     │
│  🔒 Your contacts are stored        │
│     securely and never shared      │
└─────────────────────────────────────┘
```

---

## 🎯 **Screen 2: Recruit Tab - Gamification Hub**

### **Purpose & Context**  
6-tier recruiting game showing progress toward rewards for both recruits submitted and recruits hired. Emphasizes achievements and motivation.

### **Layout Structure**
```
┌─────────────────────────────────────┐
│  Recruiting Game           🏆       │ ← App Bar with trophy
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────┐   │ ← Overall Progress Card
│  │  📊 Your Recruiting Stats    │   │
│  │                             │   │
│  │  7 Submitted  •  1 Hired    │   │ ← Key Numbers (large)
│  │                             │   │
│  │  Next Reward: 3 more for    │   │
│  │  Tier 2 - $50 Gift Card     │   │
│  │  ████████████░░░░ 70%       │   │ ← Progress Bar
│  └─────────────────────────────┘   │
│                                     │
│  RECRUIT SUBMISSIONS               │ ← Section Header
│  ┌─────────────────────────────┐   │
│  │ ✅ TIER 1 - Work Shirt      │   │ ← Completed Tier
│  │    5 submits • ACHIEVED!     │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ ⏳ TIER 2 - $50 Gift Card   │   │ ← In Progress 
│  │    7/10 submits • 30% more  │   │
│  │    █████████░░░░░░░░░ 70%   │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ 🔒 TIER 3 - $500 Experience │   │ ← Locked
│  │    0/15 submits • Locked    │   │
│  └─────────────────────────────┘   │
│                                     │
│  RECRUIT HIRES                     │ ← Section Header
│  ┌─────────────────────────────┐   │
│  │ ✅ TIER 1 - Premium Bonus   │   │ ← Completed Hire Tier
│  │    1 hire • ACHIEVED!       │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ 🔒 TIER 2 - Experience Day  │   │ ← Needs More Hires
│  │    1/3 hires • Need 2 more  │   │
│  └─────────────────────────────┘   │
│                                     │
│  Recent Activity                   │ ← Section Header
│  • John Smith - Interview today   │ ← Recent Recruits
│  • Lisa Wang - Hired! 🎉         │
│  • Mike Chen - Contacted          │
│                                     │
├─────────────────────────────────────┤
│  📱  🎯  📈  👤                  │ ← Bottom Navigation
└─────────────────────────────────────┘
```

### **Achievement Celebration Modal**
```
┌─────────────────────────────────────┐
│          🎉 TIER 2 ACHIEVED! 🎉     │ ← Full-screen celebration
│                                     │
│              🏆                     │ ← Trophy Icon (large)
│                                     │
│         $50 Gift Card               │ ← Reward (prominent)
│         UNLOCKED!                   │
│                                     │
│    You submitted 10 recruits!       │ ← Achievement details
│    You're building an amazing team! │
│                                     │
│  ┌───────────────────────────────┐ │
│  │      Claim Your Reward        │ │ ← Primary CTA
│  └───────────────────────────────┘ │
│                                     │
│           [Continue]                │ ← Secondary action
└─────────────────────────────────────┘
```

---

## 📈 **Screen 3: Progress Tab - 28-Day Program & Leads**

### **Purpose & Context**
Tracks the 28-day ramp program progress AND customer lead development. Shows both task completion (with cash rewards) and customer opportunity pipeline.

### **Layout Structure**
```
┌─────────────────────────────────────┐
│  My Progress     Day 15/28    📅    │ ← App Bar with day counter
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────┐   │ ← Program Overview Card
│  │  📊 28-Day Program          │   │
│  │                             │   │
│  │  Week 3 of 4 - Outcomes     │   │ ← Current Week Status
│  │  ████████████████░░░░ 54%   │   │
│  │                             │   │
│  │  💰 $475 earned so far      │   │ ← Cash Earned (prominent)
│  │  $125 pending this week     │   │
│  └─────────────────────────────┘   │
│                                     │
│  THIS WEEK'S TASKS (Week 3)        │ ← Section Header
│  ┌─────────────────────────────┐   │
│  │ ✅ Set 3 demos      +$50    │   │ ← Completed Task
│  │    Completed yesterday      │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ ⏳ Get 2 referrals  +$40    │   │ ← In Progress Task
│  │    1/2 complete • 50%       │   │
│  │    ████████░░░░░░░░ 50%     │   │
│  │    [Mark Complete]          │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ 📝 Schedule 5 inspections   │   │ ← Pending Task
│  │    +$75 reward              │   │
│  │    [Mark Complete]          │   │
│  └─────────────────────────────┘   │
│                                     │
│  MY CUSTOMER LEADS                 │ ← Section Header  
│  ┌─────────────────────────────┐   │
│  │ 🛍️ Sarah Johnson           │   │ ← Customer Lead
│  │    Demo scheduled Thu 2pm   │   │
│  │    From: Contact swiping    │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ ⭐ Mike Chen (CUSTOMER!)    │   │ ← First Win!
│  │    WON! Signed yesterday    │   │
│  │    Your first customer! 🎉  │   │
│  └─────────────────────────────┘   │
│                                     │
│  ⚡ FAST START (Day 15/14) DONE    │ ← Fast Start Complete
│  Final: 4 opportunities created     │
│  Tier 2 achieved! 🏆              │
│                                     │
├─────────────────────────────────────┤
│  📱  🎯  📈  👤                  │ ← Bottom Navigation
└─────────────────────────────────────┘
```

### **Task Completion Flow**
```
┌─────────────────────────────────────┐
│        Mark Task Complete?          │ ← Completion Modal
├─────────────────────────────────────┤
│                                     │
│  Task: Schedule 5 inspections       │
│  Reward: +$75 cash                 │
│                                     │
│  How many did you complete?         │
│  ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐   │ ← Number Input
│  │  1  │ │  2  │ │  3  │ │  4  │   │
│  └─────┘ └─────┘ └─────┘ └─────┘   │
│  ┌─────┐                           │
│  │  5  │ ✅ Complete               │
│  └─────┘                           │
│                                     │
│  Verification: 📸 Upload Photo      │ ← Verification Method
│  (Optional but recommended)         │
│                                     │
│      [Cancel] [Complete Task]       │ ← Actions
└─────────────────────────────────────┘
```

### **First Customer Win Celebration**
```
┌─────────────────────────────────────┐
│        🎊 YOUR FIRST CUSTOMER! 🎊   │ ← Major Milestone
│                                     │
│              💰                     │ ← Large icon
│                                     │
│         Mike Chen signed!           │ ← Customer name
│                                     │
│  You're now part of the 89% who     │ ← Success rate message
│  stay with the company long-term!   │
│                                     │
│  This changes everything!           │ ← Motivational message
│  The first customer is always       │
│  the hardest to get.               │
│                                     │
│  ┌───────────────────────────────┐ │
│  │     Celebrate! 🎉            │ │ ← Primary CTA
│  └───────────────────────────────┘ │
│                                     │
│        [Keep Going!]                │ ← Continue action
└─────────────────────────────────────┘
```

---

## 👤 **Screen 4: Profile Tab - Settings & Info**

### **Purpose & Context**
Simple profile management, company information, app settings, and help resources. Clean and focused on essential functions.

### **Layout Structure**
```
┌─────────────────────────────────────┐
│  Profile                    ⚙️      │ ← App Bar with settings
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────┐   │ ← User Info Card
│  │     👤 David Johnson         │   │ ← Name (large)
│  │                             │   │
│  │  Sales Rep • ABC Company    │   │ ← Role & Company
│  │  Started: March 15, 2024    │   │
│  │  Program Day: 15 of 28      │   │
│  └─────────────────────────────┘   │
│                                     │
│  ┌─────────────────────────────┐   │ ← Quick Stats Card
│  │  📊 Your RepX Stats         │   │
│  │                             │   │
│  │  247 Contacts processed     │   │ ← Key metrics
│  │  12 Recruits submitted      │   │
│  │  1 Recruit hired           │   │
│  │  $475 Cash earned          │   │
│  │  1 Customer won 🎉         │   │
│  └─────────────────────────────┘   │
│                                     │
│  SETTINGS                          │ ← Section Header
│  📔 Notifications              >    │ ← Settings Items
│  🔒 Privacy & Contacts         >    │
│  📱 Contact Permissions        >    │
│                                     │
│  HELP & SUPPORT                    │ ← Section Header  
│  ❓ How RepX Works             >    │ ← Help Items
│  📞 Contact Support            >    │
│  🎥 Video Tutorials            >    │
│  📖 Success Stories            >    │
│                                     │
│  COMPANY INFO                      │ ← Section Header
│  🏢 About ABC Company          >    │ ← Company Items
│  👨‍💼 Manager: John Smith        >    │
│  📚 Company Resources          >    │
│  🎯 Training Materials         >    │
│                                     │
│  ┌─────────────────────────────┐   │
│  │         Sign Out            │   │ ← Sign Out Button
│  └─────────────────────────────┘   │
│                                     │
├─────────────────────────────────────┤
│  📱  🎯  📈  👤                  │ ← Bottom Navigation
└─────────────────────────────────────┘
```

### **Settings Screens**

#### **Notification Settings:**
```
┌─────────────────────────────────────┐
│  ← Notifications                    │ ← Back navigation
├─────────────────────────────────────┤
│                                     │
│  Task Reminders              ●○○   │ ← Toggle switches
│  Achievement Celebrations    ●○○   │
│  Recruit Updates             ●○○   │
│  Weekly Progress             ●○○   │
│  Fast Start Updates          ●○○   │
│                                     │
│  TIMING                            │
│  Daily reminder at: 9:00 AM        │
│  Weekend reminders:  ○○● Off       │
│                                     │
│  SOUND & VIBRATION                 │
│  Notification sound:  Default      │
│  Vibration:          ●○○ On       │
│                                     │
└─────────────────────────────────────┘
```

---

## 🎯 **Key Design Patterns**

### **Success Messaging**
- **89% Retention**: Prominently featured in first customer win
- **Progress Reinforcement**: "You're on track for success!"
- **Achievement Celebrations**: Full-screen modals with confetti
- **Streak Recognition**: "5 days of consistent contact swiping"

### **Cash Emphasis**  
- **Green Color**: All cash amounts in RepX cash green
- **Large Typography**: Cash values prominently displayed
- **Real-time Updates**: Running totals update immediately
- **Payment Status**: Clear pending vs. paid indicators

### **Mobile Optimization**
- **56px Touch Targets**: All interactive elements
- **One-handed Usage**: Primary actions in thumb reach
- **Swipe Gestures**: Natural, responsive swipe interactions
- **Visual Feedback**: Immediate response to all actions

### **Gamification Elements**
- **Progress Bars**: Multiple progress indicators
- **Achievement Badges**: Visual tier completion markers
- **Celebrations**: Animated success celebrations
- **Tier Progression**: Clear next-goal visibility

---

## ✅ **Screen Implementation Checklist**

### **Contacts Tab:**
- [ ] Contact import and permission flow
- [ ] Smooth swipe gestures with visual feedback
- [ ] Prospect type selection modal
- [ ] Session progress tracking
- [ ] Empty state for no contacts

### **Recruit Tab:**
- [ ] 6-tier progress visualization  
- [ ] Achievement celebration modals
- [ ] Real-time progress updates
- [ ] Recent activity feed
- [ ] Reward claim workflow

### **Progress Tab:**
- [ ] 28-day program overview
- [ ] Weekly task management
- [ ] Cash earning tracking
- [ ] Customer lead pipeline
- [ ] First customer celebration

### **Profile Tab:**
- [ ] User stats summary
- [ ] Settings and preferences
- [ ] Help and support resources
- [ ] Company information access
- [ ] Clean sign out flow

**🎯 These screen specifications provide a complete blueprint for building RepX's mobile-first interface that drives new sales reps toward 89% retention through systematic contact mining and gamified success programs.**
