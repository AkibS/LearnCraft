# LearnCraft - Learning Platform with AI Assistant

## Project Structure

```
LearnCraft/
├── Backend/
│   ├── LearnCraft.API/
│   ├── LearnCraft.Core/
│   ├── LearnCraft.Infrastructure/
│   └── LearnCraft.Tests/
└── Frontend/
    ├── src/
    │   ├── components/
    │   ├── redux/
    │   ├── services/
    │   ├── pages/
    │   └── utils/
    └── public/
```

## Technology Stack

### Backend
- .NET Core 8.0
- Entity Framework Core
- SQL Server / PostgreSQL
- SignalR (for real-time AI assistant)
- JWT Authentication

### Frontend
- React 18
- Redux Toolkit
- React Router
- Axios
- Material-UI / Tailwind CSS

## Features
1. **Video Library** - Browse and watch educational videos
2. **Lab Assessments** - Interactive coding/practical labs
3. **AI Learning Assistant** - Guided learning without giving direct solutions
4. **Progress Tracking** - Monitor learning progress
5. **User Authentication** - Secure login and user management

## Setup Instructions

### Backend Setup
```bash
cd Backend/LearnCraft.API
dotnet restore
dotnet ef database update
dotnet run
```

### Frontend Setup
```bash
cd Frontend
npm install
npm start
```

## API Endpoints Overview
- `/api/auth` - Authentication
- `/api/videos` - Video library management
- `/api/labs` - Lab assessments
- `/api/ai-assistant` - AI learning assistant
- `/api/progress` - User progress tracking
