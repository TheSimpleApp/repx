# RepX User Flows - Complete Journey Maps
**Step-by-Step User Interactions for the 4 Core RepX Systems**

---

## 🎯 **User Flow Overview**

**Primary User**: New sales rep in their first 28+ days  
**Core Journey**: Contact Import → Swiping → Recruiting Game → 28-Day Program → Customer Wins

---

## 📱 **1. Contact Swiping System Flow**

### **Flow A: Initial Contact Import**
```
App Launch (First Time)
│
├─ User Registration & Company Setup
│  └─ Company assigns recruiting tiers & 28-day tasks
│
├─ Privacy Permission Request
│  ├─ "Allow Contact Access?" → User Grants Permission
│  └─ Show privacy policy & data security info
│
├─ Contact Import Process  
│  ├─ "Import Phone Contacts" button
│  ├─ Loading screen: "Importing 247 contacts..."
│  ├─ Success: "247 contacts imported securely"
│  └─ "Start Swiping" CTA button
│
└─ Tutorial: Contact Swiping Interface
   ├─ Show sample contact card
   ├─ Explain swipe gestures (←, →, ↑)
   ├─ Demo prospect type selection
   └─ "Got it! Let's start swiping"
```

### **Flow B: Daily Contact Swiping Session**
```
Contacts Tab Selected
│
├─ Progress Header: "47 of 247 contacts processed"
│
├─ Current Contact Card Display
│  ├─ Contact Name (Large)
│  ├─ Phone Number
│  ├─ Any available info
│  └─ Action hint: "Swipe or tap buttons"
│
├─ User Swipe Action:
│  │
│  ├─ LEFT SWIPE (Pass)
│  │  ├─ Card slides left with animation
│  │  ├─ Next contact loads automatically
│  │  └─ Progress updates: "48 of 247"
│  │
│  ├─ RIGHT SWIPE (Yes)
│  │  ├─ Card slides right with checkmark
│  │  ├─ Prospect Type Modal appears:
│  │  │  ├─ "What type of prospect?"
│  │  │  ├─ [Recruit] [Customer] [Both] buttons
│  │  │  └─ User selects → Modal closes
│  │  ├─ Brief success animation
│  │  ├─ Next contact loads  
│  │  └─ Progress updates: "48 of 247"
│  │
│  └─ UP SWIPE (Super/Star)
│     ├─ Card flies up with star animation
│     ├─ Prospect Type Modal appears:
│     │  ├─ "High-potential prospect!"
│     │  ├─ [Recruit] [Customer] [Both] buttons
│     │  └─ User selects → Modal closes
│     ├─ Special "⭐ Super Prospect" celebration
│     ├─ Next contact loads
│     └─ Progress updates: "48 of 247"
│
├─ Session Progress Tracking
│  ├─ Visual progress bar updates
│  ├─ Running totals: "12 Recruits, 8 Customers identified"
│  ├─ Session milestone: "Great job! 50 contacts processed"
│  └─ Option to continue or take a break
│
└─ Session Complete
   ├─ "Session complete! 25 contacts processed today"
   ├─ Summary stats: "3 potential recruits, 5 potential customers"
   ├─ Motivational message: "You're building your future!"
   └─ "Continue tomorrow" or "Process more now"
```

---

## 🎯 **2. Recruiting Gamification Flow**

### **Flow C: Recruit Submission Process**
```
Recruit Tab Selected
│
├─ Tier Progress Overview
│  ├─ "Recruits Submitted: 7 / 10 for Tier 2"
│  ├─ "Recruits Hired: 0 / 1 for Tier 1" 
│  └─ Progress bars for each tier
│
├─ Recent Activity
│  ├─ List of recently submitted recruits
│  ├─ Status updates: "John Smith - Interview Scheduled"
│  └─ "Submit New Recruit" button
│
├─ Automatic Submissions (from swiping)
│  ├─ When contact swiped as "Recruit"
│  ├─ Auto-creates recruit submission
│  ├─ Shows brief confirmation: "Recruit submitted!"
│  ├─ Updates tier progress immediately
│  └─ Checks for tier achievements
│
├─ Tier Achievement Flow
│  │
│  ├─ Tier Unlock Detection
│  │  └─ User hits submission/hire threshold
│  │
│  ├─ Full-Screen Celebration
│  │  ├─ "🎉 TIER 2 ACHIEVED! 🎉"
│  │  ├─ Reward display: "$50 Gift Card"
│  │  ├─ Confetti animation
│  │  └─ "Claim Reward" button
│  │
│  ├─ Reward Claim Process
│  │  ├─ Reward details modal
│  │  ├─ How to claim instructions
│  │  ├─ "Contact [Manager] to claim"
│  │  └─ Mark as claimed
│  │
│  └─ Progress Update
│     ├─ Tier marked as completed
│     ├─ Focus shifts to next tier
│     └─ Updated progress display
│
└─ Ongoing Status Tracking
   ├─ Company updates recruit status
   ├─ Push notification: "John Smith hired! 🎉"
   ├─ Auto-updates hire count
   ├─ Checks hire tier thresholds
   └─ Triggers hire tier celebrations
```

