# ProjectFlow - Development Documentation (Complete)

### Personal Project Management Tool
- Version: 2.0.0 (Modern UI Design)
- Target: Local Hosting with Modern SaaS-Style Interface
- Architecture: Optimized File Organization & Contemporary Design

## Table of Contents
1. Project Overview
2. Project Structure
3. Technical Architecture
4. UI/UX Design Guidelines
5. Dashboard Specifications
6. Database Schema
7. Backend Implementation
8. Frontend Implementation
9. API Specification
10. Component Architecture
11. Deployment Guide
12. Performance Considerations
13. Security Guidelines


## Project Overview
### Project Description
ProjectFlow is a personal project management tool designed for local hosting. It provides comprehensive project tracking, task management, Kanban boards, analytics, and reporting capabilities with a focus on individual productivity and modern user experience.

#### Core Features
- Dashboard: Modern overview with statistics, charts, and recent activity
- Project Management: Project creation, tracking, and progress monitoring
- Task Management: Task creation, assignment, prioritization with modern UI
- Kanban Board: Visual task management with drag-and-drop functionality
- Time Tracking: Duration logging with visual time analytics
- Analytics: Interactive charts and productivity insights
- Calendar: Visual deadline tracking and event management
- Reports: Custom report generation and export
- Settings: User preferences and configuration

### Design Philosophy
- Modern: Contemporary SaaS-style interface with cards and clean layouts
- Productive: Muted, professional color palette that reduces eye strain
- Local-First: Designed for local hosting with offline capabilities
- Maintainable: Small, focused files for easy development and maintenance
- Interactive: Engaging user experience with smooth animations and feedback

## Project Structure
### Complete Directory Structure
<pre>projectflow/
├── backend/
│   ├── package.json
│   ├── server.js
│   ├── .env.example
│   ├── .gitignore
│   ├── README.md
│   ├── src/
│   │   ├── config/
│   │   │   ├── database.js
│   │   │   └── app.js
│   │   ├── controllers/
│   │   │   ├── authController.js
│   │   │   ├── projectController.js
│   │   │   ├── taskController.js
│   │   │   ├── analyticsController.js
│   │   │   ├── reportController.js
│   │   │   ├── timeLogController.js
│   │   │   ├── taskCommentController.js
│   │   │   └── milestoneController.js
│   │   ├── models/
│   │   │   ├── BaseModel.js
│   │   │   ├── User.js
│   │   │   ├── Session.js
│   │   │   ├── Project.js
│   │   │   ├── Task.js
│   │   │   ├── TimeLog.js
│   │   │   ├── TaskComment.js
│   │   │   ├── Milestone.js
│   │   │   └── Report.js
│   │   ├── routes/
│   │   │   ├── auth.js
│   │   │   ├── projects.js
│   │   │   ├── tasks.js
│   │   │   ├── analytics.js
│   │   │   ├── reports.js
│   │   │   ├── timetracking.js
│   │   │   ├── comments.js
│   │   │   └── milestones.js
│   │   ├── middleware/
│   │   │   ├── auth.js
│   │   │   ├── validation.js
│   │   │   ├── errorHandler.js
│   │   │   └── rateLimiter.js
│   │   ├── utils/
│   │   │   ├── logger.js
│   │   │   ├── validation.js
│   │   │   ├── helpers.js
│   │   │   ├── sessionSecurity.js
│   │   │   └── SessionCleanup.js
│   │   ├── migrations/
│   │   │   ├── 001_initial_schema.sql
│   │   │   ├── 002_add_sessions.sql
│   │   │   ├── 003_add_time_logs.sql
│   │   │   └── 004_add_milestones.sql
│   │   └── scripts/
│   │       ├── migrate.js
│   │       └── seed.js
│   ├── data/
│   │   ├── .gitkeep
│   │   └── backups/
│   ├── tests/
│   │   ├── unit/
│   │   ├── integration/
│   │   └── e2e/
│   ├── docs/
│   │   ├── api.md
│   │   └── development.md
│   ├── backups/
│   └── logs/
└── frontend/
    ├── index.html
    ├── css/
    │   ├── core/
    │   │   ├── variables.css
    │   │   ├── reset.css
    │   │   ├── typography.css
    │   │   ├── layout.css
    │   │   └── utilities.css
    │   ├── components/
    │   │   ├── buttons.css
    │   │   ├── forms.css
    │   │   ├── modals.css
    │   │   ├── cards.css
    │   │   ├── tables.css
    │   │   ├── navigation.css
    │   │   ├── charts.css
    │   │   ├── progress.css
    │   │   ├── status.css
    │   │   ├── dropdown.css
    │   │   ├── datepicker.css
    │   │   ├── toast.css
    │   │   ├── loader.css
    │   │   └── kanban.css
    │   ├── pages/
    │   │   ├── auth.css
    │   │   ├── dashboard.css
    │   │   ├── projects.css
    │   │   ├── project-detail.css
    │   │   ├── tasks.css
    │   │   ├── kanban-page.css
    │   │   ├── analytics.css
    │   │   ├── calendar.css
    │   │   ├── reports.css
    │   │   ├── time-tracking.css
    │   │   └── settings.css
    │   └── responsive.css
    ├── js/
    │   ├── app.js
    │   ├── router.js
    │   ├── auth.js
    │   ├── api.js
    │   ├── state.js
    │   ├── components/
    │   │   ├── common/
    │   │   │   ├── Button.js
    │   │   │   ├── Input.js
    │   │   │   ├── Modal.js
    │   │   │   ├── Dropdown.js
    │   │   │   ├── DatePicker.js
    │   │   │   ├── ProgressBar.js
    │   │   │   └── Toast.js
    │   │   ├── layout/
    │   │   │   ├── Sidebar.js
    │   │   │   ├── Header.js
    │   │   │   └── Layout.js
    │   │   ├── dashboard/
    │   │   │   ├── StatCard.js
    │   │   │   ├── TimeLoggedChart.js
    │   │   │   ├── ProjectProgress.js
    │   │   │   ├── TaskOverview.js
    │   │   │   └── ActivityFeed.js
    │   │   ├── kanban/
    │   │   │   ├── KanbanBoard.js
    │   │   │   ├── KanbanColumn.js
    │   │   │   ├── KanbanCard.js
    │   │   │   ├── TaskModal.js
    │   │   │   └── dragDrop.js
    │   │   ├── projects/
    │   │   │   ├── ProjectTable.js
    │   │   │   ├── ProjectForm.js
    │   │   │   └── ProjectCard.js
    │   │   ├── tasks/
    │   │   │   ├── TaskTable.js
    │   │   │   ├── TaskForm.js
    │   │   │   ├── TaskFilters.js
    │   │   │   └── TaskDetail.js
    │   │   ├── analytics/
    │   │   │   ├── Chart.js
    │   │   │   ├── MetricCard.js
    │   │   │   └── ReportGenerator.js
    │   │   ├── calendar/
    │   │   │   ├── CalendarView.js
    │   │   │   ├── CalendarEvent.js
    │   │   │   └── CalendarFilters.js
    │   │   ├── time-tracking/
    │   │   │   ├── TimeLogger.js
    │   │   │   ├── TimeLogTable.js
    │   │   │   └── TimeStats.js
    │   │   ├── comments/
    │   │   │   ├── CommentList.js
    │   │   │   ├── CommentForm.js
    │   │   │   └── CommentItem.js
    │   │   └── reports/
    │   │       ├── ReportBuilder.js
    │   │       ├── ReportPreview.js
    │   │       └── ExportPanel.js
    │   ├── pages/
    │   │   ├── AuthPage.js
    │   │   ├── DashboardPage.js
    │   │   ├── ProjectsPage.js
    │   │   ├── ProjectDetailPage.js
    │   │   ├── TasksPage.js
    │   │   ├── KanbanPage.js
    │   │   ├── AnalyticsPage.js
    │   │   ├── CalendarPage.js
    │   │   ├── ReportsPage.js
    │   │   ├── TimeTrackingPage.js
    │   │   └── SettingsPage.js
    │   └── utils/
    │       ├── helpers.js
    │       ├── dateUtils.js
    │       ├── validation.js
    │       ├── storage.js
    │       └── chartConfig.js
    ├── assets/
    │   ├── icons/
    │   │   ├── auth/
    │   │   ├── navigation/
    │   │   ├── actions/
    │   │   ├── status/
    │   │   ├── calendar/
    │   │   ├── charts/
    │   │   └── general/
    │   └── fonts/
    │       └── inter/
    └── README.md</pre>

