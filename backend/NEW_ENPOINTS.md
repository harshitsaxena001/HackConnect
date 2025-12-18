## 1. Current State Assessment
- Solid foundation in place:  
  - User management  
  - Authentication  
  - CRUD operations for Hackathons and Teams  
- **Critical gaps identified:**  
  1. No mechanism for teams to submit final projects  
  2. Limited tools for event organizers (editing, analytics, judging)  
  3. Missing AI-powered matchmaking ("Moneyball" feature)

## 2. Proposed Enhancements Overview
Three new functional layers to be added:

1. **Submission Layer** – Enable teams to submit projects and judges to review them  
2. **Organizer Suite** – Provide full administrative control and insights  
3. **AI & Matchmaking Layer** – Deliver intelligent team recommendations and generative tools

## 3. Detailed API Proposals

### 3.1 Submissions Layer (/api/submissions)

| Endpoint                              | Method | Description                                      | Key Details |
|---------------------------------------|--------|--------------------------------------------------|-------------|
| `POST /api/submissions/`              | POST   | Team leader submits final project                 | Requires `hackathon_id`, `team_id`, `project_title`, `description`, `repo_links[]`, `demo_video_url` |
| `GET /api/submissions/{hackathon_id}` | GET    | Retrieve all submissions for a hackathon (for judges/organizers) | Returns list of submissions |

### 3.2 Organizer Suite (/api/organizer & related)

| Endpoint                                          | Method | Description                                          | Security / Notes |
|---------------------------------------------------|--------|------------------------------------------------------|------------------|
| `PUT /api/hackathons/{hackathon_id}`               | PUT    | Update hackathon details (description, prizes, deadlines) | Restricted to organizer (`request.user.id == hackathon.organizer_id`) |
| `PATCH /api/hackathons/{hackathon_id}/status`      | PATCH  | Change event status (draft → published → live → archived) | Controls public visibility |
| `GET /api/organizer/{hackathon_id}/stats`          | GET    | Dashboard analytics                                  | Returns: `total_registrants`, `teams_formed`, `looking_for_team`, `submissions_received` |
| `POST /api/organizer/{hackathon_id}/announce`      | POST   | Broadcast announcement to participants               | Triggers realtime notifications or emails |
| `POST /api/judging/score`                         | POST   | Submit judging scores for a submission               | Fields: `submission_id`, `judge_id`, scores (technical/design/utility), `comment` |

### 3.3 AI & Matchmaking Layer (/api/ai)

| Endpoint                                      | Method | Description                                          | Key Details |
|-----------------------------------------------|--------|------------------------------------------------------|-------------|
| `GET /api/ai/teams/match/{hackathon_id}`       | GET    | "Moneyball" team recommendations                     | Returns ranked teams with `match_score` and `reason` based on user skills |
| `POST /api/ai/generate-description`           | POST   | Auto-generate hackathon description using Gemini API  | Input: `topic`, `prizes`, etc. |

## 4. Summary of Required Changes

| Priority | Change Description                                      | Impact |
|----------|---------------------------------------------------------|--------|
| High     | Add `PUT /api/hackathons/{id}`                           | Enables organizers to correct/update events |
| High     | Add `POST /api/submissions`                              | Completes hackathon lifecycle (teams can now "win") |
| High     | Add `PATCH /api/hackathons/{id}/status`                  | Controls event visibility (draft vs. public) |
| Medium   | Add `GET /api/organizer/{id}/stats`                      | Provides actionable insights for organizers |
| Medium   | Refine `POST /register` logic                           | Ensure correct role assignment (Hacker vs. Organizer) in Appwrite DB |
