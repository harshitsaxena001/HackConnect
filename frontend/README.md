# HackConnect Frontend 🚀

This is the frontend client for **HackConnect**, built as a Single Page Application (SPA) using **React** and **Vite**. It serves as the "LinkedIn for Builders," facilitating hackathon discovery, team formation, and professional portfolio building.

## 🛠 Tech Stack

*   **Framework**: React 18 + Vite
*   **Language**: TypeScript
*   **Styling**: Tailwind CSS
*   **UI Components**: Shadcn/UI (Radix Primitives)
*   **Icons**: Lucide React
*   **Routing**: React Router DOM
*   **Backend/Auth**: Appwrite (Client-side integration)
*   **State Management**: React Hooks + TanStack Query

## 📂 Project Structure

```
frontend/
├── src/
│   ├── components/
│   │   ├── features/       # Business-specific components (HackathonCard, TeamCard)
│   │   ├── layout/         # Global layout (Navbar, Footer, Sidebar)
│   │   └── ui/             # Reusable UI atoms (Buttons, Inputs, Cards)
│   ├── hooks/              # Custom hooks (useAuth, useTheme)
│   ├── lib/                # Configuration & Utilities (appwrite.ts, utils.ts)
│   ├── pages/              # Route views (Index, Explore, Dashboard)
│   ├── types/              # TypeScript interfaces (User, Hackathon)
│   └── utils/              # Helper functions (date formatting, validation)
├── .env                    # Environment variables (VITE_ prefixes)
└── package.json
```

## ⚡️ Setup & Installation

1.  **Install Dependencies**
    ```bash
    npm install
    ```

2.  **Environment Configuration**
    Ensure your .env file is set up with your Appwrite credentials:
    ```env
    VITE_APPWRITE_ENDPOINT=https://cloud.appwrite.io/v1
    VITE_APPWRITE_PROJECT_ID=your_project_id
    VITE_APPWRITE_DATABASE_ID=your_database_id
    VITE_COLLECTION_USERS=users
    VITE_COLLECTION_HACKATHONS=hackathons
    # ... other collections
    ```

3.  **Run Development Server**
    ```bash
    npm run dev
    ```

## 🔄 Features

### 1. Authentication
*   **Status**: Implemented in `src/hooks/useAuth.ts`.
*   **Features**: Signup, Login, Logout, and User Profile fetching from the `users` collection.

### 2. Hackathon Discovery
*   **Status**: Implemented in `src/pages/Index.tsx` and `src/pages/Explore.tsx`.
*   **Features**: Real-time fetching from Appwrite, filtering, and search.

### 3. User Dashboard
*   **Status**: Implemented in `src/pages/Dashboard.tsx`.
*   **Features**: Personalized stats, upcoming hackathons, and team activity.

### 4. Team Management
*   **Status**: Implemented in `src/pages/TeamsLobby.tsx`.
*   **Features**: Create teams, join requests, and member management.

## 📝 Data Models (Appwrite)

Ensure your Appwrite Database has the following collections matching `src/types/`:

*   **Users**: `username`, `email`, `avatar_url`, `bio`, `skills` (array), `xp`.
*   **Hackathons**: `title`, `description`, `start_date`, `prize_pool`, `tags` (array), `cover_image`.
*   **Teams**: `name`, `hackathon_id`, `members` (array of user_ids), `looking_for` (array).