## Technical Architecture
### Stack Recommendation
#### Backend
- Runtime: Node.js v18+ with Express.js 5.x
- Database: SQLite with WAL mode for local storage
- Authentication: Opaque tokens stored in database (NOT JWTs)
- File Upload: Multer for file handling
- Date Handling: date-fns for date manipulation
- Security: bcrypt for password hashing, Helmet for security headers

#### Frontend
- Core: Vanilla JavaScript (ES6+) with module system
- Styling: Modern CSS3 with CSS Grid and Flexbox
- Interactions: HTML5 Drag and Drop API for Kanban
- Charts: Custom SVG charts for data visualization
- Storage: Local Storage for user preferences
- Architecture: Component-based with state management

#### Development Tools
- Build Tool: Vite for fast development and building
- Code Quality: ESLint for linting, Prettier for formatting
- Testing: Jest for unit testing, Supertest for API testing
- Process Management: PM2 for production deployment

### Architecture Patterns
#### MVC Structure
<pre>backend/src/
├── models/           # Data layer - database interactions
├── controllers/      # Business logic - request processing
├── routes/          # API endpoints - HTTP routing
├── middleware/      # Cross-cutting concerns
└── utils/           # Helper functions and utilities</pre>

#### Database-First Approach
- SQLite for simplicity and portability
- Migration system for schema versioning
- Indexes for query optimization
- Foreign keys for data integrity

## UI/UX Design Guidelines
### Color Palette (Professional & Muted)
```css
:root {
  /* Primary Brand Colors - Professional Teal */
  --color-primary: #049592;          /* Main teal primary */
  --color-primary-light: #edf4f2;    /* Very light mint background */
  --color-primary-dark: #037571;     /* Dark teal */
  
  /* Secondary Colors - Warm Accent */
  --color-secondary: #eaca6a;        /* Professional yellow accent */
  --color-secondary-light: #d5c99d;  /* Light cream */
  --color-secondary-dark: #c5b455;   /* Darker yellow */
  
  /* Neutral Colors - Professional Grays */
  --color-white: #FFFFFF;
  --color-gray-charcoal: #323435;    /* Main text color */
  --color-gray-brown: #7f6b5e;       /* Secondary text */
  --color-gray-sage: #90a2a0;        /* Muted sage green */
  --color-gray-light: #bbc2c2;       /* Light gray borders */
  --color-gray-lighter: #cdcac8;     /* Very light gray */
  --color-gray-beige: #b2a69f;       /* Warm beige */
  
  /* Background Colors */
  --color-bg-primary: #FFFFFF;
  --color-bg-secondary: #edf4f2;
  --color-bg-tertiary: #cdcac8;
  
  /* Status Colors */
  --color-success: #049592;          /* Teal for success */
  --color-warning: #eaca6a;          /* Yellow for warnings */
  --color-danger: #7f6b5e;           /* Brown for errors */
  --color-info: #90a2a0;             /* Sage for info */
}
```

### Typography System
```css
:root {
  /* Font Families */
  --font-primary: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', monospace;
  
  /* Font Sizes */
  --text-xs: 0.75rem;     /* 12px */
  --text-sm: 0.875rem;    /* 14px */
  --text-base: 1rem;      /* 16px */
  --text-lg: 1.125rem;    /* 18px */
  --text-xl: 1.25rem;     /* 20px */
  --text-2xl: 1.5rem;     /* 24px */
  --text-3xl: 1.75rem;    /* 28px */
  --text-4xl: 2.25rem;    /* 36px */
  
  /* Font Weights */
  --font-normal: 400;
  --font-medium: 500;
  --font-semibold: 600;
  --font-bold: 700;
  
  /* Line Heights */
  --leading-tight: 1.25;
  --leading-normal: 1.5;
  --leading-relaxed: 1.75;
}
```

### Spacing System
```css
:root {
  --space-1: 0.25rem;    /* 4px */
  --space-2: 0.5rem;     /* 8px */
  --space-3: 0.75rem;    /* 12px */
  --space-4: 1rem;       /* 16px */
  --space-5: 1.25rem;    /* 20px */
  --space-6: 1.5rem;     /* 24px */
  --space-8: 2rem;       /* 32px */
  --space-10: 2.5rem;    /* 40px */
  --space-12: 3rem;      /* 48px */
  --space-16: 4rem;      /* 64px */
  --space-20: 5rem;      /* 80px */
  --space-24: 6rem;      /* 96px */
}
```

### Shadow and Border System
```css
:root {
  /* Shadows */
  --shadow-sm: 0 1px 2px 0 rgba(4, 149, 146, 0.05);
  --shadow-md: 0 4px 6px -1px rgba(4, 149, 146, 0.1), 0 2px 4px -1px rgba(4, 149, 146, 0.06);
  --shadow-lg: 0 10px 15px -3px rgba(4, 149, 146, 0.1), 0 4px 6px -2px rgba(4, 149, 146, 0.05);
  --shadow-xl: 0 20px 25px -5px rgba(4, 149, 146, 0.1), 0 10px 10px -5px rgba(4, 149, 146, 0.04);
  
  /* Border Radius */
  --radius-sm: 0.375rem;  /* 6px */
  --radius-md: 0.5rem;    /* 8px */
  --radius-lg: 0.75rem;   /* 12px */
  --radius-xl: 1rem;      /* 16px */
  --radius-full: 9999px;  /* Full round */
}
```

### Component Design Principles
#### Modern Card Design
- Clean white background with subtle teal-tinted shadows
- Rounded corners (16px border radius)
- Proper spacing and padding (24px)
- Gradient top borders for visual hierarchy
- Smooth hover transitions with elevation changes

#### Interactive Elements
- Hover effects with subtle elevation changes
- Smooth transitions (200-300ms ease)
- Professional color feedback for different states
- Modern button styling with proper contrast
- Loading states with skeleton screens

#### Data Visualization
- Custom SVG charts using brand colors
- Interactive elements with hover states
- Progress indicators with teal gradient fills
- Visual hierarchy with typography and spacing

## Dashboard Specifications
### Layout Structure
The dashboard uses a responsive 4-column grid system with the following structure:

#### Row 1: Quick Statistics (4 columns)
- Total Projects
- Completed Tasks
- Overdue Tasks
- Productivity Rate

#### Row 2: Time Management (4 columns)
- Time Logged (Full width with chart visualization)

#### Row 3: Project & Task Details (4 columns)
- Recent Projects (2 columns)
- Task Overview (2 columns)

#### Row 4: Activity Stream (4 columns)
- Recent Activity (Full width)

