# 📐 RepX MVP Design Guidelines
**Mobile-First Design System for New Sales Rep Success**

---

## 🎯 Core Principles

* **Field Sales Optimized**: Design for new sales reps using phones in various environments
* **Swipe-First Interaction**: Tinder-like contact swiping as primary interface pattern
* **Gamification-Focused**: Visual celebration of achievements, progress, and rewards
* **Single-Handed Usage**: All primary actions within thumb reach for one-handed operation
* **Immediate Gratification**: Instant visual feedback for every action and achievement
* **89% Success Mindset**: Design reinforces confidence and success trajectory

---

# 🎨 RepX Design System

## Typography Scale (Mobile-Optimized)
* **Base**: 16px root font size for mobile readability
* **Contact Names**: text-2xl (24px) font-semibold - prominent in swipe interface
* **Tier Rewards**: text-xl (20px) font-bold - emphasize reward values
* **Cash Amounts**: text-lg (18px) font-semibold - highlight earnings prominently  
* **Progress Labels**: text-base (16px) font-medium - clear status information
* **Helper Text**: text-sm (14px) font-normal - secondary information
* **Button Text**: text-base (16px) font-medium - clear call-to-action text
* **Line Height**: 1.4x for contact names, 1.5x for body text

## RepX Color System (Gamified)
```css
/* Success & Achievement Colors */
--repx-success: hsl(142, 76%, 36%)     /* Green - completed tasks, wins */
--repx-tier-gold: hsl(45, 93%, 58%)    /* Gold - tier achievements, stars */
--repx-cash-green: hsl(134, 61%, 41%)  /* Money green - cash rewards */

/* Action Colors */  
--repx-swipe-right: hsl(142, 76%, 36%) /* Green - yes/recruit/customer */
--repx-swipe-left: hsl(0, 72%, 51%)    /* Red - pass/no */
--repx-super-swipe: hsl(45, 93%, 58%)  /* Gold - star/super swipe */

/* Progress & System Colors */
--repx-primary: hsl(224, 76%, 48%)     /* Blue - primary actions */
--repx-progress: hsl(204, 86%, 53%)    /* Light blue - progress bars */
--repx-background: hsl(0, 0%, 100%)    /* White - clean background */
--repx-surface: hsl(210, 20%, 98%)     /* Very light gray - cards */
--repx-border: hsl(210, 14%, 89%)      /* Light gray - borders */

/* Status Colors */
--repx-pending: hsl(43, 89%, 58%)      /* Amber - pending/in-progress */
--repx-error: hsl(0, 72%, 51%)         /* Red - errors/failed */
--repx-muted: hsl(210, 14%, 83%)       /* Gray - disabled/inactive */
```

## Spacing & Layout (Thumb-Friendly)
* **Base Unit**: 8px grid system
* **Swipe Card Padding**: p-6 (24px) for contact information
* **Touch Targets**: Minimum 56px (h-14) for swipe actions and buttons  
* **Content Gaps**: gap-4 (16px) between related elements
* **Section Spacing**: gap-6 (24px) between major sections
* **Screen Padding**: px-4 (16px) minimum, px-6 (24px) preferred
* **Bottom Tab Height**: h-20 (80px) for easy thumb access

---

# 🧩 RepX Component Patterns

## Contact Swiping Interface
```jsx
/* Contact Swipe Card */
<Card className="mx-4 my-6 h-96 relative bg-white shadow-lg">
  <CardContent className="p-6 flex flex-col justify-center h-full">
    <h2 className="text-2xl font-semibold text-center mb-2">{contactName}</h2>
    <p className="text-base text-center text-muted-foreground">{phoneNumber}</p>
  </CardContent>
  
  {/* Swipe Action Buttons */}
  <div className="absolute bottom-4 flex justify-center w-full gap-6">
    <Button variant="destructive" size="icon" className="h-14 w-14 rounded-full">
      <X className="h-6 w-6" />
    </Button>
    <Button variant="default" className="h-16 w-16 rounded-full bg-repx-tier-gold">
      <Star className="h-7 w-7" />
    </Button>
    <Button variant="default" size="icon" className="h-14 w-14 rounded-full bg-repx-success">
      <Check className="h-6 w-6" />
    </Button>
  </div>
</Card>
```