### **Flow D: Hire Confirmation & Rewards**
```
Company Admin Action (Background)
├─ Recruiter confirms: "John Smith hired"
├─ Database updates: hire status = 'hired'
└─ Triggers user notification

Rep Receives Notification
│
├─ Push Notification: "Great news! John Smith was hired!"
├─ Open app → Recruit tab
├─ Automatic tier check: User now has 1 hire
│
├─ Tier 1 Hire Achievement
│  ├─ Full-screen celebration: "🎉 FIRST HIRE! 🎉"
│  ├─ Reward display: "[Company Custom Reward]"
│  ├─ "This is just the beginning!"
│  └─ Progress update: Working toward Tier 2 (3 hires)
│
└─ Updated Recruit Tab
   ├─ Hire count: "1 recruit hired"
   ├─ Progress toward next tier
   ├─ Success story: "John Smith - Success Story"
   └─ Motivation: "Keep building your team!"
```

---

## 📈 **3. 28-Day Ramp Program Flow**

### **Flow E: Daily Task Management**
```
Progress Tab Selected
│
├─ Program Overview Header
│  ├─ "Day 12 of 28" with progress bar
│  ├─ Current week: "Week 2 - Foundation"
│  └─ "This week's focus: [Company Custom]"
│
├─ Today's Tasks Section
│  ├─ "Today's Tasks (Week 2)" header
│  ├─ Task list with checkboxes:
│  │  ├─ ☐ "Make 50 door contacts" ($25 cash)
│  │  ├─ ☑ "Complete training module 4" ($15 cash) ✓
│  │  ├─ ☐ "Attend team meeting" ($10 cash)
│  │  └─ ☐ "Submit 2 recruits" ($20 cash)
│  └─ Daily total: "$45 available today"
│
├─ Task Completion Flow
│  │
│  ├─ User taps task checkbox
│  │
│  ├─ Task Completion Modal
│  │  ├─ "Mark task complete?"
│  │  ├─ Task details & requirements
│  │  ├─ Verification method:
│  │  │  ├─ Self-report: "I completed this task"
│  │  │  ├─ Photo: "Upload verification photo"
│  │  │  └─ GPS: Auto-verify location
│  │  └─ [Mark Complete] button
│  │
│  ├─ Task Completion Celebration
│  │  ├─ Checkmark animation
│  │  ├─ Cash reward notification: "+$25 earned!"
│  │  ├─ Progress update
│  │  └─ Brief motivational message
│  │
│  └─ Updated Progress Display
│     ├─ Task marked complete
│     ├─ Daily progress updates
│     ├─ Running cash total updates
│     └─ Next task highlighted
│
├─ Weekly Milestone Achievement
│  │
│  ├─ Week Completion Detection
│  │  └─ All required week tasks complete
│  │
│  ├─ Weekly Celebration
│  │  ├─ "🎉 WEEK 2 COMPLETE! 🎉"  
│  │  ├─ Weekly cash total: "$175 earned this week"
│  │  ├─ Progress: "Halfway through foundation phase!"
│  │  └─ Preview: "Week 3 unlocked - Outcome tasks begin!"
│  │
│  └─ Program Progression
│     ├─ Week 3 tasks unlock
│     ├─ Difficulty increases (outcome-based)
│     ├─ Higher cash rewards available
│     └─ Focus shifts to results
│
└─ 28-Day Program Completion
   ├─ Final task completion triggers celebration
   ├─ "🎊 PROGRAM COMPLETE! 🎊"
   ├─ Total cash earned: "$850"
   ├─ Success rate display: "Part of the 89% who succeed!"
   └─ Transition to ongoing success mode
```

### **Flow F: Weekly Progress Transitions**
```
Week Progression Flow

Week 1-2: Foundation Tasks (Rep Control)
├─ Tasks fully within rep control
├─ Examples: Door knocks, training, meetings
├─ Cash rewards: $15-$25 per task
├─ Focus: Building habits & confidence
└─ Success rate: Target 90%+ completion

Transition to Week 3
├─ "Foundation phase complete!"
├─ "Ready for outcome-based challenges?"
├─ Preview higher cash rewards
└─ Motivational messaging

Week 3-4: Outcome Tasks (Results-Based)  
├─ Tasks based on business outcomes
├─ Examples: Demos set, opportunities created
├─ Cash rewards: $25-$50 per task
├─ Focus: Generating real business results
└─ Success rate: Target 75%+ completion

Program Completion
├─ All 4 weeks complete
├─ Total cash earned calculation
├─ Performance analytics
├─ Transition to ongoing rep activities
└─ Success celebration & recognition
```

