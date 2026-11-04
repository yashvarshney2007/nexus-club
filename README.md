# 🌟 Nexus: Club & Event Hub

> A responsive, modern web application for college students to discover campus clubs, register for events with instant scannable QR tickets, and build a verified digital participation identity called the **Nexus Campus Passport**.

![Nexus Banner](https://images.unsplash.com/photo-1523240795612-9a054b0db644?w=1200&auto=format&fit=crop&q=80)

---

## 🚀 Key Features

### 1. Public Landing Page (`/`)
- **Sticky Glassmorphism Navbar**: Logo with glowing gradient icon, navigation links (`Events`, `Clubs`, `How It Works`, `Check-in Demo`), dark/light mode toggle switch, and Google Sign-in action button.
- **Hero Showcase**: Compelling headline, youthful gradient styling, key campus stats, and primary call-to-actions (*Explore Events*, *Join a Club*).
- **Upcoming Events & Search Filter**:
  - Filter chips: `All`, `Tech`, `Cultural`, `Sports`, `Workshop`, `Social`.
  - Real-time search query matching titles, venues, organizer clubs, and tag keywords.
  - Interactive cards featuring posters, seats-left urgency badges, bookmark toggles, and direct links to full details.
- **Campus Clubs Grid**: Showcase of 6 collegiate societies with member counts, meeting schedules, tags, and one-click *Join Club* toggles.
- **How Nexus Works**: 5-step roadmap explaining authentication, interest tailoring, QR passes, gate check-in, and digital badge achievements.
- **Responsive Footer**: Campus links, ethical participation verification guidelines, and developer credits.

### 2. Mock Google Sign-In & Authentication
- Google-style modal with real Google branding and OAuth styling.
- **3 Demo Accounts**:
  - `Alex Rivera` (Computer Science & AI, Year 3)
  - `Maya Chen` (Interaction Design & Media, Year 2)
  - `Rohan Patel` (Robotics & Automation, Year 4)
- Authentic loading delay spinner to simulate secure OAuth credential synchronization.
- Persistent session saved in browser `localStorage`.
- Full Sign-out capabilities with state cleanup.

### 3. Student Interest Onboarding (First Login Only)
- Triggered automatically on initial account creation.
- Interactive multi-select grid with 15+ passions: `Coding`, `AI/ML`, `Music`, `Dance`, `Robotics`, `Photography`, `Sports`, `Entrepreneurship`, `Art`, `Gaming`, `Web3`, `Design`, etc.
- Requires selecting at least 3 interests before proceeding to customize recommendations and passport profile.

### 4. Protected Student Dashboard (`/dashboard`)
- Guarded by `<ProtectedRoute>` (redirects unauthenticated users to `/` and triggers the sign-in modal).
- Personalized greeting with student avatar, department, academic year, and Passport ID.
- **Quick Stats Bar**: Registered events, verified attended events, badges unlocked, and total Nexus XP score.
- **Recommended For You**: Curated events dynamically matched against the student's selected interests.
- **My Registrations**: Active passes with quick access to scannable tickets.
- **Bookmarked Events**: Real-time list of saved events with empty states.
- **Clubs Tailored For You**: Club suggestions with one-click membership joining.

### 5. Event Details & Scannable QR Ticket Generation (`/events/:id`)
- Full-width hero banner, category badge, and organizer info.
- Rich agenda schedule timeline, venue logistics, and seat availability tracking.
- **Registration Flow**:
  - Automatically checks capacity and prevents duplicate ticket issuance.
  - Generates a unique Ticket ID (`NX-TKT-XXXXXX`).
  - Encodes verifiable metadata into a high-contrast QR code (`ticketId`, `eventId`, `eventTitle`, `userEmail`, `date`, `venue`) using `qrcode.react`.
- **My Tickets Page (`/tickets`)**:
  - High-fidelity boarding pass design with perforation line and coupon notches.
  - **"Download Ticket"**: Draws a crisp PNG graphic onto an HTML5 canvas and triggers an instant client-side download.
  - **"Simulate Attendance"**: One-click demo button directly on the ticket pass to simulate gate entrance.

### 6. Nexus Campus Passport (`/passport`)
- **Digital Holographic ID Card**:
  - Student avatar, name, customizable department and academic year (editable inline).
  - Unique Passport ID (`NX-2026-XXXX`).
  - Active passion tags.
  - Campus tier ranking (`Campus Newcomer`, `Active Explorer`, `Campus Leader`, `Campus Legend`) with dynamic XP progress bars.
  - One-click **"Copy Passport Link"** button for sharing credentials with peers or recruiters.
- **Participation Timeline**: Chronological ledger of every attended campus workshop, hackathon, and game with dates, organizing clubs, and points earned.
- **Digital Badge Collection**:
  - Automatically awarded upon meeting attendance or engagement thresholds.
  - **Badges Included**:
    1. 👣 *First Step* (Attended 1 event)
    2. 🧭 *Campus Explorer* (Attended events across 3 distinct categories)
    3. 🛡️ *Club Champion* (Joined 2+ campus clubs)
    4. 🔥 *Nexus Regular* (Attended 5 events)
    5. 🏆 *Top Contributor* (Attended 10 events)
    6. ⚡ *Tech Pioneer* (Attended 2 Tech events)
    7. 🎵 *Culture Vulture* (Attended 2 Cultural events)
    8. ✨ *Early Bird* (Registered for 3 upcoming events)
  - Locked badges appear greyed out with animated progress bars showing exact milestones remaining.

### 7. Organizer Gate Check-in Portal (`/checkin`)
- Realistic event organizer scanner portal to simulate real gate management.
- Paste or scan any ticket ID to verify entrance.
- **Verification Logic**:
  - Validates ticket against stored registrations.
  - Detects if ticket was already checked in.
  - Marks status as `Attended`, awards `+100 Campus XP`.
  - Automatically calculates newly unlocked badges, triggers celebration confetti (`canvas-confetti`), and displays celebratory achievement toasts.
- **Testing Sandbox**: Includes quick 1-click buttons for all pending registered tickets so judges and evaluators can demo the full check-in flow in seconds!

---

## 🛠️ Tech Stack

| Technology | Purpose |
| :--- | :--- |
| **React 18** | Declarative Component-driven UI |
| **Vite 5** | Lightning-fast build tooling and HMR dev server |
| **Tailwind CSS 3** | Utility-first responsive design, custom glow effects & dark mode |
| **React Router 6** | Declarative client-side routing & protected route guards |
| **qrcode.react** | SVG-based QR code generation for ticket passes |
| **lucide-react** | Modern icon set |
| **canvas-confetti** | Interactive celebratory particle animations on badge unlock |
| **LocalStorage** | Persistence for user profiles, interests, tickets, and bookmarks |

---

## 📁 Project Structure

```
nexus-hub/
├── index.html
├── package.json
├── postcss.config.js
├── tailwind.config.js
├── vite.config.js
├── README.md
└── src/
    ├── main.jsx
    ├── App.jsx
    ├── index.css
    ├── context/
    │   ├── AuthContext.jsx       # Google mock OAuth, profile state, onboarding
    │   ├── EventsContext.jsx     # Events, tickets, bookmarks, clubs, check-in, badges
    │   └── ThemeContext.jsx      # Dark / Light theme toggle & localStorage sync
    ├── data/
    │   ├── events.json           # 12 diverse campus events with schedules & posters
    │   ├── clubs.json            # 6 collegiate societies with leads & meeting details
    │   ├── badges.json           # 8 tiered digital achievement badges with XP rewards
    │   └── mockUsers.json        # 3 realistic Google student profiles
    ├── components/
    │   ├── Navbar.jsx            # Sticky glass navbar with theme toggle & user dropdown
    │   ├── Footer.jsx            # Youthful campus footer with links & verified credentials info
    │   ├── ProtectedRoute.jsx    # Authentication route guard
    │   ├── EventCard.jsx         # Event poster, seats indicator, category pill, bookmark
    │   ├── ClubCard.jsx          # Club card with member count & 1-click join toggle
    │   ├── BadgeCard.jsx         # Achievement badge with locked/unlocked progress bar
    │   ├── TicketCard.jsx        # Boarding pass ticket with SVG QR code & canvas PNG download
    │   ├── GoogleSignInModal.jsx # Authentic Google account chooser modal with loading spinner
    │   ├── OnboardingModal.jsx   # Interest selection screen (pick 3+ passions)
    │   ├── PassportCard.jsx      # Futuristic holographic student ID card
    │   └── ToastNotification.jsx # Floating alerts for XP gains, bookmarks, and badges
    ├── pages/
    │   ├── LandingPage.jsx       # Public homepage with Hero, Events search, Clubs, How-it-Works
    │   ├── DashboardPage.jsx     # Protected student dashboard with interest recommendations
    │   ├── EventDetailsPage.jsx  # Event details, schedule timeline, and registration
    │   ├── MyTicketsPage.jsx     # All student tickets with filter tabs & QR passes
    │   ├── PassportPage.jsx      # Digital ID, participation timeline, and badge showcase
    │   ├── CheckInPage.jsx       # Gate check-in simulator with confetti & badge unlock
    │   └── NotFoundPage.jsx      # 404 page
    └── utils/
        ├── storage.js            # LocalStorage abstraction layer
        ├── formatters.js         # Badge classes, ticket ID generator, level calculator
        └── badgeCalculator.js    # Rule engine for progress tracking & badge unlock detection
```

---

## 💻 How to Run on Windows

### Prerequisites
- Node.js (v18 or higher recommended)
- npm

### Step-by-Step Instructions

1. **Open a terminal** (PowerShell or Command Prompt) and navigate to the project directory:
   ```powershell
   cd C:\Users\vansh\.gemini\antigravity\scratch\nexus-hub
   ```

2. **Install dependencies**:
   ```powershell
   npm install
   ```

3. **Start the development server**:
   ```powershell
   npm run dev
   ```

4. **Open your browser** and visit:
   ```
   http://localhost:5173
   ```

5. **Build for production**:
   ```powershell
   npm run build
   ```
   To preview the production build locally:
   ```powershell
   npm run preview
   ```

---

## 🎯 Quick Demo Walkthrough

1. **Explore the Landing Page**: Scroll through the Hero, try typing in the search bar or filtering by `Tech` or `Cultural`, and check out the Clubs section.
2. **Sign In with Google**: Click **Sign in with Google** in the navbar. Select `Alex Rivera` or `Maya Chen`.
3. **Onboarding**: Select at least 3 interests (e.g. *Coding*, *AI/ML*, *Music*) and click **Continue to Dashboard**.
4. **Register for an Event**: Browse your personalized recommendations on the dashboard, click an event, and hit **Register Now**. Your unique QR ticket is instantly created!
5. **View & Download Pass**: Head over to **Tickets** (`/tickets`). View your pass with its scannable QR code, and click **Download Ticket** to save it as a high-res PNG image.
6. **Simulate Gate Check-in**:
   - Option A: Click **Simulate Attendance** right on your ticket.
   - Option B: Navigate to **Check-in Demo** (`/checkin`), click one of the pending tickets in the sandbox, and hit **Verify & Check In**.
7. **Celebrate Badge Unlock**: Watch the confetti burst, celebrate the toast notification, and visit your **Nexus Campus Passport** (`/passport`) to see your attendance recorded on the timeline and newly unlocked badges!