### Dashboard Components
#### 1. Statistics Cards
```javascript
// Component Structure
{
  icon: "SVG_ICON",
  number: "METRIC_VALUE", 
  label: "METRIC_DESCRIPTION",
  trend: "PERCENTAGE_CHANGE",
  trendDirection: "up|down|neutral"
}
```

##### Metrics:
- Total Projects: Count of all projects
- Completed Tasks: Count of tasks with status "done"
- Overdue Tasks: Count of tasks past due date
- Productivity Rate: Percentage based on completed vs total tasks

#### 2. Time Logged Chart
```javascript
// Component Structure
{
  totalHours: "MONTHLY_TOTAL",
  periodData: [
    { month: "Jan", hours: 40 },
    { month: "Feb", hours: 55 },
    // ... 12 months
  ],
  tabs: ["Monthly", "Quarterly", "Annually"],
  changePercentage: "+6%"
}
```

##### Features:
- Interactive bar chart with 12 months of data
- Tabbed view for different time periods
- Highlighted current month
- Trend indicators

#### 3. Recent Projects
```javascript
// Component Structure
{
  projects: [
    {
      name: "PROJECT_NAME",
      completedTasks: NUMBER,
      totalTasks: NUMBER,
      dueDate: "DATE",
      progressPercentage: NUMBER
    }
  ]
}
```

##### Features:
- Progress bars with completion percentages
- Due date indicators
- Task completion ratios

#### 4. Task Overview
```javascript
// Component Structure
{
  taskCounts: {
    todo: NUMBER,
    inProgress: NUMBER,
    review: NUMBER,
    done: NUMBER
  },
  recentTasks: [
    {
      title: "TASK_TITLE",
      project: "PROJECT_NAME", 
      status: "todo|in_progress|review|done"
    }
  ]
}
```

##### Features:
- Status distribution grid
- Recent task list with status badges
- Quick task overview

#### 5. Recent Activity
```javascript
// Component Structure
{
  activities: [
    {
      user: "USER_NAME",
      action: "ACTION_TYPE",
      target: "TARGET_OBJECT",
      project: "PROJECT_NAME",
      timestamp: "TIME_AGO",
      icon: "ACTION_ICON"
    }
  ]
}
```

##### Action Types:
- Task completion
- Task creation
- Project creation
- Status updates
- Time logging

### Responsive Behavior
```css
/* Desktop (1400px+) */
.dashboard-grid {
  grid-template-columns: repeat(4, 1fr);
}

/* Tablet (1024px - 1399px) */
@media (max-width: 1399px) {
  .dashboard-grid {
    grid-template-columns: repeat(3, 1fr);
  }
  .time-logged-card,
  .recent-activity-card {
    grid-column: span 3;
  }
}

/* Mobile (768px - 1023px) */
@media (max-width: 1023px) {
  .dashboard-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .time-logged-card,
  .recent-projects-card,
  .task-overview-card,
  .recent-activity-card {
    grid-column: span 2;
  }
}

/* Small Mobile (767px and below) */
@media (max-width: 767px) {
  .dashboard-grid {
    grid-template-columns: 1fr;
  }
  .stat-card,
  .time-logged-card,
  .recent-projects-card,
  .task-overview-card,
  .recent-activity-card {
    grid-column: span 1;
  }
}
```

