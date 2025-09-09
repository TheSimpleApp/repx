# Build Instructions - RepX MVP

## 🚀 **Complete Development Guide**

### **Project Overview**
RepX MVP is a mobile-first gamification platform for new sales rep onboarding built with FlutterFlow. This guide provides step-by-step instructions for frontend, backend, and stakeholder teams.

---

## 📋 **Pre-Development Setup**

### **Team Structure & Responsibilities**

#### **Frontend Team (FlutterFlow)**
- **Lead Developer**: FlutterFlow expert, mobile UI/UX
- **UI/UX Designer**: Screen design, user experience optimization
- **Mobile Developer**: Platform-specific optimizations, testing

#### **Backend Team**
- **Backend Lead**: Database design, API development
- **DevOps Engineer**: Infrastructure, deployment, monitoring
- **Integration Specialist**: Third-party APIs, payment processing

#### **Product Team**
- **Product Manager**: Feature prioritization, stakeholder communication
- **QA Engineer**: Testing, quality assurance, user acceptance testing
- **Data Analyst**: Analytics setup, performance monitoring

### **Development Environment Setup**

#### **Required Tools**
- **FlutterFlow Account**: Team plan with collaboration features
- **Firebase Project**: Production and staging environments
- **Stripe Account**: Payment processing for cash rewards
- **Version Control**: GitHub repository with branch protection
- **Communication**: Slack workspace for team coordination

#### **Development Accounts**
```bash
# Firebase Projects
- repx-mvp-dev (Development)
- repx-mvp-staging (Staging)
- repx-mvp-prod (Production)

# Stripe Accounts
- Development: test keys for local development
- Production: live keys for actual payments

# Third-Party Services
- Twilio: SMS notifications
- SendGrid: Email notifications
- Sentry: Error monitoring
```

---

## 🏗️ **Phase 1: Foundation Setup (Week 1)**

### **Day 1-2: Project Initialization**

#### **FlutterFlow Setup**
1. **Create New Project**: 
   - Project name: "RepX MVP"
   - Platform: iOS + Android
   - Theme: Custom (RepX design system)

2. **Configure Firebase**:
   - Connect to Firebase project
   - Enable Firestore database
   - Set up Firebase Authentication
   - Configure Firebase Storage