---

## 🛍️ **4. Lead Tracker & Customer Win Flow**

### **Flow G: Customer Lead Development**
```
Customer Lead Creation (from Contact Swiping)
├─ Contact swiped as "Customer" or "Both"  
├─ Automatically added to Lead Tracker
├─ Appears in Progress Tab → Lead section
└─ Status: "New Prospect"

Lead Management Flow
│
├─ Lead List Display
│  ├─ "Sarah Johnson - New Prospect"
│  ├─ "Mike Chen - Contacted"  
│  ├─ "Lisa Wang - Opportunity Scheduled"
│  └─ Tap lead → Lead Detail Modal
│
├─ Lead Action Flow
│  │
│  ├─ Contact Lead
│  │  ├─ Tap "Contact" button
│  │  ├─ Choose method: Call, Text, Email
│  │  ├─ Log contact attempt
│  │  └─ Update status to "Contacted"
│  │
│  ├─ Create Opportunity
│  │  ├─ Lead shows interest
│  │  ├─ "Schedule Demo/Inspection" button
│  │  ├─ Set date and type
│  │  ├─ Status → "Opportunity Scheduled"
│  │  └─ Counts for Fast Start program
│  │
│  └─ Win Customer
│     ├─ Opportunity converts to sale
│     ├─ "Mark as Customer" button
│     ├─ Customer details & value entry
│     ├─ Status → "Customer Won"
│     └─ Trigger first win celebration
│
├─ First Customer Win Flow
│  │
│  ├─ First Win Detection
│  │  └─ first_customer_won = true trigger
│  │
│  ├─ Major Celebration
│  │  ├─ "🎊 YOUR FIRST CUSTOMER! 🎊"
│  │  ├─ "You're now part of the 89% success rate!"
│  │  ├─ Confetti & celebration animation
│  │  ├─ Customer details display
│  │  └─ "This changes everything!"
│  │
│  ├─ Success Milestone Tracking
│  │  ├─ Mark achievement in progress
│  │  ├─ Update retention probability
│  │  ├─ Notify manager of success
│  │  └─ Unlock ongoing rep features
│  │
│  └─ Motivation Boost
│     ├─ "The first is the hardest!"
│     ├─ "Now let's get customer #2"
│     ├─ Lead generation tips
│     └─ Focus on building customer base
│
└─ Ongoing Lead Development
   ├─ Continue working contact leads
   ├─ Build systematic approach
   ├─ Track conversion rates
   └─ Optimize lead generation
```

### **Flow H: 14-Day Fast Start Program**
```
Fast Start Program Activation
├─ Automatically starts on Day 1
├─ Runs parallel to 28-day program
├─ Focus: Opportunity creation speed
└─ 14-day time limit for all opportunities

Daily Fast Start Flow
│
├─ Fast Start Section (in Progress Tab)
│  ├─ "Fast Start: Day 8 of 14" 
│  ├─ "Opportunities Created: 3"
│  ├─ Current tier: "Tier 1 Complete"
│  └─ Progress toward Tier 2
│
├─ Opportunity Creation
│  ├─ Customer lead → Opportunity scheduled
│  ├─ Auto-counts for Fast Start
│  ├─ Real-time tier progress update
│  └─ Check tier achievement
│
├─ Fast Start Tier Achievement
│  │
│  ├─ Tier Completion Detection
│  │  └─ Opportunity count hits tier threshold
│  │
│  ├─ Fast Start Celebration  
│  │  ├─ "⚡ FAST START TIER 2! ⚡"
│  │  ├─ "3 opportunities in 8 days!"
│  │  ├─ Tier reward display
│  │  └─ Progress toward next tier
│  │
│  └─ Leaderboard Update
│     ├─ Position among other reps
│     ├─ Days remaining: "6 days left!"
│     ├─ Next tier requirements
│     └─ Competitive motivation
│
├─ Fast Start Completion (Day 14)
│  ├─ Program completion notification
│  ├─ Final tier achievement
│  ├─ Total opportunities summary
│  ├─ Leaderboard final position
│  └─ "Fast Start graduate!" badge
│
└─ Post-Fast Start
   ├─ Badge remains permanent
   ├─ Achievement unlocked in profile  
   ├─ Focus returns to 28-day program
   └─ Ongoing opportunity development
```