## Database Schema
### Tables Structure
#### Users Table
```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  username VARCHAR(50) UNIQUE NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  full_name VARCHAR(100),
  timezone VARCHAR(50) DEFAULT 'UTC',
  preferences TEXT, -- JSON string
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

#### Sessions Table
```sql
CREATE TABLE sessions (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  token VARCHAR(255) UNIQUE NOT NULL,
  expires_at DATETIME NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  last_used_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  user_agent TEXT,
  ip_address VARCHAR(45),
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

#### Projects Table
```sql
CREATE TABLE projects (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  name VARCHAR(200) NOT NULL,
  description TEXT,
  status VARCHAR(20) DEFAULT 'active', -- active, planning, review, completed, archived
  priority VARCHAR(10) DEFAULT 'medium', -- low, medium, high
  start_date DATE,
  due_date DATE,
  completion_percentage INTEGER DEFAULT 0,
  color VARCHAR(7), -- hex color code
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

#### Tasks Table
```sql
CREATE TABLE tasks (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  project_id INTEGER NOT NULL,
  user_id INTEGER NOT NULL,
  title VARCHAR(200) NOT NULL,
  description TEXT,
  status VARCHAR(20) DEFAULT 'todo', -- todo, in_progress, review, done
  priority VARCHAR(10) DEFAULT 'medium', -- low, medium, high
  due_date DATETIME,
  estimated_hours DECIMAL(5,2),
  actual_hours DECIMAL(5,2),
  tags TEXT, -- JSON array
  position INTEGER DEFAULT 0, -- for kanban ordering
  completed_at DATETIME,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (project_id) REFERENCES projects(id) ON DELETE CASCADE,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

#### Task Comments Table
```sql
CREATE TABLE task_comments (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  task_id INTEGER NOT NULL,
  user_id INTEGER NOT NULL,
  content TEXT NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (task_id) REFERENCES tasks(id) ON DELETE CASCADE,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

#### Time Logs Table
```sql
CREATE TABLE time_logs (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  task_id INTEGER NOT NULL,
  user_id INTEGER NOT NULL,
  description TEXT,
  duration_minutes INTEGER NOT NULL,
  logged_date DATE NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (task_id) REFERENCES tasks(id) ON DELETE CASCADE,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

#### Milestones Table
```sql
CREATE TABLE milestones (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  project_id INTEGER NOT NULL,
  name VARCHAR(200) NOT NULL,
  description TEXT,
  due_date DATE,
  status VARCHAR(20) DEFAULT 'pending', -- pending, completed
  completed_at DATETIME,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (project_id) REFERENCES projects(id) ON DELETE CASCADE
);
```

#### Reports Table
```sql
CREATE TABLE reports (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  name VARCHAR(200) NOT NULL,
  type VARCHAR(50) NOT NULL, -- weekly, project_summary, time_tracking, etc.
  parameters TEXT, -- JSON string of report parameters
  generated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  file_path VARCHAR(500),
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

#### Database Indexes
```sql
-- Performance indexes
CREATE INDEX idx_tasks_project_id ON tasks(project_id);
CREATE INDEX idx_tasks_user_id ON tasks(user_id);
CREATE INDEX idx_tasks_status ON tasks(status);
CREATE INDEX idx_tasks_due_date ON tasks(due_date);
CREATE INDEX idx_projects_user_id ON projects(user_id);
CREATE INDEX idx_projects_status ON projects(status);
CREATE INDEX idx_time_logs_task_id ON time_logs(task_id);
CREATE INDEX idx_time_logs_logged_date ON time_logs(logged_date);
CREATE INDEX idx_sessions_token ON sessions(token);
CREATE INDEX idx_sessions_user_id ON sessions(user_id);
CREATE INDEX idx_sessions_expires_at ON sessions(expires_at);
CREATE INDEX idx_task_comments_task_id ON task_comments(task_id);
CREATE INDEX idx_milestones_project_id ON milestones(project_id);
CREATE INDEX idx_reports_user_id ON reports(user_id);
```

## Backend Implementation
### Server Configuration
```javascript
// server.js
import express from 'express';
import cors from 'cors';
import helmet from 'helmet';
import cookieParser from 'cookie-parser';
import path from 'path';
import { fileURLToPath } from 'url';
import { Database } from './src/config/database.js';
import { authRoutes } from './src/routes/auth.js';
import { projectRoutes } from './src/routes/projects.js';
import { taskRoutes } from './src/routes/tasks.js';
import { analyticsRoutes } from './src/routes/analytics.js';
import { reportRoutes } from './src/routes/reports.js';
import { timeTrackingRoutes } from './src/routes/timetracking.js';
import { commentRoutes } from './src/routes/comments.js';
import { milestoneRoutes } from './src/routes/milestones.js';
import { errorHandler } from './src/middleware/errorHandler.js';
import { authMiddleware } from './src/middleware/auth.js';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

const app = express();
const PORT = process.env.PORT || 3000;

// Initialize database
const db = new Database();
await db.initialize();

// Security middleware
app.use(helmet({
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      styleSrc: ["'self'", "'unsafe-inline'"],
      scriptSrc: ["'self'"],
      imgSrc: ["'self'", "data:", "https:"],
    },
  },
}));

app.use(cors({
  origin: process.env.FRONTEND_URL || 'http://localhost:3000',
  credentials: true
}));

app.use(express.json({ limit: '10mb' }));
app.use(express.urlencoded({ extended: true }));
app.use(cookieParser());

// Serve static files
app.use(express.static(path.join(__dirname, '../frontend')));

// API Routes
app.use('/api/auth', authRoutes);
app.use('/api/projects', authMiddleware, projectRoutes);
app.use('/api/tasks', authMiddleware, taskRoutes);
app.use('/api/analytics', authMiddleware, analyticsRoutes);
app.use('/api/reports', authMiddleware, reportRoutes);
app.use('/api/time-logs', authMiddleware, timeTrackingRoutes);
app.use('/api/comments', authMiddleware, commentRoutes);
app.use('/api/milestones', authMiddleware, milestoneRoutes);

// Health check
app.get('/health', (req, res) => {
  res.json({ status: 'ok', timestamp: new Date().toISOString() });
});

// Error handling
app.use(errorHandler);

// SPA fallback
app.get('*', (req, res) => {
  res.sendFile(path.join(__dirname, '../frontend', 'index.html'));
});

app.listen(PORT, () => {
  console.log(`ProjectFlow server running on http://localhost:${PORT}`);
});
```

### BaseModel Class
```javascript
// src/models/BaseModel.js
import { Database } from '../config/database.js';

export class BaseModel {
  constructor(tableName) {
    this.tableName = tableName;
    this.db = Database.getInstance();
  }

  async findAll(filters = {}, options = {}) {
    const { limit = 50, offset = 0, orderBy = 'created_at DESC' } = options;
    
    let query = `SELECT * FROM ${this.tableName}`;
    const params = [];
    
    if (Object.keys(filters).length > 0) {
      const conditions = Object.keys(filters).map(key => {
        params.push(filters[key]);
        return `${key} = ?`;
      });
      query += ` WHERE ${conditions.join(' AND ')}`;
    }
    
    query += ` ORDER BY ${orderBy} LIMIT ? OFFSET ?`;
    params.push(limit, offset);
    
    return await this.db.all(query, params);
  }

  async findById(id, userId = null) {
    let query = `SELECT * FROM ${this.tableName} WHERE id = ?`;
    const params = [id];
    
    if (userId) {
      query += ' AND user_id = ?';
      params.push(userId);
    }
    
    return await this.db.get(query, params);
  }

  async create(data) {
    const sanitizedData = this.sanitizeData(data);
    const columns = Object.keys(sanitizedData);
    const placeholders = columns.map(() => '?').join(', ');
    const values = Object.values(sanitizedData);
    
    const query = `
      INSERT INTO ${this.tableName} (${columns.join(', ')})
      VALUES (${placeholders})
    `;
    
    const result = await this.db.run(query, values);
    return await this.findById(result.lastID);
  }

  async update(id, data) {
    const sanitizedData = this.sanitizeData(data);
    sanitizedData.updated_at = new Date().toISOString();
    
    const columns = Object.keys(sanitizedData);
    const setClause = columns.map(col => `${col} = ?`).join(', ');
    const values = [...Object.values(sanitizedData), id];
    
    const query = `UPDATE ${this.tableName} SET ${setClause} WHERE id = ?`;
    
    await this.db.run(query, values);
    return await this.findById(id);
  }

  async delete(id) {
    const query = `DELETE FROM ${this.tableName} WHERE id = ?`;
    return await this.db.run(query, [id]);
  }

  async count(filters = {}) {
    let query = `SELECT COUNT(*) as count FROM ${this.tableName}`;
    const params = [];
    
    if (Object.keys(filters).length > 0) {
      const conditions = Object.keys(filters).map(key => {
        params.push(filters[key]);
        return `${key} = ?`;
      });
      query += ` WHERE ${conditions.join(' AND ')}`;
    }
    
    const result = await this.db.get(query, params);
    return result.count;
  }

  sanitizeData(data) {
    const sanitized = { ...data };
    
    // Remove undefined values
    Object.keys(sanitized).forEach(key => {
      if (sanitized[key] === undefined) {
        delete sanitized[key];
      }
    });
    
    // Add timestamps if creating
    if (!sanitized.id && !sanitized.created_at) {
      sanitized.created_at = new Date().toISOString();
    }
    
    return sanitized;
  }

  async withTransaction(callback) {
    await this.db.exec('BEGIN TRANSACTION');
    try {
      const result = await callback();
      await this.db.exec('COMMIT');
      return result;
    } catch (error) {
      await this.db.exec('ROLLBACK');
      throw error;
    }
  }
}
```

## Frontend Implementation
### Component Architecture
#### StatCard Component
```javascript
// js/components/dashboard/StatCard.js
export class StatCard {
  constructor(config) {
    this.config = {
      icon: '',
      number: '',
      label: '',
      trend: '',
      trendDirection: 'neutral', // up, down, neutral
      color: 'primary',
      ...config
    };
    this.element = this.createElement();
  }
  
  createElement() {
    const card = document.createElement('div');
    card.className = 'card stat-card';
    
    const trendClass = `trend-${this.config.trendDirection}`;
    const iconClass = `stat-icon-${this.config.color}`;
    
    card.innerHTML = `
      <div class="stat-icon ${iconClass}">
        ${this.config.icon}
      </div>
      <div class="stat-number">${this.config.number}</div>
      <div class="stat-label">${this.config.label}</div>
      <div class="stat-trend ${trendClass}">
        ${this.config.trend}
      </div>
    `;
    
    return card;
  }
  
  updateValue(newNumber, newTrend, newDirection) {
    this.config.number = newNumber;
    this.config.trend = newTrend;
    this.config.trendDirection = newDirection;
    
    const numberEl = this.element.querySelector('.stat-number');
    const trendEl = this.element.querySelector('.stat-trend');
    
    numberEl.textContent = newNumber;
    trendEl.textContent = newTrend;
    trendEl.className = `stat-trend trend-${newDirection}`;
  }
}
```

#### TimeLoggedChart Component
```javascript
// js/components/dashboard/TimeLoggedChart.js
export class TimeLoggedChart {
  constructor(config) {
    this.config = {
      totalHours: 0,
      monthlyData: [],
      changePercentage: '',
      activeTab: 'Monthly',
      ...config
    };
    
    this.element = this.createElement();
    this.setupEventListeners();
  }
  
  createElement() {
    const container = document.createElement('div');
    container.className = 'card time-logged-card';
    
    container.innerHTML = `
      <div class="time-header">
        <div class="time-info">
          <h3>Time Logged</h3>
          <div class="time-number">${this.config.totalHours}</div>
          <div class="time-label">hours this month</div>
          <div class="time-change">${this.config.changePercentage}</div>
        </div>
        <div class="time-controls">
          <div class="time-tabs">
            <button class="tab active" data-period="Monthly">Monthly</button>
            <button class="tab" data-period="Quarterly">Quarterly</button>
            <button class="tab" data-period="Annually">Annually</button>
          </div>
        </div>
      </div>
      <div class="chart-container">
        ${this.renderChart()}
      </div>
      <div class="chart-labels">
        ${this.renderLabels()}
      </div>
    `;
    
    return container;
  }
  
  renderChart() {
    return this.config.monthlyData.map((data, index) => {
      const height = Math.max((data.hours / Math.max(...this.config.monthlyData.map(d => d.hours))) * 100, 10);
      const isActive = data.month === this.getCurrentMonth();
      
      return `
        <div class="chart-bar ${isActive ? 'active' : ''}" 
             style="height: ${height}px;" 
             data-month="${data.month}"
             data-hours="${data.hours}">
        </div>
      `;
    }).join('');
  }
  
  renderLabels() {
    return this.config.monthlyData.map(data => 
      `<div class="chart-label">${data.month}</div>`
    ).join('');
  }
  
  setupEventListeners() {
    this.element.addEventListener('click', (e) => {
      if (e.target.classList.contains('tab')) {
        this.handleTabClick(e.target);
      }
    });
  }
  
  handleTabClick(tabElement) {
    // Remove active class from all tabs
    this.element.querySelectorAll('.tab').forEach(tab => 
      tab.classList.remove('active')
    );
    
    // Add active class to clicked tab
    tabElement.classList.add('active');
    
    // Update data based on selected period
    const period = tabElement.dataset.period;
    this.updateChartData(period);
  }
  
  async updateChartData(period) {
    try {
      const response = await fetch(`/api/analytics/time-logged?period=${period}`);
      const data = await response.json();
      
      if (data.success) {
        this.config.monthlyData = data.chartData;
        this.config.totalHours = data.totalHours;
        this.config.changePercentage = data.changePercentage;
        
        this.refreshChart();
      }
    } catch (error) {
      console.error('Error updating chart data:', error);
    }
  }
  
  refreshChart() {
    const chartContainer = this.element.querySelector('.chart-container');
    const labelsContainer = this.element.querySelector('.chart-labels');
    const timeNumber = this.element.querySelector('.time-number');
    const timeChange = this.element.querySelector('.time-change');
    
    chartContainer.innerHTML = this.renderChart();
    labelsContainer.innerHTML = this.renderLabels();
    timeNumber.textContent = this.config.totalHours;
    timeChange.textContent = this.config.changePercentage;
  }
  
  getCurrentMonth() {
    const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
                   'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
    return months[new Date().getMonth()];
  }
}
```

#### State Management
```javascript
// js/state.js
export class StateManager {
  constructor() {
    this.state = {};
    this.listeners = {};
  }
  
  setState(key, value) {
    const oldValue = this.state[key];
    this.state[key] = value;
    
    if (this.listeners[key] && oldValue !== value) {
      this.listeners[key].forEach(listener => listener(value, oldValue));
    }
  }
  
  getState(key) {
    return this.state[key];
  }
  
  subscribe(key, listener) {
    if (!this.listeners[key]) {
      this.listeners[key] = [];
    }
    this.listeners[key].push(listener);
    
    // Return unsubscribe function
    return () => {
      this.listeners[key] = this.listeners[key].filter(l => l !== listener);
    };
  }
  
  async loadDashboardData() {
    try {
      const response = await fetch('/api/analytics/dashboard');
      const data = await response.json();
      
      if (data.success) {
        this.setState('dashboardStats', data.stats);
        this.setState('timeLoggedData', data.timeLogged);
        this.setState('recentProjects', data.recentProjects);
        this.setState('taskOverview', data.taskOverview);
        this.setState('recentActivity', data.recentActivity);
      }
    } catch (error) {
      console.error('Error loading dashboard data:', error);
    }
  }
  
  dispatch(action) {
    switch (action.type) {
      case 'SET_CURRENT_USER':
        this.setState('currentUser', action.payload);
        break;
      case 'SET_CURRENT_PROJECT':
        this.setState('currentProject', action.payload);
        break;
      case 'UPDATE_DASHBOARD_STATS':
        this.setState('dashboardStats', action.payload);
        break;
      case 'ADD_TASK':
        const tasks = this.getState('tasks') || [];
        this.setState('tasks', [...tasks, action.payload]);
        break;
      case 'UPDATE_TASK':
        const allTasks = this.getState('tasks') || [];
        const updatedTasks = allTasks.map(task => 
          task.id === action.payload.id ? { ...task, ...action.payload } : task
        );
        this.setState('tasks', updatedTasks);
        break;
      case 'REMOVE_TASK':
        const remainingTasks = (this.getState('tasks') || []).filter(
          task => task.id !== action.payload
        );
        this.setState('tasks', remainingTasks);
        break;
      default:
        console.warn('Unknown action type:', action.type);
    }
  }
}

// Global state instance
export const appState = new StateManager();
```

## API Specification
### Dashboard Analytics Endpoints
```javascript
// GET /api/analytics/dashboard
// Response
{
  "success": true,
  "data": {
    "stats": {
      "totalProjects": 24,
      "completedTasks": 147,
      "overdueTasks": 6,
      "productivityRate": 85
    },
    "timeLogged": {
      "totalHours": 162,
      "changePercentage": "+6%",
      "monthlyData": [
        { "month": "Jan", "hours": 40 },
        { "month": "Feb", "hours": 55 },
        // ... 12 months
      ]
    },
    "recentProjects": [
      {
        "id": 1,
        "name": "Website Redesign",
        "completedTasks": 9,
        "totalTasks": 12,
        "dueDate": "2025-07-15",
        "progressPercentage": 75
      }
    ],
    "taskOverview": {
      "counts": {
        "todo": 15,
        "in_progress": 8,
        "review": 4,
        "done": 147
      },
      "recentTasks": [
        {
          "id": 1,
          "title": "Review API documentation",
          "project": "Website Redesign",
          "status": "in_progress"
        }
      ]
    },
    "recentActivity": [
      {
        "id": 1,
        "user": "John Doe",
        "action": "completed",
        "target": "Review API documentation",
        "project": "Website Redesign",
        "timestamp": "2 hours ago",
        "icon": "check"
      }
    ]
  }
}
```

### Time Tracking Endpoints
```javascript
// GET /api/analytics/time-logged?period=Monthly
// Response
{
  "success": true,
  "data": {
    "totalHours": 162,
    "changePercentage": "+6%",
    "chartData": [
      { "month": "Jan", "hours": 40 },
      { "month": "Feb", "hours": 55 },
      // ... based on period
    ]
  }
}

// POST /api/time-logs
// Request
{
  "taskId": 1,
  "description": "Working on API documentation",
  "durationMinutes": 120,
  "loggedDate": "2025-06-24"
}

// Response
{
  "success": true,
  "data": {
    "id": 1,
    "taskId": 1,
    "description": "Working on API documentation",
    "durationMinutes": 120,
    "loggedDate": "2025-06-24",
    "createdAt": "2025-06-24T10:30:00Z"
  }
}
```

### Project Endpoints
```javascript
// GET /api/projects
// Query Parameters: ?status=active&limit=10&offset=0

// Response
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Website Redesign",
      "description": "Complete redesign of company website",
      "status": "active",
      "priority": "high",
      "startDate": "2025-01-01",
      "dueDate": "2025-03-01",
      "completionPercentage": 75,
      "taskCount": 12,
      "completedTasks": 9,
      "createdAt": "2025-01-01T00:00:00Z"
    }
  ],
  "total": 24,
  "page": 1,
  "limit": 10
}