3. **Design System Setup**:
   - Import color palette (Primary: #2563eb, Secondary: #7c3aed)
   - Configure typography (Inter font family)
   - Set up component library

#### **Database Schema Creation**
```bash
# Firebase Firestore Setup
1. Create collections structure:
   - users
   - companies  
   - weeklyTasks
   - contactTiers
   - swipeActions
   - offlineActions

2. Set up security rules (see Database_Entities_Firebase.md)

3. Create indexes:
   - users: companyId, isActive
   - weeklyTasks: programId, weekNumber
   - contacts: userId, isProcessed, category

4. Import sample data for testing
```

### **Day 3-5: Core Architecture**

#### **Navigation Structure**
```dart
// FlutterFlow Page Structure
1. Authentication Pages:
   - LoginPage
   - SignupPage
   - ForgotPasswordPage

2. Main App Pages:
   - DashboardPage (Bottom nav index 0)
   - ContactsPage (Bottom nav index 1) 
   - TasksPage (Bottom nav index 2)
   - RewardsPage (Bottom nav index 3)
   - ProfilePage (Bottom nav index 4)

3. Modal Pages:
   - ContactSwipePage (Full screen modal)
   - TaskDetailsPage (Slide up modal)
   - RewardDetailsPage (Slide up modal)
   - WeeklyProgressPage (Full screen modal)
```

#### **State Management Setup**
```dart
// App State Variables (FlutterFlow)
- currentUser: DocumentReference
- currentWeek: int
- contactsProcessed: int
- totalContacts: int
- weeklyEarnings: double
- totalEarnings: double
- isOnboarding: bool
```

---

## 🎯 **Phase 2: Core Features (Week 2-3)**

### **Week 2: Contact Management System**

#### **Contact Import Implementation**
```dart
// FlutterFlow Custom Action: importContacts
Future<bool> importContacts() async {
  try {
    // Request contacts permission
    final permission = await Permission.contacts.request();
    if (!permission.isGranted) return false;
    
    // Get contacts from device phone only (no social media)
    final contacts = await ContactsService.getContacts();
    
    // Filter to only contacts with phone numbers
    final phoneContacts = contacts.where((contact) => 
      contact.phones?.isNotEmpty == true).toList();
    
    // Batch import to Firestore
    final batch = FirebaseFirestore.instance.batch();
    final userContactsRef = FirebaseFirestore.instance
        .collection('users')
        .doc(FFAppState().currentUser.id)
        .collection('contacts');
    
    for (int i = 0; i < phoneContacts.length; i++) {
      final contact = phoneContacts[i];
      final docRef = userContactsRef.doc();
      
      batch.set(docRef, {
        'contactName': contact.displayName ?? 'Unknown',
        'phoneNumber': contact.phones?.isNotEmpty == true 
            ? contact.phones!.first.value 
            : null,
        'email': contact.emails?.isNotEmpty == true 
            ? contact.emails!.first.value 
            : null,
        'contactSource': 'phone_sync', // MVP only supports phone contacts
        'contactIndex': i,
        'isProcessed': false,
        'createdAt': FieldValue.serverTimestamp(),
      });
    }
    
    await batch.commit();
    
    // Show success message
    FFAppState().showSnackBar('${phoneContacts.length} phone contacts imported successfully!');
    return true;
  } catch (e) {
    print('Error importing phone contacts: $e');
    FFAppState().showSnackBar('Error importing contacts. Please try again.');
    return false;
  }
}
```

#### **Contact Swiping Interface**
```dart
// FlutterFlow Custom Widget: ContactSwipeCard
class ContactSwipeCard extends StatelessWidget {
  final DocumentReference contactRef;
  final VoidCallback onSwipeLeft;
  final Function(String category, int tier, bool isStarred) onSwipeRight;
  
  @override
  Widget build(BuildContext context) {
    return StreamBuilder<DocumentSnapshot>(
      stream: contactRef.snapshots(),
      builder: (context, snapshot) {
        if (!snapshot.hasData) return CircularProgressIndicator();
        
        final contact = snapshot.data!.data() as Map<String, dynamic>;
        
        return Dismissible(
          key: Key(contactRef.id),
          direction: DismissDirection.horizontal,
          onDismissed: (direction) {
            if (direction == DismissDirection.startToEnd) {
              // Right swipe - categorize
              _showCategorizationDialog(context);
            } else {
              // Left swipe - skip
              onSwipeLeft();
            }
          },
          child: Card(
            child: Padding(
              padding: EdgeInsets.all(20),
              child: Column(
                children: [
                  Text(contact['contactName'], 
                       style: Theme.of(context).textTheme.headlineSmall),
                  if (contact['phoneNumber'] != null)
                    Text(contact['phoneNumber']),
                  if (contact['email'] != null)
                    Text(contact['email']),
                  
                  SizedBox(height: 20),
                  
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                    children: [
                      ElevatedButton(
                        onPressed: onSwipeLeft,
                        child: Text('Skip'),
                        style: ElevatedButton.styleFrom(
                          backgroundColor: Colors.grey,
                        ),
                      ),
                      ElevatedButton(
                        onPressed: () => _showCategorizationDialog(context),
                        child: Text('Select'),
                        style: ElevatedButton.styleFrom(
                          backgroundColor: Theme.of(context).primaryColor,
                        ),
                      ),
                    ],
                  ),
                ],
              ),
            ),
          ),
        );
      },
    );
  }
  
  void _showCategorizationDialog(BuildContext context) {
    // Show dialog for category and tier selection
  }
}
```

### **Week 3: Task Management System**

#### **Weekly Tasks Display**
```dart
// FlutterFlow Custom Widget: WeeklyTasksList
class WeeklyTasksList extends StatelessWidget {
  final int weekNumber;
  
  @override
  Widget build(BuildContext context) {
    return StreamBuilder<QuerySnapshot>(
      stream: FirebaseFirestore.instance
          .collection('weeklyTasks')
          .where('programId', isEqualTo: FFAppState().currentUser.programId)
          .where('weekNumber', isEqualTo: weekNumber)
          .orderBy('sortOrder')
          .snapshots(),
      builder: (context, snapshot) {
        if (!snapshot.hasData) return CircularProgressIndicator();
        
        final tasks = snapshot.data!.docs;
        
        return ListView.builder(
          itemCount: tasks.length,
          itemBuilder: (context, index) {
            final task = tasks[index].data() as Map<String, dynamic>;
            
            return FutureBuilder<DocumentSnapshot>(
              future: FirebaseFirestore.instance
                  .collection('users')
                  .doc(FFAppState().currentUser.id)
                  .collection('taskCompletions')
                  .doc(tasks[index].id)
                  .get(),
              builder: (context, completionSnapshot) {
                final isCompleted = completionSnapshot.hasData && 
                    completionSnapshot.data!.exists &&
                    (completionSnapshot.data!.data() as Map<String, dynamic>)['completionStatus'] == 'completed';
                
                return TaskCard(
                  task: task,
                  isCompleted: isCompleted,
                  onTap: () => _showTaskDetails(context, tasks[index].id, task),
                );
              },
            );
          },
        );
      },
    );
  }
}
```

#### **Task Completion Flow**
```dart
// FlutterFlow Custom Action: completeTask
Future<bool> completeTask(String taskId, Map<String, dynamic> verificationData) async {
  try {
    final userId = FFAppState().currentUser.id;
    final batch = FirebaseFirestore.instance.batch();
    
    // Create task completion record
    final completionRef = FirebaseFirestore.instance
        .collection('users')
        .doc(userId)
        .collection('taskCompletions')
        .doc(taskId);
    
    batch.set(completionRef, {
      'taskId': taskId,
      'completionStatus': 'completed',
      'completionDate': FieldValue.serverTimestamp(),
      'verificationData': verificationData,
      'createdAt': FieldValue.serverTimestamp(),
    });
    
    // Create reward transaction
    final rewardRef = FirebaseFirestore.instance
        .collection('users')
        .doc(userId)
        .collection('rewardTransactions')
        .doc();
    
    batch.set(rewardRef, {
      'transactionType': 'task_completion',
      'referenceId': taskId,
      'amount': verificationData['rewardAmount'],
      'description': 'Completed: ${verificationData['taskName']}',
      'status': 'approved',
      'paymentMethod': 'stripe',
      'createdAt': FieldValue.serverTimestamp(),
    });
    
    await batch.commit();
    
    // Trigger celebration animation
    _showCelebrationAnimation(verificationData['rewardAmount']);
    
    return true;
  } catch (e) {
    print('Error completing task: $e');
    return false;
  }
}
```

---

## 📱 **Phase 3: Mobile Optimization (Week 4)**

### **Offline Functionality**
```dart
// FlutterFlow Custom Service: OfflineManager
class OfflineManager {
  static const String _offlineActionsKey = 'offline_actions';
  
  // Queue action when offline
  static Future<void> queueOfflineAction(Map<String, dynamic> action) async {
    final prefs = await SharedPreferences.getInstance();
    final actionsJson = prefs.getString(_offlineActionsKey) ?? '[]';
    final actions = List<Map<String, dynamic>>.from(jsonDecode(actionsJson));
    
    action['queuedAt'] = DateTime.now().toIso8601String();
    action['syncStatus'] = 'pending';
    actions.add(action);
    
    await prefs.setString(_offlineActionsKey, jsonEncode(actions));
  }
  
  // Sync when back online
  static Future<void> syncOfflineActions() async {
    final connectivity = await Connectivity().checkConnectivity();
    if (connectivity == ConnectivityResult.none) return;
    
    final prefs = await SharedPreferences.getInstance();
    final actionsJson = prefs.getString(_offlineActionsKey) ?? '[]';
    final actions = List<Map<String, dynamic>>.from(jsonDecode(actionsJson));
    
    for (final action in actions) {
      if (action['syncStatus'] == 'pending') {
        try {
          await _executeAction(action);
          action['syncStatus'] = 'synced';
        } catch (e) {
          action['syncStatus'] = 'failed';
          action['error'] = e.toString();
        }
      }
    }
    
    // Remove synced actions
    final pendingActions = actions.where((a) => a['syncStatus'] != 'synced').toList();
    await prefs.setString(_offlineActionsKey, jsonEncode(pendingActions));
  }
}
```

### **Push Notifications Setup**
```dart
// FlutterFlow Custom Action: setupPushNotifications
Future<void> setupPushNotifications() async {
  final messaging = FirebaseMessaging.instance;
  
  // Request permission
  await messaging.requestPermission(
    alert: true,
    badge: true,
    sound: true,
  );
  
  // Get FCM token
  final token = await messaging.getToken();
  
  // Save token to user document
  await FirebaseFirestore.instance
      .collection('users')
      .doc(FFAppState().currentUser.id)
      .update({'fcmToken': token});
  
  // Handle foreground messages
  FirebaseMessaging.onMessage.listen((RemoteMessage message) {
    _showInAppNotification(message);
  });
  
  // Handle background messages
  FirebaseMessaging.onMessageOpenedApp.listen((RemoteMessage message) {
    _handleNotificationTap(message);
  });
}
```

---

## 🔧 **Backend Implementation**

### **Firebase Cloud Functions**

#### **Reward Processing Function**
```typescript
// functions/src/rewardProcessing.ts
import { onDocumentCreated } from 'firebase-functions/v2/firestore';
import { getFirestore } from 'firebase-admin/firestore';
import Stripe from 'stripe';

const stripe = new Stripe(process.env.STRIPE_SECRET_KEY!, {
  apiVersion: '2023-10-16',
});

export const processRewardTransaction = onDocumentCreated(
  'users/{userId}/rewardTransactions/{transactionId}',
  async (event) => {
    const transaction = event.data?.data();
    if (!transaction || transaction.status !== 'approved') return;

    try {
      // Get user payment info
      const userDoc = await getFirestore()
        .collection('users')
        .doc(event.params.userId)
        .get();
      
      const user = userDoc.data();
      if (!user) throw new Error('User not found');

      // Process payment via Stripe
      const payout = await stripe.transfers.create({
        amount: Math.round(transaction.amount * 100), // Convert to cents
        currency: 'usd',
        destination: user.stripeAccountId,
        description: transaction.description,
      });

      // Update transaction status
      await event.data?.ref.update({
        status: 'paid',
        paymentReference: payout.id,
        processedAt: new Date(),
      });

      // Send success notification
      await sendRewardNotification(user.phone, transaction.amount);

    } catch (error) {
      console.error('Error processing reward:', error);
      
      // Update transaction with error
      await event.data?.ref.update({
        status: 'failed',
        error: error.message,
        processedAt: new Date(),
      });
    }
  }
);
```

#### **Analytics Processing Function**
```typescript
// functions/src/analyticsProcessing.ts
export const updateDailyAnalytics = onSchedule('0 2 * * *', async () => {
  const db = getFirestore();
  const yesterday = new Date();
  yesterday.setDate(yesterday.getDate() - 1);
  const dateString = yesterday.toISOString().split('T')[0];

  // Get all companies
  const companiesSnapshot = await db.collection('companies').get();
  
  for (const companyDoc of companiesSnapshot.docs) {
    const companyId = companyDoc.id;
    
    // Calculate daily metrics for company
    const analytics = await calculateDailyMetrics(companyId, dateString);
    
    // Save analytics
    await db.collection('companyAnalytics').doc(`${companyId}_${dateString}`).set({
      companyId,
      analyticsDate: dateString,
      ...analytics,
      createdAt: new Date(),
    });
  }
});

async function calculateDailyMetrics(companyId: string, date: string) {
  const db = getFirestore();
  
  // Get all users for company
  const usersSnapshot = await db.collection('users')
    .where('companyId', '==', companyId)
    .get();
  
  let newRepsStarted = 0;
  let contactsProcessed = 0;
  let tasksCompleted = 0;
  let rewardsPaid = 0;
  
  for (const userDoc of usersSnapshot.docs) {
    const user = userDoc.data();
    const userId = userDoc.id;
    
    // Check if started onboarding today
    if (user.onboardingStartDate?.toDate().toISOString().split('T')[0] === date) {
      newRepsStarted++;
    }
    
    // Get daily engagement data
    const engagementDoc = await db.collection('users')
      .doc(userId)
      .collection('dailyEngagement')
      .doc(date)
      .get();
    
    if (engagementDoc.exists) {
      const engagement = engagementDoc.data()!;
      contactsProcessed += engagement.contactsSwiped || 0;
      tasksCompleted += engagement.tasksCompleted || 0;
    }
    
    // Get rewards paid today
    const rewardsSnapshot = await db.collection('users')
      .doc(userId)
      .collection('rewardTransactions')
      .where('processedAt', '>=', new Date(date))
      .where('processedAt', '<', new Date(date + 'T23:59:59'))
      .where('status', '==', 'paid')
      .get();
    
    rewardsPaid += rewardsSnapshot.docs.reduce((sum, doc) => 
      sum + (doc.data().amount || 0), 0);
  }
  
  return {
    newRepsStarted,
    contactsProcessed,
    tasksCompleted,
    totalRewardsPaid: rewardsPaid,
  };
}
```

### **Week 3: Task & Reward Systems**

#### **Task Verification System**
```dart
// FlutterFlow Custom Action: verifyTaskWithGPS
Future<bool> verifyTaskWithGPS(String taskId, List<Map<String, dynamic>> locations) async {
  try {
    // Validate GPS data
    if (locations.length < 50) {
      FFAppState().showSnackBar('Need at least 50 locations for verification');
      return false;
    }
    
    // Check for unique addresses (simplified)
    final uniqueLocations = _filterUniqueLocations(locations);
    if (uniqueLocations.length < 45) {
      FFAppState().showSnackBar('Need more unique locations');
      return false;
    }
    
    // Calculate total distance
    final totalDistance = _calculateTotalDistance(locations);
    
    // Create verification data
    final verificationData = {
      'verificationType': 'gps_tracking',
      'addressesVisited': uniqueLocations.length,
      'gpsCoordinates': locations,
      'totalDistance': totalDistance,
      'timeSpent': _calculateTimeSpent(locations),
      'verifiedAt': FieldValue.serverTimestamp(),
    };
    
    // Complete task with verification
    return await completeTask(taskId, verificationData);
  } catch (e) {
    print('Error verifying GPS task: $e');
    return false;
  }
}
```

---

## 🎨 **UI/UX Implementation**

### **Design System Components**

#### **RepX Button Component**
```dart
// FlutterFlow Custom Widget: RepXButton
class RepXButton extends StatelessWidget {
  final String text;
  final VoidCallback? onPressed;
  final ButtonType type;
  final bool isLoading;
  
  @override
  Widget build(BuildContext context) {
    return Container(
      width: double.infinity,
      height: 48,
      child: ElevatedButton(
        onPressed: isLoading ? null : onPressed,
        style: ElevatedButton.styleFrom(
          backgroundColor: _getBackgroundColor(),
          foregroundColor: _getTextColor(),
          shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.circular(12),
          ),
          elevation: 0, // Flat design
        ),
        child: isLoading 
            ? CircularProgressIndicator(color: _getTextColor())
            : Text(text, style: TextStyle(fontSize: 16, fontWeight: FontWeight.w500)),
      ),
    );
  }
  
  Color _getBackgroundColor() {
    switch (type) {
      case ButtonType.primary:
        return Color(0xFF2563EB); // Primary blue
      case ButtonType.secondary:
        return Colors.transparent;
      case ButtonType.success:
        return Color(0xFF10B981); // Success green
      default:
        return Color(0xFF6B7280); // Gray
    }
  }
}

enum ButtonType { primary, secondary, success, disabled }
```

#### **Progress Indicator Component**
```dart
// FlutterFlow Custom Widget: RepXProgressIndicator
class RepXProgressIndicator extends StatelessWidget {
  final double progress; // 0.0 to 1.0
  final String label;
  final Color color;
  
  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Row(
          mainAxisAlignment: MainAxisAlignment.spaceBetween,
          children: [
            Text(label, style: TextStyle(fontSize: 14, fontWeight: FontWeight.w500)),
            Text('${(progress * 100).round()}%', 
                 style: TextStyle(fontSize: 14, color: color)),
          ],
        ),
        SizedBox(height: 8),
        Container(
          width: double.infinity,
          height: 8,
          decoration: BoxDecoration(
            backgroundColor: Color(0xFFF3F4F6), // Light gray background
            borderRadius: BorderRadius.circular(4),
          ),
          child: FractionallySizedBox(
            alignment: Alignment.centerLeft,
            widthFactor: progress,
            child: Container(
              decoration: BoxDecoration(
                color: color,
                borderRadius: BorderRadius.circular(4),
              ),
            ),
          ),
        ),
      ],
    );
  }
}
```

### **Animation & Celebration System**
```dart
// FlutterFlow Custom Widget: CelebrationOverlay
class CelebrationOverlay extends StatefulWidget {
  final double rewardAmount;
  final String achievementText;
  final VoidCallback onComplete;
  
  @override
  _CelebrationOverlayState createState() => _CelebrationOverlayState();
}

class _CelebrationOverlayState extends State<CelebrationOverlay> 
    with TickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _scaleAnimation;
  late Animation<double> _fadeAnimation;
  
  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(milliseconds: 2000),
      vsync: this,
    );
    
    _scaleAnimation = Tween<double>(begin: 0.0, end: 1.0).animate(
      CurvedAnimation(parent: _controller, curve: Curves.elasticOut),
    );
    
    _fadeAnimation = Tween<double>(begin: 0.0, end: 1.0).animate(
      CurvedAnimation(parent: _controller, curve: Curves.easeIn),
    );
    
    _controller.forward().then((_) {
      Future.delayed(Duration(seconds: 3), () {
        widget.onComplete();
      });
    });
  }
  
  @override
  Widget build(BuildContext context) {
    return Material(
      color: Colors.black54,
      child: Center(
        child: AnimatedBuilder(
          animation: _controller,
          builder: (context, child) {
            return Transform.scale(
              scale: _scaleAnimation.value,
              child: Opacity(
                opacity: _fadeAnimation.value,
                child: Container(
                  padding: EdgeInsets.all(32),
                  margin: EdgeInsets.all(32),
                  decoration: BoxDecoration(
                    color: Colors.white,
                    borderRadius: BorderRadius.circular(20),
                  ),
                  child: Column(
                    mainAxisSize: MainAxisSize.min,
                    children: [
                      Text('🎉', style: TextStyle(fontSize: 64)),
                      SizedBox(height: 16),
                      Text(
                        'Congratulations!',
                        style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
                      ),
                      SizedBox(height: 8),
                      Text(
                        widget.achievementText,
                        textAlign: TextAlign.center,
                        style: TextStyle(fontSize: 16),
                      ),
                      SizedBox(height: 16),
                      Container(
                        padding: EdgeInsets.symmetric(horizontal: 20, vertical: 12),
                        decoration: BoxDecoration(
                          color: Color(0xFF10B981),
                          borderRadius: BorderRadius.circular(12),
                        ),
                        child: Text(
                          '+\$${widget.rewardAmount.toStringAsFixed(2)} Earned!',
                          style: TextStyle(
                            color: Colors.white,
                            fontSize: 18,
                            fontWeight: FontWeight.bold,
                          ),
                        ),
                      ),
                    ],
                  ),
                ),
              ),
            );
          },
        ),
      ),
    );
  }
}
```

---

## 📊 **Testing Strategy**

### **Unit Testing**
```dart
// test/services/contact_service_test.dart
import 'package:flutter_test/flutter_test.dart';
import 'package:mockito/mockito.dart';

void main() {
  group('ContactService', () {
    late ContactService contactService;
    late MockFirestore mockFirestore;
    
    setUp(() {
      mockFirestore = MockFirestore();
      contactService = ContactService(firestore: mockFirestore);
    });
    
    test('should import contacts successfully', () async {
      // Arrange
      final contacts = [
        Contact(name: 'John Doe', phone: '+1234567890'),
        Contact(name: 'Jane Smith', phone: '+0987654321'),
      ];
      
      // Act
      final result = await contactService.importContacts(contacts);
      
      // Assert
      expect(result, isTrue);
      verify(mockFirestore.collection('users').doc(any).collection('contacts').add(any)).called(2);
    });
    
    test('should categorize contact correctly', () async {
      // Arrange
      const contactId = 'contact123';
      const category = 'customer';
      const tier = 2;
      
      // Act
      final result = await contactService.categorizeContact(contactId, category, tier);
      
      // Assert
      expect(result, isTrue);
      verify(mockFirestore.collection('users').doc(any).collection('contacts').doc(contactId).update({
        'category': category,
        'tierLevel': tier,
        'isProcessed': true,
        'swipeDate': any,
      })).called(1);
    });
  });
}
```

### **Integration Testing**
```dart
// integration_test/app_test.dart
import 'package:flutter/services.dart';
import 'package:flutter_test/flutter_test.dart';
import 'package:integration_test/integration_test.dart';
import 'package:repx_mvp/main.dart' as app;

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();
  
  group('RepX App Integration Tests', () {
    testWidgets('complete onboarding flow', (WidgetTester tester) async {
      app.main();
      await tester.pumpAndSettle();
      
      // Test login flow
      await tester.tap(find.byKey(Key('email_field')));
      await tester.enterText(find.byKey(Key('email_field')), 'test@example.com');
      
      await tester.tap(find.byKey(Key('password_field')));
      await tester.enterText(find.byKey(Key('password_field')), 'password123');
      
      await tester.tap(find.byKey(Key('login_button')));
      await tester.pumpAndSettle();
      
      // Verify dashboard loads
      expect(find.byKey(Key('dashboard_page')), findsOneWidget);
      
      // Test contact import
      await tester.tap(find.byKey(Key('import_contacts_button')));
      await tester.pumpAndSettle();
      
      // Verify contact swiping interface
      expect(find.byKey(Key('contact_swipe_page')), findsOneWidget);
      
      // Test contact swipe
      await tester.fling(find.byKey(Key('contact_card')), Offset(300, 0), 1000);
      await tester.pumpAndSettle();
      
      // Verify categorization dialog
      expect(find.byKey(Key('categorization_dialog')), findsOneWidget);
    });
  });
}
```

---

## 🚀 **Deployment Instructions**

### **FlutterFlow Deployment**

#### **iOS App Store Deployment**
```bash
# 1. Configure iOS settings in FlutterFlow
- Bundle ID: com.repx.mvp
- App Name: RepX
- Version: 1.0.0
- Build Number: 1

# 2. Configure certificates and provisioning profiles
- Development Certificate
- Distribution Certificate  
- App Store Provisioning Profile

# 3. Build and deploy
- Download iOS build from FlutterFlow
- Upload to App Store Connect via Transporter
- Submit for App Store Review
```

#### **Android Play Store Deployment**
```bash
# 1. Configure Android settings in FlutterFlow
- Package Name: com.repx.mvp
- App Name: RepX
- Version Code: 1
- Version Name: 1.0.0

# 2. Generate signed APK/AAB
- Upload keystore to FlutterFlow
- Configure signing settings
- Build release version

# 3. Deploy to Play Store
- Upload AAB to Play Console
- Complete store listing
- Submit for review
```

### **Firebase Production Setup**
```bash
# 1. Production Firebase Project
firebase projects:create repx-mvp-prod
firebase use repx-mvp-prod

# 2. Enable required services
firebase firestore:enable
firebase auth:enable
firebase storage:enable
firebase functions:enable

# 3. Deploy security rules
firebase deploy --only firestore:rules

# 4. Deploy cloud functions
cd functions
npm install
firebase deploy --only functions

# 5. Configure environment variables
firebase functions:config:set stripe.secret_key="sk_live_..."
firebase functions:config:set twilio.account_sid="AC..."
firebase functions:config:set sendgrid.api_key="SG..."
```

---

## 📋 **Launch Checklist**

### **Pre-Launch Requirements**
- [ ] All core features tested and working
- [ ] Database schema deployed and tested
- [ ] Payment processing configured and tested
- [ ] Push notifications working
- [ ] App store listings complete
- [ ] Privacy policy and terms of service published
- [ ] Customer onboarding documentation ready
- [ ] Support system established

### **Go-Live Sequence**
1. **Final Testing**: Complete end-to-end testing with real data
2. **Production Deploy**: Deploy all services to production environment
3. **Monitoring Setup**: Configure alerts and monitoring dashboards
4. **Soft Launch**: Limited release to beta customers
5. **Feedback Collection**: Gather initial user feedback and iterate
6. **Full Launch**: Public release with marketing campaign

### **Post-Launch Monitoring**
- **Performance Metrics**: App performance, API response times, error rates
- **Business Metrics**: User retention, task completion, reward distribution
- **User Feedback**: App store reviews, support tickets, user surveys
- **System Health**: Database performance, payment processing, notification delivery

---

**🎯 These build instructions provide a complete roadmap for developing, testing, and deploying the RepX MVP with clear responsibilities for frontend, backend, and product teams.**
