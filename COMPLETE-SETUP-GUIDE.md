# LearnCraft - Complete Setup Guide

## 📁 Project Structure

```
LearnCraft/
├── Backend/
│   ├── LearnCraft.API/
│   │   ├── Controllers/
│   │   │   ├── AuthController.cs
│   │   │   ├── VideosController.cs
│   │   │   ├── LabsController.cs
│   │   │   └── ProgressController.cs
│   │   ├── Hubs/
│   │   │   └── AIAssistantHub.cs
│   │   ├── Program.cs
│   │   ├── appsettings.json
│   │   └── LearnCraft.API.csproj
│   │
│   ├── LearnCraft.Core/
│   │   ├── Entities/
│   │   │   ├── User.cs
│   │   │   ├── Video.cs
│   │   │   ├── Lab.cs
│   │   │   └── [other entities]
│   │   ├── Interfaces/
│   │   │   ├── IAuthService.cs
│   │   │   ├── IVideoService.cs
│   │   │   ├── ILabService.cs
│   │   │   └── IAIAssistantService.cs
│   │   └── DTOs/
│   │       ├── LoginDto.cs
│   │       ├── RegisterDto.cs
│   │       └── [other DTOs]
│   │
│   └── LearnCraft.Infrastructure/
│       ├── Data/
│       │   └── LearnCraftDbContext.cs
│       └── Services/
│           ├── AuthService.cs
│           ├── VideoService.cs
│           ├── LabService.cs
│           └── AIAssistantService.cs
│
└── Frontend/
    ├── public/
    ├── src/
    │   ├── components/
    │   │   ├── layout/
    │   │   │   ├── MainLayout.tsx
    │   │   │   └── Navbar.tsx
    │   │   ├── common/
    │   │   │   └── PrivateRoute.tsx
    │   │   ├── lab/
    │   │   │   ├── CodeEditor.tsx
    │   │   │   ├── LabInstructions.tsx
    │   │   │   └── SubmissionResult.tsx
    │   │   └── ai/
    │   │       └── AIAssistant.tsx
    │   │
    │   ├── pages/
    │   │   ├── LoginPage.tsx
    │   │   ├── RegisterPage.tsx
    │   │   ├── Dashboard.tsx
    │   │   ├── VideoLibrary.tsx
    │   │   ├── VideoPlayer.tsx
    │   │   ├── LabList.tsx
    │   │   ├── LabWorkspace.tsx
    │   │   └── ProgressPage.tsx
    │   │
    │   ├── redux/
    │   │   ├── store.ts
    │   │   └── slices/
    │   │       ├── authSlice.ts
    │   │       ├── videoSlice.ts
    │   │       ├── labSlice.ts
    │   │       ├── aiAssistantSlice.ts
    │   │       └── progressSlice.ts
    │   │
    │   ├── services/
    │   │   └── api.ts
    │   │
    │   ├── App.tsx
    │   ├── index.tsx
    │   └── index.css
    │
    ├── package.json
    └── tsconfig.json
```

## 🚀 Backend Setup (.NET Core)

### Prerequisites
- .NET 8.0 SDK
- SQL Server or PostgreSQL
- Visual Studio 2022 / VS Code

### Step 1: Create Project Structure
```bash
# Create solution
dotnet new sln -n LearnCraft

# Create API project
dotnet new webapi -n LearnCraft.API
dotnet sln add LearnCraft.API

# Create Core library
dotnet new classlib -n LearnCraft.Core
dotnet sln add LearnCraft.Core

# Create Infrastructure library
dotnet new classlib -n LearnCraft.Infrastructure
dotnet sln add LearnCraft.Infrastructure

# Add project references
cd LearnCraft.API
dotnet add reference ../LearnCraft.Core
dotnet add reference ../LearnCraft.Infrastructure

cd ../LearnCraft.Infrastructure
dotnet add reference ../LearnCraft.Core
```

### Step 2: Install NuGet Packages
```bash
# In LearnCraft.API
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Tools
dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer
dotnet add package Microsoft.AspNetCore.SignalR

# In LearnCraft.Infrastructure
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package BCrypt.Net-Next
```

### Step 3: Configure Database
1. Update `appsettings.json` with your database connection string
2. Run migrations:
```bash
dotnet ef migrations add InitialCreate
dotnet ef database update
```

### Step 4: Run Backend
```bash
cd LearnCraft.API
dotnet run
```
Backend will run on: http://localhost:5000

## 🎨 Frontend Setup (React + Redux)

### Prerequisites
- Node.js 18+ and npm
- Code editor (VS Code recommended)