// POST /api/projects
// Request
{
  "name": "Mobile App Development",
  "description": "Native mobile app for iOS and Android",
  "priority": "high",
  "startDate": "2025-07-01",
  "dueDate": "2025-12-01",
  "color": "#049592"
}

// Response
{
  "success": true,
  "data": {
    "id": 5,
    "name": "Mobile App Development",
    "status": "active",
    "completionPercentage": 0,
    // ... other fields
  }
}
```

### Task Endpoints
```javascript
// GET /api/tasks
// Query Parameters: ?project_id=1&status=todo&priority=high

// Response
{
  "success": true,
  "data": [
    {
      "id": 1,
      "title": "Review API documentation",
      "description": "Review and update API documentation",
      "status": "in_progress",
      "priority": "high",
      "dueDate": "2025-07-15T23:59:59Z",
      "project": {
        "id": 1,
        "name": "Website Redesign"
      },
      "estimatedHours": 4,
      "actualHours": 2.5,
      "position": 0,
      "createdAt": "2025-06-01T00:00:00Z"
    }
  ]
}

// PATCH /api/tasks/:id/status
// Request
{
  "status": "done",
  "position": 1
}

// Response
{
  "success": true,
  "data": {
    "id": 1,
    "status": "done",
    "completedAt": "2025-06-24T15:30:00Z",
    // ... other fields
  }
}
```

## Component Architecture
### Layout Components
#### Sidebar Component
```javascript
// js/components/layout/Sidebar.js
export class Sidebar {
  constructor() {
    this.activeItem = 'dashboard';
    this.element = this.createElement();
    this.setupEventListeners();
  }
  
