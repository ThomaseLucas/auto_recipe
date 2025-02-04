**System Design Diagram for Meal Planner**

### **1. Components**

#### **Frontend (React + Firebase Hosting)**
- User Interface for adding/removing recipes.
- Connects to Firebase Firestore for real-time data updates.
- Calls backend APIs for meal selection and calendar updates.

#### **Backend (Firebase Cloud Functions - Python Flask-like API)**
- Exposes API endpoints:
  - POST /add_recipe: Adds a recipe to Firestore.
  - DELETE /remove_recipe: Removes a recipe.
  - GET /pick_meals: Selects 5 random recipes.
  - POST /add_to_calendar: Sends meals to Google Calendar.
- Runs scheduled job every Sunday to pick meals and update calendar.
- Uses Firebase Authentication for user permissions.

#### **Database (Firebase Firestore)**
- Stores recipes with fields:
  - id (unique identifier)
  - title (recipe name)
  - url (link to recipe)
  - tags (optional categorization)
  - added_by (user ID for tracking)

#### **Google API Integration**
- Uses OAuth via Firebase Authentication.
- Google Calendar API adds selected meals to a shared calendar.
- Ensures user permissions for modifying calendar events.

### **2. Data Flow**
1. User adds/removes recipes via the frontend.
2. Firebase Firestore updates in real-time.
3. Scheduled job (Firebase Cloud Function) picks 5 meals weekly.
4. The function sends selected meals to Google Calendar using Google API.
5. User sees meal plan on Google Calendar.

### **3. Hosting & Deployment**
- **Frontend**: Firebase Hosting.
- **Backend**: Firebase Cloud Functions.
- **Database**: Firebase Firestore.

### **4. Authentication & Security**
- Firebase Authentication manages user logins.
- Only authorized users can modify recipes.
- Google OAuth ensures safe calendar integration.

### **5. Scalability Considerations**
- Firebase Cloud Functions auto-scale based on usage.
- Firestore supports real-time sync and offline access.
- Google Calendar API has rate limits (to be handled with retry logic).

---

This setup ensures a simple, scalable, and user-friendly meal planning system with minimal maintenance!