## Recruiting Tier Cards
```jsx
/* Tier Progress Card */
<Card className="bg-gradient-to-r from-repx-surface to-white border-l-4 border-repx-tier-gold">
  <CardHeader className="pb-2">
    <div className="flex justify-between items-center">
      <h3 className="text-lg font-semibold">Tier 2 - $50 Gift Card</h3>
      <Badge variant="secondary" className="bg-repx-success text-white">
        {isCompleted ? "ACHIEVED!" : `${current}/${required}`}
      </Badge>
    </div>
  </CardHeader>
  <CardContent>
    <Progress value={progressPercent} className="h-3 bg-repx-muted">
      <div className="bg-repx-tier-gold h-full transition-all" />
    </Progress>
    <p className="text-sm text-muted-foreground mt-2">
      {remaining} more recruits to unlock reward
    </p>
  </CardContent>
</Card>
```

## 28-Day Program Tasks
```jsx
/* Task Completion Item */
<Card className="border-l-4 border-repx-progress hover:shadow-md transition-shadow">
  <CardContent className="p-4">
    <div className="flex items-center gap-4">
      <Checkbox 
        id={taskId}
        checked={isCompleted}
        className="h-6 w-6"
      />
      <div className="flex-1">
        <label htmlFor={taskId} className="text-base font-medium cursor-pointer">
          {taskTitle}
        </label>
        <p className="text-sm text-muted-foreground">{taskDescription}</p>
      </div>
      <div className="text-right">
        <span className="text-lg font-semibold text-repx-cash-green">
          +${cashReward}
        </span>
      </div>
    </div>
  </CardContent>
</Card>
```

## Achievement Celebrations
```jsx
/* Full-Screen Achievement Modal */
<Dialog open={showAchievement}>
  <DialogContent className="max-w-sm mx-auto bg-gradient-to-b from-repx-tier-gold/20 to-white">
    <div className="text-center py-8">
      <motion.div
        initial={{ scale: 0 }}
        animate={{ scale: 1 }}
        transition={{ type: "spring", duration: 0.6 }}
      >
        <Trophy className="h-20 w-20 mx-auto text-repx-tier-gold mb-4" />
      </motion.div>
      
      <h2 className="text-2xl font-bold text-repx-tier-gold mb-2">
        🎉 TIER 2 ACHIEVED! 🎉
      </h2>
      
      <p className="text-xl font-semibold mb-4">
        $50 Gift Card Unlocked!
      </p>
      
      <p className="text-base text-muted-foreground mb-6">
        You're building an amazing team!
      </p>
      
      <Button className="w-full h-12 bg-repx-tier-gold hover:bg-repx-tier-gold/90">
        Claim Your Reward
      </Button>
    </div>
  </DialogContent>
</Dialog>
```

## Progress Tracking Components
```jsx
/* Daily Progress Overview */
<Card className="bg-gradient-to-r from-repx-primary/5 to-repx-success/5">
  <CardHeader>
    <h2 className="text-xl font-semibold">Day 12 of 28</h2>
    <Progress value={42.8} className="h-4" />
  </CardHeader>
  <CardContent>
    <div className="grid grid-cols-2 gap-4">
      <div className="text-center">
        <p className="text-2xl font-bold text-repx-success">{contactsProcessed}</p>
        <p className="text-sm text-muted-foreground">Contacts Swiped</p>
      </div>
      <div className="text-center">
        <p className="text-2xl font-bold text-repx-cash-green">${cashEarned}</p>
        <p className="text-sm text-muted-foreground">Cash Earned</p>
      </div>
    </div>
  </CardContent>
</Card>
```

---

# 🎭 RepX Interaction Patterns

## Swipe Gestures & Animations
```jsx
/* Contact Swipe with Motion */
const SwipeCard = ({ contact, onSwipe }) => {
  const [dragX, setDragX] = useState(0);
  
  return (
    <motion.div
      drag="x"
      dragConstraints={{ left: -200, right: 200 }}
      onDrag={(_, info) => setDragX(info.offset.x)}
      onDragEnd={(_, info) => {
        if (Math.abs(info.offset.x) > 100) {
          onSwipe(info.offset.x > 0 ? 'right' : 'left');
        }
      }}
      whileDrag={{ rotate: dragX * 0.1 }}
      className="cursor-grab active:cursor-grabbing"
    >
      {/* Swipe Indicators */}
      <div className={`absolute inset-0 flex items-center justify-start pl-8 
        ${dragX > 50 ? 'opacity-100' : 'opacity-0'} transition-opacity`}>
        <div className="bg-repx-success text-white p-3 rounded-full">
          <Check className="h-8 w-8" />
        </div>
      </div>
      
      <div className={`absolute inset-0 flex items-center justify-end pr-8
        ${dragX < -50 ? 'opacity-100' : 'opacity-0'} transition-opacity`}>
        <div className="bg-repx-swipe-left text-white p-3 rounded-full">
          <X className="h-8 w-8" />
        </div>
      </div>
      
      {/* Contact Card Content */}
      <ContactCard contact={contact} />
    </motion.div>
  );
};
```