  createElement() {
    const sidebar = document.createElement('div');
    sidebar.className = 'sidebar';
    
    sidebar.innerHTML = `
      <div class="logo">
        <svg viewBox="0 0 24 24" fill="currentColor">
          <path d="M7 14l3-3 3 3 5-5-1.41-1.42L12 12.17 9 9.17 4.41 13.58z"/>
        </svg>
      </div>
      <div class="nav-items">
        ${this.renderNavItems()}
      </div>
    `;
    
    return sidebar;
  }
  
  renderNavItems() {
    const navItems = [
      { id: 'dashboard', icon: 'home', title: 'Dashboard' },
      { id: 'projects', icon: 'folder', title: 'Projects' },
      { id: 'tasks', icon: 'check', title: 'Tasks' },
      { id: 'kanban', icon: 'grid', title: 'Kanban' },
      { id: 'analytics', icon: 'chart', title: 'Analytics' },
      { id: 'calendar', icon: 'calendar', title: 'Calendar' },
      { id: 'reports', icon: 'document', title: 'Reports' },
      { id: 'time-tracking', icon: 'clock', title: 'Time Tracking' },
      { id: 'settings', icon: 'settings', title: 'Settings' }
    ];
    
    return navItems.map(item => `
      <div class="nav-item ${item.id === this.activeItem ? 'active' : ''}" 
           data-page="${item.id}" 
           title="${item.title}">
        ${this.getIcon(item.icon)}
      </div>
    `).join('');
  }
  
  getIcon(iconName) {
    const icons = {
      home: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/></svg>',
      folder: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M10,4H4C2.89,4 2,4.89 2,6V18A2,2 0 0,0 4,20H20A2,2 0 0,0 22,18V8C22,6.89 21.1,6 20,6H12L10,4Z"/></svg>',
      check: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M9,20.42L2.79,14.21L5.62,11.38L9,14.77L18.88,4.88L21.71,7.71L9,20.42Z"/></svg>',
      grid: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M5,5H10V10H5V5M14,5H19V10H14V5M14,14H19V19H14V14M5,14H10V19H5V14Z"/></svg>',
      chart: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M16,bc1qre8jdw2azrg6tf49wmp652w00xltddxmpk98xp,8H13V13H7V8M8,4H15V10H17V20H5V10H7V4Z"/></svg>',
      calendar: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M19,3H18V1H16V3H8V1H6V3H5C3.89,3 3,3.9 3,5V19A2,2 0 0,0 5,21H19A2,2 0 0,0 21,19V5A2,2 0 0,0 19,3M19,19H5V8H19V19Z"/></svg>',
      document: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M14,2H6A2,2 0 0,0 4,4V20A2,2 0 0,0 6,22H18A2,2 0 0,0 20,20V8L14,2M18,20H6V4H13V9H18V20Z"/></svg>',
      clock: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2M16.2,16.2L11,13V7H12.5V12.2L17,14.7L16.2,16.2Z"/></svg>',
      settings: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M12,15.5A3.5,3.5 0 0,1 8.5,12A3.5,3.5 0 0,1 12,8.5A3.5,3.5 0 0,1 15.5,12A3.5,3.5 0 0,1 12,15.5M19.43,12.97C19.47,12.65 19.5,12.33 19.5,12C19.5,11.67 19.47,11.34 19.43,11L21.54,9.37C21.73,9.22 21.78,8.95 21.66,8.73L19.66,5.27C19.54,5.05 19.27,4.96 19.05,5.05L16.56,6.05C16.04,5.66 15.5,5.32 14.87,5.07L14.5,2.42C14.46,2.18 14.25,2 14,2H10C9.75,2 9.54,2.18 9.5,2.42L9.13,5.07C8.5,5.32 7.96,5.66 7.44,6.05L4.95,5.05C4.73,4.96 4.46,5.05 4.34,5.27L2.34,8.73C2.22,8.95 2.27,9.22 2.46,9.37L4.57,11C4.53,11.34 4.5,11.67 4.5,12C4.5,12.33 4.53,12.65 4.57,12.97L2.46,14.63C2.27,14.78 2.22,15.05 2.34,15.27L4.34,18.73C4.46,18.95 4.73,19.03 4.95,18.95L7.44,17.94C7.96,18.34 8.5,18.68 9.13,18.93L9.5,21.58C9.54,21.82 9.75,22 10,22H14C14.25,22 14.46,21.82 14.5,21.58L14.87,18.93C15.5,18.68 16.04,18.34 16.56,17.94L19.05,18.95C19.27,19.03 19.54,18.95 19.66,18.73L21.66,15.27C21.78,15.05 21.73,14.78 21.54,14.63L19.43,12.97Z"/></svg>'
    };
    
    return icons[iconName] || '';
  }
  
  setupEventListeners() {
    this.element.addEventListener('click', (e) => {
      const navItem = e.target.closest('.nav-item');
      if (navItem) {
        this.handleNavClick(navItem);
      }
    });
  }
  
  handleNavClick(navItem) {
    const page = navItem.dataset.page;
    
    // Update active state
    this.element.querySelectorAll('.nav-item').forEach(item => 
      item.classList.remove('active')
    );
    navItem.classList.add('active');
    
    // Emit navigation event
    this.element.dispatchEvent(new CustomEvent('navigate', {
      detail: { page }
    }));
    
    this.activeItem = page;
  }
  
  setActivePage(page) {
    this.activeItem = page;
    
    this.element.querySelectorAll('.nav-item').forEach(item => {
      item.classList.toggle('active', item.dataset.page === page);
    });
  }
}
```

#### Dashboard Page Component
```javascript
// js/pages/DashboardPage.js
import { StatCard } from '../components/dashboard/StatCard.js';
import { TimeLoggedChart } from '../components/dashboard/TimeLoggedChart.js';
import { appState } from '../state.js';