---

## 🎮 **5. Integrated Gamification Elements**

### **Flow I: Daily Engagement Loop**
```
Daily App Open
├─ Welcome message: "Day 15 - Let's make it count!"
├─ Quick progress overview: 4 systems
├─ Today's priority actions highlighted
└─ Motivational streak tracking

Progress Momentum Building
│
├─ Contact Swiping Progress
│  ├─ "47 contacts remaining"
│  ├─ Session goal: "Process 10 more today"
│  └─ Streak: "5 days of consistent swiping"
│
├─ Recruiting Game Momentum  
│  ├─ "2 more recruits for Tier 2 reward"
│  ├─ Recent activity: "John Smith - Interview tomorrow"
│  └─ Team impact: "You've helped grow the team!"
│
├─ 28-Day Program Momentum
│  ├─ "3 tasks left this week"
│  ├─ Cash available: "$65 remaining this week"
│  └─ Week completion: "85% through Week 2"
│
└─ Lead Development Momentum
   ├─ "Follow up with Sarah Johnson today"
   ├─ Opportunity pipeline: "2 demos scheduled"
   └─ Fast Start: "Tier 3 within reach!"

Achievement Recognition System
│
├─ Celebration Triggers
│  ├─ Task completion → Immediate cash animation
│  ├─ Tier achievement → Full-screen celebration  
│  ├─ First customer → Major milestone party
│  ├─ Week completion → Progress celebration
│  └─ Streak milestones → Consistency recognition
│
├─ Progress Visualization
│  ├─ Multiple progress bars across systems
│  ├─ Achievement badges and trophies
│  ├─ Streak counters and consistency metrics
│  ├─ Cash earned running total
│  └─ Success probability indicators
│
└─ Motivational Messaging
   ├─ Context-aware encouragement
   ├─ Success rate reinforcement
   ├─ Peer comparison (when beneficial)
   ├─ Company-specific messaging
   └─ Personal milestone celebrations
```

---

## 🔄 **6. Cross-System Integration Flows**

### **Flow J: How the 4 Systems Work Together**

```
Complete RepX User Journey Integration

Day 1-3: Foundation Setup
├─ Import contacts → Contact Swiping System
├─ Learn recruiting tiers → Recruiting Game System
├─ Start first tasks → 28-Day Program System
└─ Begin lead identification → Lead Tracker System

Week 1: Building Momentum
├─ Daily contact swiping sessions
├─ Foundation tasks (within control)  
├─ First recruits submitted
├─ Customer prospects identified
└─ Fast Start program tracking

Week 2: Gaining Confidence  
├─ Consistent contact processing
├─ More recruits submitted → Tier 1 achieved
├─ Foundation tasks completed → Cash rewards
├─ First customer opportunities → Fast Start progress
└─ Week 2 completion celebration

Week 3: Generating Results
├─ Contact swiping becomes routine
├─ Recruiting pipeline developing
├─ Outcome-based tasks begin
├─ Customer opportunities converting  
└─ Fast Start program completion

Week 4: Achieving Success
├─ All contacts processed
├─ Multiple recruiting tiers achieved
├─ 28-day program completion  
├─ First customer won (89% retention trigger)
└─ Full system success celebration

Ongoing Success Mode
├─ New contact imports (periodic)
├─ Continued recruiting (ongoing tiers)
├─ Advanced rep responsibilities
├─ Customer base expansion
└─ Mentor role for new reps
```

---

## 📊 **Success Metrics & Flow Optimization**

### **Key Flow Success Indicators**

**Contact Swiping Flows**
- 95%+ contacts processed within 30 days
- <3 seconds per contact decision  
- 85%+ positive sentiment on swiping experience
- 90%+ prospect categorization accuracy

**Recruiting Game Flows**
- 90%+ users achieve at least Tier 1 submission
- 75%+ users achieve at least Tier 1 hire
- <24 hours from tier achievement to celebration
- 95%+ tier reward claim rate

**28-Day Program Flows**
- 90%+ foundation task completion (weeks 1-2)
- 75%+ outcome task completion (weeks 3-4)
- 85%+ overall program completion
- <1 hour weekly time investment

**Lead Tracker Flows**
- 75%+ get first customer within 14 days
- 80%+ Fast Start program participation
- 65%+ achieve at least Fast Start Tier 2
- 89% retention rate achievement

---

**🎯 These user flows ensure every interaction in RepX drives toward the ultimate goal: transforming new sales reps into successful recruiters while securing their first customer win within 14 days for 89% retention.**