## Task Completion Animations
```jsx
/* Task Check Animation */
const TaskItem = ({ task, onComplete }) => {
  const [isCompleting, setIsCompleting] = useState(false);
  
  const handleComplete = async () => {
    setIsCompleting(true);
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 800));
    onComplete(task.id);
    
    // Celebration animation
    confetti({
      particleCount: 50,
      spread: 60,
      origin: { y: 0.8 }
    });
  };
  
  return (
    <motion.div
      animate={isCompleting ? { scale: [1, 1.02, 1] } : {}}
      transition={{ duration: 0.3 }}
    >
      <TaskCard 
        task={task}
        onComplete={handleComplete}
        showCashAnimation={isCompleting}
      />
    </motion.div>
  );
};
```

## Tier Achievement Flow
```jsx
/* Progressive Tier Unlock */
const TierProgress = ({ currentCount, tierRequirements }) => {
  const [showCelebration, setShowCelebration] = useState(false);
  
  useEffect(() => {
    // Check for tier achievement
    const achievedTier = tierRequirements.find(tier => 
      currentCount >= tier.requirement && !tier.achieved
    );
    
    if (achievedTier) {
      setShowCelebration(true);
      // Mark tier as achieved
      markTierAchieved(achievedTier.id);
    }
  }, [currentCount]);
  
  return (
    <>
      {tierRequirements.map((tier, index) => (
        <TierCard 
          key={tier.id}
          tier={tier}
          progress={Math.min(currentCount / tier.requirement * 100, 100)}
          isNext={index === 0 && !tier.achieved}
        />
      ))}
      
      <AchievementCelebration 
        show={showCelebration}
        onClose={() => setShowCelebration(false)}
      />
    </>
  );
};
```

---

# 📱 RepX Mobile Patterns

## One-Handed Navigation
```jsx
/* Bottom-Heavy UI Layout */
<div className="min-h-screen flex flex-col">
  {/* Header - Minimal */}
  <header className="p-4 bg-white border-b">
    <h1 className="text-lg font-semibold text-center">RepX</h1>
  </header>
  
  {/* Main Content - Scrollable */}
  <main className="flex-1 overflow-auto pb-24">
    {children}
  </main>
  
  {/* Bottom Actions - Thumb Zone */}
  <div className="fixed bottom-0 left-0 right-0 bg-white border-t">
    {/* Floating Action Button */}
    <Button className="absolute -top-8 right-6 h-16 w-16 rounded-full shadow-lg">
      <Plus className="h-8 w-8" />
    </Button>
    
    {/* Tab Navigation */}
    <nav className="h-20 flex items-center justify-around">
      {tabs.map(tab => (
        <TabButton key={tab.id} {...tab} />
      ))}
    </nav>
  </div>
</div>
```

## Touch-Optimized Interactions
```jsx
/* Large Touch Targets */
const SwipeActionButtons = ({ onSwipe }) => (
  <div className="flex justify-center gap-8 mt-6">
    <Button
      variant="outline"
      size="lg"
      className="h-16 w-16 rounded-full border-2 border-repx-swipe-left 
                 hover:bg-repx-swipe-left hover:text-white
                 active:scale-95 transition-all duration-150"
      onClick={() => onSwipe('left')}
    >
      <X className="h-8 w-8" />
    </Button>
    
    <Button
      size="lg"
      className="h-20 w-20 rounded-full bg-repx-tier-gold 
                 hover:bg-repx-tier-gold/90
                 active:scale-95 transition-all duration-150
                 shadow-lg"
      onClick={() => onSwipe('super')}
    >
      <Star className="h-10 w-10" />
    </Button>
    
    <Button
      variant="outline"
      size="lg"
      className="h-16 w-16 rounded-full border-2 border-repx-success
                 hover:bg-repx-success hover:text-white
                 active:scale-95 transition-all duration-150"
      onClick={() => onSwipe('right')}
    >
      <Check className="h-8 w-8" />
    </Button>
  </div>
);
```