export class DashboardPage {
  constructor() {
    this.components = {};
    this.element = this.createElement();
    this.initializeComponents();
    this.loadData();
  }
  
  createElement() {
    const page = document.createElement('div');
    page.className = 'dashboard-content';
    
    page.innerHTML = `
      <div class="dashboard-header">
        <div class="welcome-section">
          <div class="welcome-text">
            <h1>Welcome back, John!</h1>
            <p>Here's a quick overview of your current project progress and productivity metrics.</p>
          </div>
          <div class="header-actions-dashboard">
            <button class="btn btn-secondary" id="generate-report">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path d="M14,2H6A2,2 0 0,0 4,4V20A2,2 0 0,0 6,22H18A2,2 0 0,0 20,20V8L14,2M18,20H6V4H13V9H18V20Z"/>
              </svg>
              Generate Report
            </button>
            <button class="btn btn-primary" id="new-project">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path d="M19,bc1qre8jdw2azrg6tf49wmp652w00xltddxmpk98xp"/>
              </svg>
              New Project
            </button>
          </div>
        </div>
      </div>
      <div class="dashboard-grid">
        <div id="total-projects-card"></div>
        <div id="completed-tasks-card"></div>
        <div id="overdue-tasks-card"></div>
        <div id="productivity-rate-card"></div>
        <div id="time-logged-chart"></div>
        <div id="recent-projects"></div>
        <div id="task-overview"></div>
        <div id="recent-activity"></div>
      </div>
    `;
    
    return page;
  }
  
  initializeComponents() {
    // Initialize stat cards
    this.components.totalProjects = new StatCard({
      icon: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M10,4H4C2.89,4 2,4.89 2,6V18A2,2 0 0,0 4,20H20A2,2 0 0,0 22,18V8C22,6.89 21.1,6 20,6H12L10,4Z"/></svg>',
      number: '24',
      label: 'Total Projects',
      trend: '↗ +12% from last month',
      trendDirection: 'up'
    });
    
    this.components.completedTasks = new StatCard({
      icon: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M9,20.42L2.79,14.21L5.62,11.38L9,14.77L18.88,4.88L21.71,7.71L9,20.42Z"/></svg>',
      number: '147',
      label: 'Completed Tasks',
      trend: '↗ +23% from last month',
      trendDirection: 'up'
    });
    
    this.components.overdueTasks = new StatCard({
      icon: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2M16.2,16.2L11,13V7H12.5V12.2L17,14.7L16.2,16.2Z"/></svg>',
      number: '6',
      label: 'Overdue Tasks',
      trend: '↘ -8% from last month',
      trendDirection: 'down'
    });
    
    this.components.productivityRate = new StatCard({
      icon: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M16,bc1qre8jdw2azrg6tf49wmp652w00xltddxmpk98xp,8H13V13H7V8M8,4H15V10H17V20H5V10H7V4Z"/></svg>',
      number: '85%',
      label: 'Productivity Rate',
      trend: '↗ +5% from last month',
      trendDirection: 'up'
    });
    
    // Initialize time logged chart
    this.components.timeLoggedChart = new TimeLoggedChart({
      totalHours: 162,
      changePercentage: '+6% from last month',
      monthlyData: [
        { month: 'Jan', hours: 40 },
        { month: 'Feb', hours: 55 },
        { month: 'Mar', hours: 35 },
        { month: 'Apr', hours: 45 },
        { month: 'May', hours: 30 },
        { month: 'Jun', hours: 85 },
        { month: 'Jul', hours: 50 },
        { month: 'Aug', hours: 65 },
        { month: 'Sep', hours: 40 },
        { month: 'Oct', hours: 35 },
        { month: 'Nov', hours: 45 },
        { month: 'Dec', hours: 30 }
      ]
    });
  }
  
  async loadData() {
    await appState.loadDashboardData();
    
    // Subscribe to state changes
    appState.subscribe('dashboardStats', (stats) => {
      this.updateStatCards(stats);
    });
    
    appState.subscribe('timeLoggedData', (data) => {
      this.components.timeLoggedChart.updateChartData(data);
    });
  }
  
  updateStatCards(stats) {
    if (stats) {
      this.components.totalProjects.updateValue(
        stats.totalProjects,
        stats.totalProjectsTrend,
        stats.totalProjectsTrendDirection
      );
      
      this.components.completedTasks.updateValue(
        stats.completedTasks,
        stats.completedTasksTrend,
        stats.completedTasksTrendDirection
      );
      
      this.components.overdueTasks.updateValue(
        stats.overdueTasks,
        stats.overdueTasksTrend,
        stats.overdueTasksTrendDirection
      );
      
      this.components.productivityRate.updateValue(
        `${stats.productivityRate}%`,
        stats.productivityRateTrend,
        stats.productivityRateTrendDirection
      );
    }
  }
  
  mount() {
    // Append component elements to their containers
    const totalProjectsContainer = this.element.querySelector('#total-projects-card');
    const completedTasksContainer = this.element.querySelector('#completed-tasks-card');
    const overdueTasksContainer = this.element.querySelector('#overdue-tasks-card');
    const productivityRateContainer = this.element.querySelector('#productivity-rate-card');
    const timeLoggedContainer = this.element.querySelector('#time-logged-chart');
    
    totalProjectsContainer.appendChild(this.components.totalProjects.element);
    completedTasksContainer.appendChild(this.components.completedTasks.element);
    overdueTasksContainer.appendChild(this.components.overdueTasks.element);
    productivityRateContainer.appendChild(this.components.productivityRate.element);
    timeLoggedContainer.appendChild(this.components.timeLoggedChart.element);
    
    // Setup additional containers (Recent Projects, Task Overview, Activity Feed)
    this.renderRecentProjects();
    this.renderTaskOverview();
    this.renderRecentActivity();
    
    return this.element;
  }
  
  renderRecentProjects() {
    const container = this.element.querySelector('#recent-projects');
    // Implementation for recent projects
  }
  
  renderTaskOverview() {
    const container = this.element.querySelector('#task-overview');
    // Implementation for task overview
  }
  
  renderRecentActivity() {
    const container = this.element.querySelector('#recent-activity');
    // Implementation for recent activity
  }
}
```

## Deployment Guide
### Local Development Setup
#### Prerequisites
```bash
# Node.js 18+ required
node --version
npm --version

# Git for version control
git --version
```

#### Installation Steps
```bash
# 1. Clone repository
git clone <repository-url>
cd projectflow

# 2. Backend setup
cd backend
npm install

# 3. Environment configuration
cp .env.example .env
# Edit .env with your configuration

# 4. Database initialization
npm run migrate

# 5. Start backend server
npm run dev

# 6. Frontend setup (in new terminal)
cd ../frontend
# No npm install needed for vanilla JS
# Just serve static files through backend
```

#### Environment Configuration
```bash
# .env.example
NODE_ENV=development
PORT=3000
DB_PATH=./data/projectflow.db
SESSION_EXPIRES_DAYS=7
LOG_LEVEL=info
BACKUP_INTERVAL=24h
FRONTEND_URL=http://localhost:3000

# Security
BCRYPT_ROUNDS=12
SESSION_SECRET=your-session-secret-here

# Backup
BACKUP_ENABLED=true
BACKUP_RETENTION_DAYS=30
```

### Production Deployment
#### Option 1: Traditional Server
```bash
# 1. Server preparation
mkdir -p /opt/projectflow
cd /opt/projectflow