### Step 1: Create React App
```bash
npx create-react-app learncraft-frontend --template typescript
cd learncraft-frontend
```

### Step 2: Install Dependencies
```bash
npm install @reduxjs/toolkit react-redux
npm install react-router-dom
npm install axios
npm install @microsoft/signalr
npm install -D tailwindcss postcss autoprefixer
npm install -D @tailwindcss/line-clamp
```

### Step 3: Setup Tailwind CSS
```bash
npx tailwindcss init -p
```

Update `tailwind.config.js`:
```javascript
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [
    require('@tailwindcss/line-clamp'),
  ],
}
```

### Step 4: File Structure Setup
Copy the provided files into their respective locations:
- Redux slices → `src/redux/slices/`
- Services → `src/services/`
- Components → `src/components/`
- Pages → `src/pages/`

### Step 5: Run Frontend
```bash
npm start
```
Frontend will run on: http://localhost:3000

## 🗄️ Database Schema

### Tables Created by EF Core
- **Users** - User authentication and profiles
- **Videos** - Video library content
- **VideoCategories** - Video categorization
- **Labs** - Lab assessments and instructions
- **LabSubmissions** - User lab submissions
- **UserProgress** - Learning progress tracking
- **AIConversations** - AI assistant chat history

## 🔑 Key Features Implementation

### 1. Authentication (JWT)
- Register/Login endpoints
- Token-based authentication
- Password hashing with BCrypt

### 2. Video Library
- Browse videos by category
- Search functionality
- Video progress tracking
- View count tracking

### 3. Lab Assessments
- Interactive code editor
- Multiple difficulty levels
- Submission tracking
- Test case validation

### 4. AI Learning Assistant (SignalR)
- Real-time chat interface
- Contextual hints
- Concept explanations
- NO direct solutions (educational guidance only)

### 5. Progress Tracking
- Video completion tracking
- Lab submission history
- Learning analytics

## 🔐 Environment Variables

### Backend (.env or appsettings.json)
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "YOUR_CONNECTION_STRING"
  },
  "JwtSettings": {
    "SecretKey": "YOUR_SECRET_KEY_MIN_32_CHARS",
    "Issuer": "LearnCraft",
    "Audience": "LearnCraftUsers"
  }
}
```

### Frontend (.env)
```
REACT_APP_API_URL=http://localhost:5000/api
REACT_APP_HUB_URL=http://localhost:5000/hubs
```

## 📝 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - User login

### Videos
- `GET /api/videos` - Get all videos
- `GET /api/videos/{id}` - Get video by ID
- `GET /api/videos/categories` - Get categories
- `POST /api/videos/{id}/track-view` - Track video view

### Labs
- `GET /api/labs` - Get all labs
- `GET /api/labs/{id}` - Get lab by ID
- `POST /api/labs/{id}/submit` - Submit lab
- `GET /api/labs/{id}/submissions` - Get user submissions

### Progress
- `GET /api/progress` - Get user progress
- `POST /api/progress/update` - Update progress

### SignalR Hub
- `/hubs/ai-assistant` - AI Assistant WebSocket

## 🧪 Testing

### Backend Tests
```bash
cd LearnCraft.Tests
dotnet test
```

### Frontend Tests
```bash
npm test
```

## 📦 Deployment Considerations

### Backend
1. Configure production database
2. Update CORS settings
3. Set secure JWT secret
4. Enable HTTPS
5. Configure logging

### Frontend
1. Build production bundle: `npm run build`
2. Configure API URL for production
3. Set up static file hosting
4. Enable HTTPS

## 🔧 Troubleshooting

### Common Issues

1. **Database Connection Failed**
   - Verify connection string
   - Ensure SQL Server is running
   - Check firewall settings

2. **CORS Error**
   - Verify CORS policy in Program.cs
   - Check frontend URL in allowed origins

3. **SignalR Connection Failed**
   - Verify hub URL
   - Check JWT token is being sent
   - Ensure WebSocket is enabled

4. **Build Errors**
   - Clear node_modules and reinstall
   - Clear .NET build cache: `dotnet clean`

## 📚 Next Steps

1. Implement additional services (VideoService, LabService, etc.)
2. Add code editor component (Monaco Editor or CodeMirror)
3. Implement test case runner for labs
4. Add video streaming support
5. Enhance AI assistant with better NLP
6. Add analytics dashboard
7. Implement real-time collaboration features

## 🤝 Contributing
This is a learning platform - contributions welcome!

## 📄 License
MIT License