## Loading & Empty States
```jsx
/* Contact Loading Skeleton */
const ContactLoadingSkeleton = () => (
  <Card className="mx-4 my-6 h-96">
    <CardContent className="p-6 flex flex-col justify-center h-full">
      <Skeleton className="h-8 w-48 mx-auto mb-4" />
      <Skeleton className="h-4 w-32 mx-auto mb-8" />
      <div className="flex justify-center gap-6">
        <Skeleton className="h-14 w-14 rounded-full" />
        <Skeleton className="h-16 w-16 rounded-full" />
        <Skeleton className="h-14 w-14 rounded-full" />
      </div>
    </CardContent>
  </Card>
);

/* Empty Contacts State */
const EmptyContactsState = ({ onImport }) => (
  <div className="flex flex-col items-center justify-center h-96 px-8 text-center">
    <ContactIcon className="h-24 w-24 text-repx-muted mb-6" />
    <h2 className="text-xl font-semibold mb-2">No Contacts Yet</h2>
    <p className="text-muted-foreground mb-6">
      Import your phone contacts to start building your network!
    </p>
    <Button onClick={onImport} className="h-12 px-8">
      Import Contacts
    </Button>
  </div>
);
```

---

# 🎨 RepX Specific UI Patterns

## Cash Reward Displays
```jsx
/* Prominent Cash Display */
const CashRewardDisplay = ({ amount, label, size = "default" }) => {
  const sizeClasses = {
    small: "text-lg",
    default: "text-2xl", 
    large: "text-4xl"
  };
  
  return (
    <div className="text-center">
      <div className={`font-bold text-repx-cash-green ${sizeClasses[size]}`}>
        ${amount.toFixed(2)}
      </div>
      {label && (
        <div className="text-sm text-muted-foreground mt-1">
          {label}
        </div>
      )}
    </div>
  );
};
```

## Progress Visualization
```jsx
/* Multi-System Progress Overview */
const SystemProgress = ({ systems }) => (
  <div className="grid grid-cols-2 gap-4">
    {systems.map(system => (
      <Card key={system.id} className="p-4">
        <div className="flex items-center gap-3 mb-2">
          <system.icon className="h-5 w-5 text-repx-primary" />
          <span className="font-medium text-sm">{system.name}</span>
        </div>
        <Progress 
          value={system.progress} 
          className="h-2 mb-1"
        />
        <div className="text-xs text-muted-foreground">
          {system.current} / {system.total}
        </div>
      </Card>
    ))}
  </div>
);
```

## Status Badges & Indicators
```jsx
/* RepX Status Badge System */
const StatusBadge = ({ status, count }) => {
  const statusConfig = {
    submitted: { color: "bg-repx-pending", icon: Clock, label: "Submitted" },
    contacted: { color: "bg-repx-primary", icon: Phone, label: "Contacted" },
    hired: { color: "bg-repx-success", icon: CheckCircle, label: "Hired" },
    customer: { color: "bg-repx-cash-green", icon: DollarSign, label: "Customer" }
  };
  
  const config = statusConfig[status];
  
  return (
    <Badge className={`${config.color} text-white flex items-center gap-1`}>
      <config.icon className="h-3 w-3" />
      {config.label}
      {count && <span className="ml-1">({count})</span>}
    </Badge>
  );
};
```

---

# ✅ RepX Implementation Checklist

**Contact Swiping Interface:**
- [ ] 56px minimum touch targets for swipe buttons
- [ ] Smooth drag animations with visual feedback
- [ ] Clear swipe direction indicators
- [ ] Prospect type selection modal
- [ ] Progress tracking with contact count

**Recruiting Gamification:**
- [ ] Tier cards with prominent reward displays  
- [ ] Progress bars with gold accent color
- [ ] Achievement celebration modals
- [ ] Badge system for tier completions
- [ ] Cash/reward value emphasis

**28-Day Program:**
- [ ] Checkbox interactions with completion animations
- [ ] Cash reward displays with green accent
- [ ] Weekly milestone celebrations
- [ ] Progress visualization across 4 weeks
- [ ] Task verification UI patterns

**Lead Tracking:**
- [ ] Customer prospect cards with status
- [ ] Opportunity creation workflows
- [ ] First customer win celebration
- [ ] Fast Start leaderboard display
- [ ] Success rate reinforcement UI

**Mobile Optimization:**
- [ ] Bottom navigation with 80px height
- [ ] Thumb-friendly button placement
- [ ] One-handed usage optimization
- [ ] Loading skeletons for all states
- [ ] Offline-ready UI feedback

**Gamification Elements:**
- [ ] Confetti animations for achievements
- [ ] Progress celebration micro-interactions
- [ ] Success rate messaging integration
- [ ] Tier progression visual feedback
- [ ] 89% retention rate reinforcement

---

**🎯 These design guidelines ensure RepX delivers a mobile-first, gamified experience that drives new sales reps toward the ultimate goal: 89% retention through systematic contact mining and structured success programs.**