# 2. Clone and setup
git clone <repository-url> .
cd backend
npm ci --production

# 3. Environment configuration
cp .env.example .env
# Edit .env with production values

# 4. Database setup
npm run migrate

# 5. Process management with PM2
npm install -g pm2
pm2 start ecosystem.config.js
pm2 save
pm2 startup
```

#### Option 2: Docker Deployment
```dockerfile
# Dockerfile
FROM node:18-alpine

WORKDIR /app

# Copy package files
COPY backend/package*.json ./backend/
COPY frontend/ ./frontend/

# Install dependencies
RUN cd backend && npm ci --production

# Copy application files
COPY backend/src ./backend/src
COPY backend/server.js ./backend/
COPY backend/.env.example ./backend/.env

# Create data directory
RUN mkdir -p ./backend/data

# Expose port
EXPOSE 3000

# Start application
CMD ["node", "./backend/server.js"]
yaml# docker-compose.yml
version: '3.8'
services:
  projectflow:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - ./data:/app/backend/data
      - ./backups:/app/backend/backups
      - ./logs:/app/backend/logs
    environment:
      - NODE_ENV=production
      - PORT=3000
    restart: unless-stopped
```

## Performance Considerations
### Database Optimization
#### Query Performance
```sql
-- Ensure proper indexes for common queries
CREATE INDEX idx_tasks_user_project ON tasks(user_id, project_id);
CREATE INDEX idx_tasks_status_priority ON tasks(status, priority);
CREATE INDEX idx_projects_user_status ON projects(user_id, status);
CREATE INDEX idx_time_logs_user_date ON time_logs(user_id, logged_date);

-- Optimize frequent queries with covering indexes
CREATE INDEX idx_tasks_kanban ON tasks(project_id, status, position);
CREATE INDEX idx_tasks_dashboard ON tasks(user_id, status, due_date);
```

#### Connection Management
```javascript
// Database connection pooling for SQLite
export class Database {
  constructor() {
    this.db = null;
    this.connectionPool = [];
    this.maxConnections = 10;
  }
  
  async getConnection() {
    if (this.connectionPool.length > 0) {
      return this.connectionPool.pop();
    }
    
    return await this.createConnection();
  }
  
  async releaseConnection(connection) {
    if (this.connectionPool.length < this.maxConnections) {
      this.connectionPool.push(connection);
    } else {
      await connection.close();
    }
  }
}
```

### Frontend Performance
#### Lazy Loading Components
```javascript
// Dynamic component loading
const loadComponent = async (componentName) => {
  const module = await import(`./components/${componentName}.js`);
  return module.default;
};

// Route-based code splitting
const router = {
  '/dashboard': () => loadComponent('pages/DashboardPage'),
  '/projects': () => loadComponent('pages/ProjectsPage'),
  '/kanban': () => loadComponent('pages/KanbanPage')
};
```

#### Debounced Search
```javascript
// Debounced search implementation
export const debounce = (func, wait) => {
  let timeout;
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
};

// Usage in search component
const debouncedSearch = debounce(async (query) => {
  const results = await fetch(`/api/tasks/search?q=${query}`);
  updateSearchResults(await results.json());
}, 300);
```

## Security Guidelines
### Authentication Security
#### Password Security
```javascript
// Strong password hashing with bcrypt
import bcrypt from 'bcryptjs';

export class PasswordSecurity {
  static async hashPassword(password) {
    const saltRounds = 12;
    return await bcrypt.hash(password, saltRounds);
  }
  
  static async verifyPassword(password, hash) {
    return await bcrypt.compare(password, hash);
  }
  
  static validatePasswordStrength(password) {
    const minLength = 8;
    const hasUpperCase = /[A-Z]/.test(password);
    const hasLowerCase = /[a-z]/.test(password);
    const hasNumbers = /\d/.test(password);
    const hasNonalphas = /\W/.test(password);
    
    if (password.length < minLength) {
      return { valid: false, message: 'Password must be at least 8 characters long' };
    }
    
    if (!hasUpperCase || !hasLowerCase || !hasNumbers) {
      return { valid: false, message: 'Password must contain uppercase, lowercase, and numbers' };
    }
    
    return { valid: true };
  }
}
```

#### Session Security
```javascript
// Secure session management
export class SessionSecurity {
  static generateSecureToken() {
    return crypto.randomBytes(32).toString('hex');
  }
  
  static isValidTokenFormat(token) {
    return /^[a-f0-9]{64}$/.test(token);
  }
  
  static calculateExpiry(days = 7) {
    const expiry = new Date();
    expiry.setDate(expiry.getDate() + days);
    return expiry;
  }
  
  static isExpired(expiresAt) {
    return new Date(expiresAt) < new Date();
  }
  
  // Prevent timing attacks
  static constantTimeCompare(a, b) {
    if (a.length !== b.length) {
      return false;
    }
    
    let result = 0;
    for (let i = 0; i < a.length; i++) {
      result |= a.charCodeAt(i) ^ b.charCodeAt(i);
    }
    
    return result === 0;
  }
}
```

### Input Validation and Sanitization
#### Server-Side Validation
```javascript
// Comprehensive input validation
export class ValidationSecurity {
  static sanitizeString(input, maxLength = 1000) {
    if (typeof input !== 'string') {
      return '';
    }
    
    // Remove potentially dangerous HTML
    const sanitized = input
      .replace(/<script\b[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>/gi, '')
      .replace(/<[^>]*>/g, '')
      .trim()
      .substring(0, maxLength);
    
    return sanitized;
  }
  
  static validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
  }
  
  static validateUsername(username) {
    const usernameRegex = /^[a-zA-Z0-9_]{3,20}$/;
    return usernameRegex.test(username);
  }
  
  static validateDate(dateString) {
    const date = new Date(dateString);
    return date instanceof Date && !isNaN(date);
  }
  
  static validateHexColor(color) {
    const hexColorRegex = /^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/;
    return hexColorRegex.test(color);
  }
  
  static validateInteger(value, min = null, max = null) {
    const int = parseInt(value, 10);
    if (isNaN(int)) return false;
    if (min !== null && int < min) return false;
    if (max !== null && int > max) return false;
    return true;
  }
}
```

### Security Headers and HTTPS
#### Production Security Configuration
```javascript
// Security middleware configuration
import helmet from 'helmet';

export const securityConfig = {
  // Content Security Policy
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      styleSrc: ["'self'", "'unsafe-inline'"],
      scriptSrc: ["'self'"],
      imgSrc: ["'self'", "data:", "https:"],
      connectSrc: ["'self'"],
      fontSrc: ["'self'"],
      objectSrc: ["'none'"],
      mediaSrc: ["'self'"],
      frameSrc: ["'none'"]
    }
  },
  
  // Additional security headers
  crossOriginEmbedderPolicy: false,
  crossOriginOpenerPolicy: { policy: "cross-origin" },
  crossOriginResourcePolicy: { policy: "cross-origin" },
  dnsPrefetchControl: { allow: false },
  frameguard: { action: 'deny' },
  hidePoweredBy: true,
  hsts: {
    maxAge: 31536000,
    includeSubDomains: true,
    preload: true
  },
  ieNoOpen: true,
  noSniff: true,
  originAgentCluster: true,
  permittedCrossDomainPolicies: false,
  referrerPolicy: { policy: "no-referrer" },
  xssFilter: true
};

// Apply security middleware
app.use(helmet(securityConfig));
```

This comprehensive documentation provides everything needed to build, deploy, and maintain ProjectFlow with the exact dashboard specifications, modern UI design, robust security, and professional-grade implementation we developed together.
