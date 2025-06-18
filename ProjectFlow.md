ProjectFlow - Development Documentation
Personal Project Management Tool
Version: 1.0.0
Target: Local Hosting with Minimal/Monochrome UI

Table of Contents

Project Overview
Technical Architecture
UI/UX Design Guidelines
Database Schema
API Specification
Frontend Implementation
Backend Implementation
Development Setup
Feature Specifications
Deployment Guide
Performance Considerations
Security Guidelines


Project Overview
Project Description
ProjectFlow is a personal project management tool designed for local hosting. It provides comprehensive project tracking, task management, Kanban boards, analytics, and reporting capabilities with a focus on individual productivity.
Key Features

Dashboard: Overview with statistics and recent activity
Kanban Board: Visual task management with drag-and-drop
Project Management: Project creation, tracking, and progress monitoring
Task Management: Task creation, assignment, prioritization
Analytics: Productivity insights and performance metrics
Calendar: Deadline tracking and event management
Reports: Custom report generation and export
Settings: User preferences and configuration

Design Philosophy

Minimal: Clean, uncluttered interface focusing on content
Monochrome: Primarily grayscale with selective accent colors
Local-First: Designed for local hosting and offline capability
Performance: Fast, lightweight, and responsive


Technical Architecture
Stack Recommendation
Backend
- Node.js with Express.js
- SQLite for local database
- JWT for authentication (if needed)
- Multer for file uploads
- date-fns for date handling
Frontend
- Vanilla JavaScript (ES6+) or React.js
- CSS3 with CSS Grid and Flexbox
- HTML5 Drag and Drop API
- Chart.js for analytics
- Local Storage for settings
Development Tools
- Vite or Webpack for bundling
- ESLint for code quality
- Prettier for formatting
- Jest for testing
Architecture Patterns
MVC Structure
src/
├── models/           # Data models and database interactions
├── views/            # Frontend components and pages
├── controllers/      # Business logic and API handlers
├── routes/           # API route definitions
├── middleware/       # Custom middleware
├── utils/            # Helper functions
├── public/           # Static assets
└── config/           # Configuration files
Database-First Approach

SQLite for simplicity and portability
Migration system for schema updates
Data validation at model level
Automatic backups


UI/UX Design Guidelines
Color Palette (Monochrome + Accent)
Primary Colors
css:root {
  /* Monochrome Base */
  --color-white: #ffffff;
  --color-gray-50: #f9fafb;
  --color-gray-100: #f3f4f6;
  --color-gray-200: #e5e7eb;
  --color-gray-300: #d1d5db;
  --color-gray-400: #9ca3af;
  --color-gray-500: #6b7280;
  --color-gray-600: #4b5563;
  --color-gray-700: #374151;
  --color-gray-800: #1f2937;
  --color-gray-900: #111827;
  --color-black: #000000;
  
  /* Accent Colors (Selective Use) */
  --color-accent-primary: #3b82f6;    /* Blue for actions */
  --color-accent-success: #10b981;    /* Green for success */
  --color-accent-warning: #f59e0b;    /* Yellow for warnings */
  --color-accent-danger: #ef4444;     /* Red for errors */
  
  /* Status Colors (Muted) */
  --color-status-active: #6b7280;
  --color-status-completed: #374151;
  --color-status-pending: #9ca3af;
  --color-status-overdue: #4b5563;
}
Typography
css:root {
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
  --text-3xl: 1.875rem;   /* 30px */
  --text-4xl: 2.25rem;    /* 36px */
  
  /* Font Weights */
  --font-normal: 400;
  --font-medium: 500;
  --font-semibold: 600;
  --font-bold: 700;
}
Spacing System
css:root {
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
Component Design Principles
Minimalism Guidelines

White Space: Generous use of white space for visual breathing room
Typography Hierarchy: Clear hierarchy using font weights and sizes
Reduced Visual Elements: Minimal use of borders, shadows, and decorative elements
Functional Color: Color used primarily for functional purposes (status, actions)
Clean Lines: Straight lines, minimal curves, geometric shapes

Interaction Patterns

Subtle Hover Effects: Light background changes or opacity shifts
Micro-animations: Short, purposeful transitions (200-300ms)
Focus States: Clear keyboard navigation indicators
Loading States: Simple loading indicators without spinners
Error Handling: Inline, contextual error messages


Database Schema
Tables Structure
Users Table
sqlCREATE TABLE users (
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
Projects Table
sqlCREATE TABLE projects (
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
Tasks Table
sqlCREATE TABLE tasks (
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
Task Comments Table
sqlCREATE TABLE task_comments (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  task_id INTEGER NOT NULL,
  user_id INTEGER NOT NULL,
  content TEXT NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (task_id) REFERENCES tasks(id) ON DELETE CASCADE,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
Time Logs Table
sqlCREATE TABLE time_logs (
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
Milestones Table
sqlCREATE TABLE milestones (
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
Reports Table
sqlCREATE TABLE reports (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  name VARCHAR(200) NOT NULL,
  type VARCHAR(50) NOT NULL, -- weekly, project_summary, time_tracking, etc.
  parameters TEXT, -- JSON string of report parameters
  generated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  file_path VARCHAR(500),
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
Database Indexes
sql-- Performance indexes
CREATE INDEX idx_tasks_project_id ON tasks(project_id);
CREATE INDEX idx_tasks_user_id ON tasks(user_id);
CREATE INDEX idx_tasks_status ON tasks(status);
CREATE INDEX idx_tasks_due_date ON tasks(due_date);
CREATE INDEX idx_projects_user_id ON projects(user_id);
CREATE INDEX idx_projects_status ON projects(status);
CREATE INDEX idx_time_logs_task_id ON time_logs(task_id);
CREATE INDEX idx_time_logs_logged_date ON time_logs(logged_date);

API Specification
Authentication Endpoints
POST /api/auth/login
javascript// Request
{
  "username": "string",
  "password": "string"
}

// Response
{
  "success": true,
  "token": "jwt_token",
  "user": {
    "id": 1,
    "username": "string",
    "email": "string",
    "full_name": "string"
  }
}
Project Endpoints
GET /api/projects
javascript// Query Parameters
?status=active&limit=10&offset=0

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
      "start_date": "2025-01-01",
      "due_date": "2025-03-01",
      "completion_percentage": 75,
      "task_count": 12,
      "completed_tasks": 9,
      "created_at": "2025-01-01T00:00:00Z"
    }
  ],
  "total": 24,
  "page": 1,
  "limit": 10
}
POST /api/projects
javascript// Request
{
  "name": "New Project",
  "description": "Project description",
  "priority": "medium",
  "start_date": "2025-01-01",
  "due_date": "2025-06-01",
  "color": "#667eea"
}

// Response
{
  "success": true,
  "data": {
    "id": 5,
    "name": "New Project",
    // ... other fields
  }
}
PUT /api/projects/:id
javascript// Request
{
  "name": "Updated Project Name",
  "status": "completed",
  "completion_percentage": 100
}

// Response
{
  "success": true,
  "data": {
    "id": 1,
    // ... updated fields
  }
}
Task Endpoints
GET /api/tasks
javascript// Query Parameters
?project_id=1&status=todo&priority=high&due_date=2025-01-15

// Response
{
  "success": true,
  "data": [
    {
      "id": 1,
      "title": "Review API documentation",
      "description": "Review and update API documentation",
      "status": "todo",
      "priority": "high",
      "due_date": "2025-01-15T23:59:59Z",
      "project": {
        "id": 1,
        "name": "Website Redesign"
      },
      "estimated_hours": 4,
      "actual_hours": null,
      "position": 0,
      "created_at": "2025-01-01T00:00:00Z"
    }
  ]
}
POST /api/tasks
javascript// Request
{
  "project_id": 1,
  "title": "New Task",
  "description": "Task description",
  "status": "todo",
  "priority": "medium",
  "due_date": "2025-01-20T23:59:59Z",
  "estimated_hours": 2
}
PATCH /api/tasks/:id/status
javascript// Request
{
  "status": "in_progress",
  "position": 1
}
Analytics Endpoints
GET /api/analytics/dashboard
javascript// Query Parameters
?period=30d&project_id=1

// Response
{
  "success": true,
  "data": {
    "overview": {
      "total_projects": 24,
      "active_projects": 8,
      "completed_tasks": 147,
      "overdue_tasks": 6,
      "productivity_rate": 85
    },
    "project_progress": [
      {
        "project_id": 1,
        "name": "Website Redesign",
        "completion_percentage": 75,
        "task_count": 12,
        "completed_count": 9
      }
    ],
    "task_distribution": {
      "todo": 15,
      "in_progress": 8,
      "review": 4,
      "done": 147
    },
    "productivity_trends": [
      {
        "date": "2025-01-01",
        "tasks_completed": 5,
        "hours_logged": 6.5
      }
    ]
  }
}
GET /api/analytics/time-tracking
javascript// Response
{
  "success": true,
  "data": {
    "daily_average": 6.2,
    "weekly_total": 43.4,
    "monthly_total": 186.8,
    "by_project": [
      {
        "project_id": 1,
        "project_name": "Website Redesign",
        "total_hours": 45.5,
        "percentage": 24.3
      }
    ]
  }
}

Frontend Implementation
Component Structure
Core Components
src/components/
├── common/
│   ├── Button.js
│   ├── Input.js
│   ├── Modal.js
│   ├── Dropdown.js
│   ├── DatePicker.js
│   └── ProgressBar.js
├── layout/
│   ├── Sidebar.js
│   ├── Header.js
│   └── Layout.js
├── dashboard/
│   ├── StatCard.js
│   ├── ProjectList.js
│   ├── ActivityFeed.js
│   └── TaskSummary.js
├── kanban/
│   ├── KanbanBoard.js
│   ├── KanbanColumn.js
│   ├── KanbanCard.js
│   └── TaskModal.js
├── projects/
│   ├── ProjectTable.js
│   ├── ProjectForm.js
│   └── ProjectCard.js
├── tasks/
│   ├── TaskTable.js
│   ├── TaskForm.js
│   ├── TaskFilters.js
│   └── TaskDetail.js
└── analytics/
    ├── Chart.js
    ├── MetricCard.js
    └── ReportGenerator.js
Example Component: Button.js
javascript// components/common/Button.js
export class Button {
  constructor(config) {
    this.config = {
      variant: 'primary', // primary, secondary, danger
      size: 'medium',     // small, medium, large
      disabled: false,
      loading: false,
      onClick: () => {},
      ...config
    };
    
    this.element = this.createElement();
  }
  
  createElement() {
    const button = document.createElement('button');
    button.className = this.getClasses();
    button.textContent = this.config.text;
    button.disabled = this.config.disabled || this.config.loading;
    
    if (this.config.icon) {
      const icon = document.createElement('span');
      icon.textContent = this.config.icon;
      icon.className = 'btn-icon';
      button.prepend(icon);
    }
    
    button.addEventListener('click', this.config.onClick);
    
    return button;
  }
  
  getClasses() {
    const base = 'btn';
    const variant = `btn-${this.config.variant}`;
    const size = `btn-${this.config.size}`;
    const loading = this.config.loading ? 'btn-loading' : '';
    
    return [base, variant, size, loading].filter(Boolean).join(' ');
  }
  
  setLoading(isLoading) {
    this.config.loading = isLoading;
    this.element.disabled = isLoading || this.config.disabled;
    this.element.classList.toggle('btn-loading', isLoading);
  }
  
  render(parent) {
    parent.appendChild(this.element);
    return this;
  }
}
Example Component: KanbanBoard.js
javascript// components/kanban/KanbanBoard.js
export class KanbanBoard {
  constructor(config) {
    this.config = config;
    this.columns = [
      { id: 'todo', title: 'To Do', icon: '📝' },
      { id: 'in_progress', title: 'In Progress', icon: '🔄' },
      { id: 'review', title: 'Review', icon: '👀' },
      { id: 'done', title: 'Done', icon: '✅' }
    ];
    
    this.tasks = [];
    this.element = this.createElement();
    this.setupDragAndDrop();
  }
  
  createElement() {
    const container = document.createElement('div');
    container.className = 'kanban-board';
    
    this.columns.forEach(column => {
      const columnElement = this.createColumn(column);
      container.appendChild(columnElement);
    });
    
    return container;
  }
  
  createColumn(column) {
    const columnEl = document.createElement('div');
    columnEl.className = 'kanban-column';
    columnEl.dataset.status = column.id;
    
    columnEl.innerHTML = `
      <div class="kanban-header">
        <div class="kanban-title">
          <span class="kanban-icon">${column.icon}</span>
          ${column.title}
        </div>
        <div class="kanban-count">0</div>
      </div>
      <div class="kanban-cards" data-status="${column.id}"></div>
      <button class="add-card-btn" data-column="${column.id}">
        + Add a task
      </button>
    `;
    
    return columnEl;
  }
  
  setupDragAndDrop() {
    this.element.addEventListener('dragstart', this.handleDragStart.bind(this));
    this.element.addEventListener('dragover', this.handleDragOver.bind(this));
    this.element.addEventListener('drop', this.handleDrop.bind(this));
    this.element.addEventListener('click', this.handleAddTask.bind(this));
  }
  
  async handleDrop(e) {
    e.preventDefault();
    
    const taskId = e.dataTransfer.getData('text/plain');
    const newStatus = e.target.closest('.kanban-column')?.dataset.status;
    
    if (taskId && newStatus) {
      await this.updateTaskStatus(taskId, newStatus);
      this.refreshTasks();
    }
  }
  
  async updateTaskStatus(taskId, status) {
    try {
      const response = await fetch(`/api/tasks/${taskId}/status`, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ status })
      });
      
      if (!response.ok) throw new Error('Failed to update task');
      
      return await response.json();
    } catch (error) {
      console.error('Error updating task:', error);
      // Show error notification
    }
  }
  
  async loadTasks(projectId = null) {
    try {
      const url = projectId 
        ? `/api/tasks?project_id=${projectId}` 
        : '/api/tasks';
        
      const response = await fetch(url);
      const result = await response.json();
      
      if (result.success) {
        this.tasks = result.data;
        this.renderTasks();
        this.updateCounts();
      }
    } catch (error) {
      console.error('Error loading tasks:', error);
    }
  }
  
  renderTasks() {
    // Clear existing tasks
    this.element.querySelectorAll('.kanban-cards').forEach(container => {
      container.innerHTML = '';
    });
    
    // Render tasks in appropriate columns
    this.tasks.forEach(task => {
      const taskElement = this.createTaskCard(task);
      const column = this.element.querySelector(`[data-status="${task.status}"]`);
      column.appendChild(taskElement);
    });
  }
  
  createTaskCard(task) {
    const card = document.createElement('div');
    card.className = 'kanban-card';
    card.draggable = true;
    card.dataset.taskId = task.id;
    
    const priorityClass = `priority-${task.priority}`;
    const dueDate = task.due_date 
      ? new Date(task.due_date).toLocaleDateString() 
      : 'No due date';
    
    card.innerHTML = `
      <div class="kanban-card-title">${task.title}</div>
      <div class="kanban-card-project">${task.project.name}</div>
      <div class="kanban-card-meta">
        <div class="kanban-card-priority ${priorityClass}">${task.priority}</div>
        <div class="kanban-card-due">Due: ${dueDate}</div>
      </div>
    `;
    
    return card;
  }
  
  updateCounts() {
    this.columns.forEach(column => {
      const count = this.tasks.filter(task => task.status === column.id).length;
      const countEl = this.element.querySelector(`[data-status="${column.id}"] .kanban-count`);
      countEl.textContent = count;
    });
  }
}
State Management
Simple State Manager
javascript// utils/StateManager.js
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
  
  dispatch(action) {
    switch (action.type) {
      case 'SET_CURRENT_PROJECT':
        this.setState('currentProject', action.payload);
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
      default:
        console.warn('Unknown action type:', action.type);
    }
  }
}

// Global state instance
export const appState = new StateManager();
CSS Framework (Minimal Design)
Base Styles
css/* styles/base.css */

/* Reset and Base */
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  font-size: 16px;
  scroll-behavior: smooth;
}

body {
  font-family: var(--font-primary);
  font-size: var(--text-base);
  font-weight: var(--font-normal);
  line-height: 1.6;
  color: var(--color-gray-800);
  background-color: var(--color-gray-50);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* Typography */
h1, h2, h3, h4, h5, h6 {
  font-weight: var(--font-semibold);
  line-height: 1.3;
  color: var(--color-gray-900);
}

h1 { font-size: var(--text-4xl); }
h2 { font-size: var(--text-3xl); }
h3 { font-size: var(--text-2xl); }
h4 { font-size: var(--text-xl); }
h5 { font-size: var(--text-lg); }
h6 { font-size: var(--text-base); }

p {
  margin-bottom: var(--space-4);
}

/* Links */
a {
  color: var(--color-accent-primary);
  text-decoration: none;
  transition: color 0.2s ease;
}

a:hover {
  color: var(--color-gray-700);
}

/* Focus States */
:focus-visible {
  outline: 2px solid var(--color-accent-primary);
  outline-offset: 2px;
}

/* Selection */
::selection {
  background-color: var(--color-gray-200);
  color: var(--color-gray-900);
}
Component Styles
css/* styles/components.css */

/* Buttons */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  padding: var(--space-3) var(--space-4);
  font-size: var(--text-sm);
  font-weight: var(--font-medium);
  line-height: 1;
  border: 1px solid transparent;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.2s ease;
  text-decoration: none;
  white-space: nowrap;
}

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.btn-primary {
  background-color: var(--color-gray-900);
  color: var(--color-white);
  border-color: var(--color-gray-900);
}

.btn-primary:hover:not(:disabled) {
  background-color: var(--color-gray-800);
  border-color: var(--color-gray-800);
}

.btn-secondary {
  background-color: var(--color-white);
  color: var(--color-gray-700);
  border-color: var(--color-gray-300);
}

.btn-secondary:hover:not(:disabled) {
  background-color: var(--color-gray-50);
  border-color: var(--color-gray-400);
}

.btn-danger {
  background-color: var(--color-accent-danger);
  color: var(--color-white);
  border-color: var(--color-accent-danger);
}

.btn-small {
  padding: var(--space-2) var(--space-3);
  font-size: var(--text-xs);
}

.btn-large {
  padding: var(--space-4) var(--space-6);
  font-size: var(--text-base);
}

/* Forms */
.form-group {
  margin-bottom: var(--space-5);
}

.form-label {
  display: block;
  margin-bottom: var(--space-2);
  font-size: var(--text-sm);
  font-weight: var(--font-medium);
  color: var(--color-gray-700);
}

.form-input,
.form-select,
.form-textarea {
  width: 100%;
  padding: var(--space-3);
  font-size: var(--text-sm);
  color: var(--color-gray-800);
  background-color: var(--color-white);
  border: 1px solid var(--color-gray-300);
  border-radius: 4px;
  transition: border-color 0.2s ease;
}

.form-input:focus,
.form-select:focus,
.form-textarea:focus {
  outline: none;
  border-color: var(--color-gray-500);
}

.form-textarea {
  min-height: 100px;
  resize: vertical;
}

/* Cards */
.card {
  background-color: var(--color-white);
  border: 1px solid var(--color-gray-200);
  border-radius: 8px;
  padding: var(--space-6);
  transition: box-shadow 0.2s ease;
}

.card:hover {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

.card-header {
  margin-bottom: var(--space-4);
  padding-bottom: var(--space-4);
  border-bottom: 1px solid var(--color-gray-200);
}

.card-title {
  font-size: var(--text-lg);
  font-weight: var(--font-semibold);
  color: var(--color-gray-900);
}

/* Tables */
.table {
  width: 100%;
  border-collapse: collapse;
  background-color: var(--color-white);
  border: 1px solid var(--color-gray-200);
  border-radius: 8px;
  overflow: hidden;
}

.table th,
.table td {
  padding: var(--space-3) var(--space-4);
  text-align: left;
  border-bottom: 1px solid var(--color-gray-200);
}

.table th {
  background-color: var(--color-gray-50);
  font-weight: var(--font-medium);
  font-size: var(--text-sm);
  color: var(--color-gray-700);
}

.table tbody tr:hover {
  background-color: var(--color-gray-50);
}

.table tbody tr:last-child td {
  border-bottom: none;
}

/* Status Indicators */
.status {
  display: inline-flex;
  align-items: center;
  gap: var(--space-1);
  padding: var(--space-1) var(--space-2);
  font-size: var(--text-xs);
  font-weight: var(--font-medium);
  text-transform: uppercase;
  letter-spacing: 0.025em;
  border-radius: 12px;
}

.status-active {
  background-color: var(--color-gray-100);
  color: var(--color-gray-700);
}

.status-completed {
  background-color: var(--color-gray-200);
  color: var(--color-gray-800);
}

.status-pending {
  background-color: var(--color-gray-100);
  color: var(--color-gray-600);
}

/* Priority Indicators */
.priority {
  display: inline-flex;
  align-items: center;
  padding: var(--space-1) var(--space-2);
  font-size: var(--text-xs);
  font-weight: var(--font-medium);
  text-transform: uppercase;
  border-radius: 4px;
}

.priority-high {
  background-color: var(--color-gray-200);
  color: var(--color-gray-800);
}

.priority-medium {
  background-color: var(--color-gray-100);
  color: var(--color-gray-700);
}

.priority-low {
  background-color: var(--color-gray-50);
  color: var(--color-gray-600);
}

/* Progress Bars */
.progress {
  width: 100%;
  height: 8px;
  background-color: var(--color-gray-200);
  border-radius: 4px;
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  background-color: var(--color-gray-600);
  transition: width 0.3s ease;
}

/* Kanban Specific */
.kanban-board {
  display: flex;
  gap: var(--space-6);
  padding: var(--space-6);
  overflow-x: auto;
  min-height: calc(100vh - 200px);
}

.kanban-column {
  min-width: 300px;
  background-color: var(--color-gray-100);
  border-radius: 8px;
  padding: var(--space-4);
  display: flex;
  flex-direction: column;
}

.kanban-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--space-4);
  padding-bottom: var(--space-3);
  border-bottom: 1px solid var(--color-gray-200);
}

.kanban-title {
  font-weight: var(--font-semibold);
  color: var(--color-gray-800);
}

.kanban-count {
  background-color: var(--color-gray-200);
  color: var(--color-gray-700);
  padding: var(--space-1) var(--space-2);
  border-radius: 12px;
  font-size: var(--text-xs);
  font-weight: var(--font-medium);
}

.kanban-cards {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
  min-height: 200px;
}

.kanban-card {
  background-color: var(--color-white);
  border: 1px solid var(--color-gray-200);
  border-radius: 6px;
  padding: var(--space-4);
  cursor: grab;
  transition: all 0.2s ease;
}

.kanban-card:hover {
  border-color: var(--color-gray-300);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.kanban-card.dragging {
  opacity: 0.6;
  transform: rotate(2deg);
}

.kanban-card-title {
  font-weight: var(--font-medium);
  color: var(--color-gray-800);
  margin-bottom: var(--space-2);
}

.kanban-card-project {
  font-size: var(--text-xs);
  color: var(--color-gray-500);
  margin-bottom: var(--space-3);
}

.kanban-card-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.kanban-card-due {
  font-size: var(--text-xs);
  color: var(--color-gray-500);
}

.add-card-btn {
  margin-top: var(--space-3);
  padding: var(--space-3);
  background-color: transparent;
  border: 2px dashed var(--color-gray-300);
  border-radius: 6px;
  color: var(--color-gray-500);
  font-size: var(--text-sm);
  cursor: pointer;
  transition: all 0.2s ease;
}

.add-card-btn:hover {
  border-color: var(--color-gray-400);
  color: var(--color-gray-600);
  background-color: var(--color-gray-50);
}

Backend Implementation
Server Setup (Node.js/Express)
Main Server File
javascript// server.js
import express from 'express';
import cors from 'cors';
import path from 'path';
import { fileURLToPath } from 'url';
import { Database } from './src/config/database.js';
import { authRoutes } from './src/routes/auth.js';
import { projectRoutes } from './src/routes/projects.js';
import { taskRoutes } from './src/routes/tasks.js';
import { analyticsRoutes } from './src/routes/analytics.js';
import { reportRoutes } from './src/routes/reports.js';
import { errorHandler } from './src/middleware/errorHandler.js';
import { authMiddleware } from './src/middleware/auth.js';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

const app = express();
const PORT = process.env.PORT || 3000;

// Initialize database
const db = new Database();
await db.initialize();

// Middleware
app.use(cors());
app.use(express.json());
app.use(express.static(path.join(__dirname, 'public')));

// Routes
app.use('/api/auth', authRoutes);
app.use('/api/projects', authMiddleware, projectRoutes);
app.use('/api/tasks', authMiddleware, taskRoutes);
app.use('/api/analytics', authMiddleware, analyticsRoutes);
app.use('/api/reports', authMiddleware, reportRoutes);

// Error handling
app.use(errorHandler);

// Serve frontend for SPA
app.get('*', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

app.listen(PORT, 'localhost', () => {
  console.log(`ProjectFlow server running on http://localhost:${PORT}`);
});
Database Configuration
javascript// src/config/database.js
import sqlite3 from 'sqlite3';
import { open } from 'sqlite';
import fs from 'fs/promises';
import path from 'path';

export class Database {
  constructor() {
    this.db = null;
    this.dbPath = path.join(process.cwd(), 'data', 'projectflow.db');
  }
  
  async initialize() {
    // Ensure data directory exists
    await fs.mkdir(path.dirname(this.dbPath), { recursive: true });
    
    // Open database connection
    this.db = await open({
      filename: this.dbPath,
      driver: sqlite3.Database
    });
    
    // Enable foreign keys
    await this.db.exec('PRAGMA foreign_keys = ON');
    
    // Run migrations
    await this.runMigrations();
    
    console.log('Database initialized successfully');
  }
  
  async runMigrations() {
    const migrationsPath = path.join(process.cwd(), 'src', 'migrations');
    const migrationFiles = await fs.readdir(migrationsPath);
    
    // Create migrations table if it doesn't exist
    await this.db.exec(`
      CREATE TABLE IF NOT EXISTS migrations (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        filename VARCHAR(255) UNIQUE NOT NULL,
        executed_at DATETIME DEFAULT CURRENT_TIMESTAMP
      )
    `);
    
    // Get executed migrations
    const executed = await this.db.all('SELECT filename FROM migrations');
    const executedFiles = executed.map(row => row.filename);
    
    // Run pending migrations
    for (const file of migrationFiles.sort()) {
      if (!executedFiles.includes(file) && file.endsWith('.sql')) {
        const migrationSQL = await fs.readFile(
          path.join(migrationsPath, file), 
          'utf8'
        );
        
        await this.db.exec(migrationSQL);
        await this.db.run(
          'INSERT INTO migrations (filename) VALUES (?)', 
          [file]
        );
        
        console.log(`Migration executed: ${file}`);
      }
    }
  }
  
  getDb() {
    return this.db;
  }
  
  async close() {
    if (this.db) {
      await this.db.close();
    }
  }
}
Project Controller
javascript// src/controllers/projectController.js
import { ProjectModel } from '../models/Project.js';
import { TaskModel } from '../models/Task.js';

export class ProjectController {
  constructor() {
    this.projectModel = new ProjectModel();
    this.taskModel = new TaskModel();
  }
  
  async getAll(req, res, next) {
    try {
      const { status, limit = 10, offset = 0 } = req.query;
      const userId = req.user.id;
      
      const filters = { user_id: userId };
      if (status) filters.status = status;
      
      const projects = await this.projectModel.findAll(filters, {
        limit: parseInt(limit),
        offset: parseInt(offset)
      });
      
      // Add task counts to each project
      const projectsWithCounts = await Promise.all(
        projects.map(async (project) => {
          const taskCounts = await this.taskModel.getCountsByStatus(project.id);
          return {
            ...project,
            task_count: taskCounts.total,
            completed_tasks: taskCounts.done || 0
          };
        })
      );
      
      const total = await this.projectModel.count(filters);
      
      res.json({
        success: true,
        data: projectsWithCounts,
        total,
        page: Math.floor(offset / limit) + 1,
        limit: parseInt(limit)
      });
    } catch (error) {
      next(error);
    }
  }
  
  async getById(req, res, next) {
    try {
      const { id } = req.params;
      const userId = req.user.id;
      
      const project = await this.projectModel.findById(id, userId);
      
      if (!project) {
        return res.status(404).json({
          success: false,
          message: 'Project not found'
        });
      }
      
      // Add detailed task information
      const tasks = await this.taskModel.findByProjectId(id);
      const taskCounts = await this.taskModel.getCountsByStatus(id);
      
      res.json({
        success: true,
        data: {
          ...project,
          tasks,
          task_counts: taskCounts
        }
      });
    } catch (error) {
      next(error);
    }
  }
  
  async create(req, res, next) {
    try {
      const projectData = {
        ...req.body,
        user_id: req.user.id
      };
      
      const validation = this.validateProjectData(projectData);
      if (!validation.isValid) {
        return res.status(400).json({
          success: false,
          message: 'Validation failed',
          errors: validation.errors
        });
      }
      
      const project = await this.projectModel.create(projectData);
      
      res.status(201).json({
        success: true,
        data: project
      });
    } catch (error) {
      next(error);
    }
  }
  
  async update(req, res, next) {
    try {
      const { id } = req.params;
      const userId = req.user.id;
      
      const existing = await this.projectModel.findById(id, userId);
      if (!existing) {
        return res.status(404).json({
          success: false,
          message: 'Project not found'
        });
      }
      
      const updateData = {
        ...req.body,
        updated_at: new Date().toISOString()
      };
      
      const project = await this.projectModel.update(id, updateData);
      
      res.json({
        success: true,
        data: project
      });
    } catch (error) {
      next(error);
    }
  }
  
  async delete(req, res, next) {
    try {
      const { id } = req.params;
      const userId = req.user.id;
      
      const existing = await this.projectModel.findById(id, userId);
      if (!existing) {
        return res.status(404).json({
          success: false,
          message: 'Project not found'
        });
      }
      
      await this.projectModel.delete(id);
      
      res.json({
        success: true,
        message: 'Project deleted successfully'
      });
    } catch (error) {
      next(error);
    }
  }
  
  validateProjectData(data) {
    const errors = [];
    
    if (!data.name || data.name.trim().length === 0) {
      errors.push('Project name is required');
    }
    
    if (data.name && data.name.length > 200) {
      errors.push('Project name must be less than 200 characters');
    }
    
    if (data.priority && !['low', 'medium', 'high'].includes(data.priority)) {
      errors.push('Priority must be low, medium, or high');
    }
    
    if (data.status && !['active', 'planning', 'review', 'completed', 'archived'].includes(data.status)) {
      errors.push('Status must be one of: active, planning, review, completed, archived');
    }
    
    if (data.due_date && isNaN(Date.parse(data.due_date))) {
      errors.push('Due date must be a valid date');
    }
    
    return {
      isValid: errors.length === 0,
      errors
    };
  }
}
Task Model
javascript// src/models/Task.js
import { BaseModel } from './BaseModel.js';

export class TaskModel extends BaseModel {
  constructor() {
    super('tasks');
  }
  
  async findByProjectId(projectId) {
    const query = `
      SELECT 
        t.*,
        p.name as project_name,
        p.color as project_color
      FROM tasks t
      JOIN projects p ON t.project_id = p.id
      WHERE t.project_id = ?
      ORDER BY t.position ASC, t.created_at DESC
    `;
    
    return await this.db.all(query, [projectId]);
  }
  
  async findByStatus(userId, status) {
    const query = `
      SELECT 
        t.*,
        p.name as project_name,
        p.color as project_color
      FROM tasks t
      JOIN projects p ON t.project_id = p.id
      WHERE t.user_id = ? AND t.status = ?
      ORDER BY t.due_date ASC, t.priority DESC
    `;
    
    return await this.db.all(query, [userId, status]);
  }
  
  async getCountsByStatus(projectId) {
    const query = `
      SELECT 
        status,
        COUNT(*) as count
      FROM tasks 
      WHERE project_id = ?
      GROUP BY status
    `;
    
    const results = await this.db.all(query, [projectId]);
    
    const counts = {
      total: 0,
      todo: 0,
      in_progress: 0,
      review: 0,
      done: 0
    };
    
    results.forEach(row => {
      counts[row.status] = row.count;
      counts.total += row.count;
    });
    
    return counts;
  }
  
  async updateStatus(id, status, position = null) {
    const updateData = {
      status,
      updated_at: new Date().toISOString()
    };
    
    if (position !== null) {
      updateData.position = position;
    }
    
    if (status === 'done' && !updateData.completed_at) {
      updateData.completed_at = new Date().toISOString();
    }
    
    return await this.update(id, updateData);
  }
  
  async getOverdueTasks(userId) {
    const query = `
      SELECT 
        t.*,
        p.name as project_name
      FROM tasks t
      JOIN projects p ON t.project_id = p.id
      WHERE t.user_id = ? 
        AND t.status != 'done'
        AND t.due_date < datetime('now')
      ORDER BY t.due_date ASC
    `;
    
    return await this.db.all(query, [userId]);
  }
  
  async getDueSoon(userId, days = 7) {
    const query = `
      SELECT 
        t.*,
        p.name as project_name
      FROM tasks t
      JOIN projects p ON t.project_id = p.id
      WHERE t.user_id = ? 
        AND t.status != 'done'
        AND t.due_date BETWEEN datetime('now') 
        AND datetime('now', '+${days} days')
      ORDER BY t.due_date ASC
    `;
    
    return await this.db.all(query, [userId]);
  }
  
  async getCompletionStats(userId, startDate, endDate) {
    const query = `
      SELECT 
        DATE(completed_at) as date,
        COUNT(*) as completed_count
      FROM tasks 
      WHERE user_id = ? 
        AND status = 'done'
        AND completed_at BETWEEN ? AND ?
      GROUP BY DATE(completed_at)
      ORDER BY date ASC
    `;
    
    return await this.db.all(query, [userId, startDate, endDate]);
  }
}

Development Setup
Project Structure
project-flow/
├── package.json
├── server.js
├── .env.example
├── .gitignore
├── README.md
├── src/
│   ├── config/
│   │   ├── database.js
│   │   └── app.js
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── projectController.js
│   │   ├── taskController.js
│   │   └── analyticsController.js
│   ├── models/
│   │   ├── BaseModel.js
│   │   ├── User.js
│   │   ├── Project.js
│   │   ├── Task.js
│   │   └── TimeLog.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── projects.js
│   │   ├── tasks.js
│   │   └── analytics.js
│   ├── middleware/
│   │   ├── auth.js
│   │   ├── validation.js
│   │   └── errorHandler.js
│   ├── utils/
│   │   ├── logger.js
│   │   ├── validation.js
│   │   └── helpers.js
│   └── migrations/
│       ├── 001_initial_schema.sql
│       ├── 002_add_time_logs.sql
│       └── 003_add_milestones.sql
├── public/
│   ├── index.html
│   ├── css/
│   │   ├── variables.css
│   │   ├── base.css
│   │   ├── components.css
│   │   └── pages.css
│   ├── js/
│   │   ├── app.js
│   │   ├── utils/
│   │   ├── components/
│   │   └── pages/
│   └── assets/
│       ├── icons/
│       └── images/
├── data/
│   └── .gitkeep
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
└── docs/
    ├── api.md
    ├── deployment.md
    └── contributing.md
Package.json
json{
  "name": "project-flow",
  "version": "1.0.0",
  "description": "Personal project management tool",
  "type": "module",
  "main": "server.js",
  "scripts": {
    "dev": "nodemon server.js",
    "start": "node server.js",
    "build": "vite build",
    "test": "jest",
    "test:watch": "jest --watch",
    "lint": "eslint src/",
    "format": "prettier --write src/",
    "migrate": "node src/scripts/migrate.js",
    "seed": "node src/scripts/seed.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "sqlite3": "^5.1.6",
    "sqlite": "^4.2.1",
    "bcryptjs": "^2.4.3",
    "jsonwebtoken": "^9.0.2",
    "cors": "^2.8.5",
    "helmet": "^7.0.0",
    "rate-limiter-flexible": "^2.4.2",
    "multer": "^1.4.5",
    "date-fns": "^2.30.0",
    "uuid": "^9.0.0"
  },
  "devDependencies": {
    "nodemon": "^3.0.1",
    "vite": "^4.4.9",
    "jest": "^29.6.4",
    "supertest": "^6.3.3",
    "eslint": "^8.47.0",
    "prettier": "^3.0.2"
  },
  "engines": {
    "node": ">=18.0.0"
  }
}
Environment Configuration
bash# .env.example
NODE_ENV=development
PORT=3000
DB_PATH=./data/projectflow.db
JWT_SECRET=your_super_secret_jwt_key_here
JWT_EXPIRES_IN=7d
LOG_LEVEL=info
BACKUP_INTERVAL=24h
Installation Steps

Clone and Setup

bashmkdir project-flow
cd project-flow
npm init -y
npm install express sqlite3 sqlite bcryptjs jsonwebtoken cors helmet
npm install -D nodemon vite jest eslint prettier

Database Setup

bashmkdir -p data src/migrations
touch src/migrations/001_initial_schema.sql

Create Initial Migration

sql-- src/migrations/001_initial_schema.sql
-- Initial database schema for ProjectFlow

-- Users table
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  username VARCHAR(50) UNIQUE NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  full_name VARCHAR(100),
  timezone VARCHAR(50) DEFAULT 'UTC',
  preferences TEXT,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- Projects table
CREATE TABLE projects (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL,
  name VARCHAR(200) NOT NULL,
  description TEXT,
  status VARCHAR(20) DEFAULT 'active',
  priority VARCHAR(10) DEFAULT 'medium',
  start_date DATE,
  due_date DATE,
  completion_percentage INTEGER DEFAULT 0,
  color VARCHAR(7),
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

-- Tasks table
CREATE TABLE tasks (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  project_id INTEGER NOT NULL,
  user_id INTEGER NOT NULL,
  title VARCHAR(200) NOT NULL,
  description TEXT,
  status VARCHAR(20) DEFAULT 'todo',
  priority VARCHAR(10) DEFAULT 'medium',
  due_date DATETIME,
  estimated_hours DECIMAL(5,2),
  actual_hours DECIMAL(5,2),
  tags TEXT,
  position INTEGER DEFAULT 0,
  completed_at DATETIME,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (project_id) REFERENCES projects(id) ON DELETE CASCADE,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

-- Create indexes for performance
CREATE INDEX idx_tasks_project_id ON tasks(project_id);
CREATE INDEX idx_tasks_user_id ON tasks(user_id);
CREATE INDEX idx_tasks_status ON tasks(status);
CREATE INDEX idx_tasks_due_date ON tasks(due_date);
CREATE INDEX idx_projects_user_id ON projects(user_id);
CREATE INDEX idx_projects_status ON projects(status);

Start Development

bashnpm run dev

Feature Specifications
Core Features Implementation
1. Dashboard
Purpose: Provide an overview of user's projects and tasks
Components:

Statistics cards (active projects, completed tasks, productivity rate)
Recent project progress
Upcoming deadlines
Recent activity feed

Implementation Priority: High
Estimated Time: 2-3 days
2. Kanban Board
Purpose: Visual task management with drag-and-drop functionality
Components:

Column-based layout (To Do, In Progress, Review, Done)
Draggable task cards
Add task functionality
Project filtering

Technical Requirements:

HTML5 Drag and Drop API
Position tracking for tasks
Real-time status updates

Implementation Priority: High
Estimated Time: 3-4 days
3. Project Management
Purpose: Create, edit, and track projects
Components:

Project list/grid view
Project creation form
Progress tracking
Status management

Implementation Priority: High
Estimated Time: 2-3 days
4. Task Management
Purpose: Detailed task operations
Components:

Task list with filtering
Task creation/editing
Priority and status management
Due date tracking

Implementation Priority: High
Estimated Time: 2-3 days
5. Analytics
Purpose: Productivity insights and reporting
Components:

Completion rate tracking
Time allocation analysis
Project progress charts
Performance insights

Technical Requirements:

Chart.js integration
Data aggregation queries
Export functionality

Implementation Priority: Medium
Estimated Time: 3-4 days
6. Calendar View
Purpose: Timeline and deadline management
Components:

Monthly calendar view
Event/deadline display
Quick task creation

Implementation Priority: Medium
Estimated Time: 2-3 days
7. Reports
Purpose: Generate and export detailed reports
Components:

Pre-defined report templates
Custom report builder
Export functionality (PDF, CSV)

Implementation Priority: Low
Estimated Time: 3-4 days
Development Phases
Phase 1: Core Backend (Week 1-2)

Database setup and migrations
Authentication system
Basic CRUD operations for projects and tasks
API endpoints implementation

Phase 2: Basic Frontend (Week 2-3)

Project structure setup
Dashboard implementation
Project and task management pages
Basic styling and responsive design

Phase 3: Kanban Board (Week 3-4)

Drag and drop functionality
Real-time updates
Visual feedback and animations
Mobile optimization

Phase 4: Analytics and Reports (Week 4-5)

Chart implementation
Data aggregation
Report generation
Export functionality

Phase 5: Polish and Optimization (Week 5-6)

Performance optimization
Error handling improvement
Testing and bug fixes
Documentation completion


Deployment Guide
Local Development Setup
Prerequisites
bash# Node.js 18+ required
node --version

# Install dependencies
npm install
Environment Setup
bash# Copy environment file
cp .env.example .env

# Edit configuration
nano .env
Database Initialization
bash# Run migrations
npm run migrate

# Optional: Add sample data
npm run seed
Start Development Server
bash# Start with auto-reload
npm run dev

# Or start production mode
npm start
Production Deployment
Option 1: Local Server Setup
bash# Create production directory
mkdir -p /opt/projectflow
cd /opt/projectflow

# Clone repository
git clone your-repo-url .

# Install dependencies
npm ci --production

# Set up environment
cp .env.example .env
# Edit .env with production values

# Build frontend
npm run build

# Start with PM2
npm install -g pm2
pm2 start ecosystem.config.js
pm2 save
pm2 startup
Option 2: Docker Deployment
dockerfile# Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --production

COPY . .

RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]
yaml# docker-compose.yml
version: '3.8'
services:
  projectflow:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - ./data:/app/data
      - ./backups:/app/backups
    environment:
      - NODE_ENV=production
    restart: unless-stopped
Option 3: Standalone Executable
bash# Install pkg globally
npm install -g pkg

# Build executable
pkg package.json --targets node18-linux-x64,node18-win-x64,node18-macos-x64
Backup Strategy
Automated Backups
javascript// src/utils/backup.js
import fs from 'fs/promises';
import path from 'path';
import { Database } from '../config/database.js';

export class BackupManager {
  constructor() {
    this.backupDir = path.join(process.cwd(), 'backups');
    this.dbPath = path.join(process.cwd(), 'data', 'projectflow.db');
  }
  
  async createBackup() {
    await fs.mkdir(this.backupDir, { recursive: true });
    
    const timestamp = new Date().toISOString().replace(/[:.]/g, '-');
    const backupFile = path.join(this.backupDir, `backup-${timestamp}.db`);
    
    await fs.copyFile(this.dbPath, backupFile);
    
    // Keep only last 30 backups
    await this.cleanOldBackups();
    
    return backupFile;
  }
  
  async cleanOldBackups() {
    const files = await fs.readdir(this.backupDir);
    const backupFiles = files
      .filter(file => file.startsWith('backup-') && file.endsWith('.db'))
      .sort()
      .reverse();
    
    if (backupFiles.length > 30) {
      const filesToDelete = backupFiles.slice(30);
      for (const file of filesToDelete) {
        await fs.unlink(path.join(this.backupDir, file));
      }
    }
  }
  
  async restoreBackup(backupFile) {
    const backupPath = path.join(this.backupDir, backupFile);
    await fs.copyFile(backupPath, this.dbPath);
  }
}
Security Considerations
Input Validation
javascript// src/middleware/validation.js
import { body, validationResult } from 'express-validator';

export const validateProject = [
  body('name')
    .trim()
    .isLength({ min: 1, max: 200 })
    .withMessage('Project name must be between 1 and 200 characters'),
  
  body('description')
    .optional()
    .isLength({ max: 2000 })
    .withMessage('Description must be less than 2000 characters'),
  
  body('priority')
    .optional()
    .isIn(['low', 'medium', 'high'])
    .withMessage('Priority must be low, medium, or high'),
  
  body('due_date')
    .optional()
    .isISO8601()
    .withMessage('Due date must be a valid date'),
  
  (req, res, next) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({
        success: false,
        message: 'Validation failed',
        errors: errors.array()
      });
    }
    next();
  }
];
Rate Limiting
javascript// src/middleware/rateLimiter.js
import { RateLimiterMemory } from 'rate-limiter-flexible';

const rateLimiter = new RateLimiterMemory({
  keyGenerator: (req) => req.ip,
  points: 100, // Number of requests
  duration: 60, // Per 60 seconds
});

export async function rateLimitMiddleware(req, res, next) {
  try {
    await rateLimiter.consume(req.ip);
    next();
  } catch (rejRes) {
    res.status(429).json({
      success: false,
      message: 'Too many requests',
      retryAfter: Math.round(rejRes.msBeforeNext / 1000)
    });
  }
}

Performance Considerations
Database Optimization
Indexing Strategy
sql-- Add performance indexes
CREATE INDEX idx_tasks_project_status ON tasks(project_id, status);
CREATE INDEX idx_tasks_user_due_date ON tasks(user_id, due_date);
CREATE INDEX idx_projects_user_status ON projects(user_id, status);
CREATE INDEX idx_time_logs_user_date ON time_logs(user_id, logged_date);
Query Optimization
javascript// Efficient project loading with task counts
async findProjectsWithTaskCounts(userId) {
  const query = `
    SELECT 
      p.*,
      COUNT(t.id) as task_count,
      COUNT(CASE WHEN t.status = 'done' THEN 1 END) as completed_tasks
    FROM projects p
    LEFT JOIN tasks t ON p.id = t.project_id
    WHERE p.user_id = ?
    GROUP BY p.id
    ORDER BY p.updated_at DESC
  `;
  
  return await this.db.all(query, [userId]);
}
Frontend Optimization
Lazy Loading
javascript// Lazy load components
const Dashboard = () => import('./pages/Dashboard.js');
const KanbanBoard = () => import('./pages/KanbanBoard.js');

// Route-based code splitting
const router = {
  '/dashboard': Dashboard,
  '/kanban': KanbanBoard,
  // ...
};
Virtual Scrolling for Large Lists
javascript// Virtual scrolling for task lists
class VirtualTaskList {
  constructor(container, itemHeight = 60) {
    this.container = container;
    this.itemHeight = itemHeight;
    this.visibleCount = Math.ceil(container.clientHeight / itemHeight);
    this.scrollTop = 0;
    
    this.setupEventListeners();
  }
  
  render(tasks) {
    const startIndex = Math.floor(this.scrollTop / this.itemHeight);
    const endIndex = Math.min(startIndex + this.visibleCount, tasks.length);
    
    const visibleTasks = tasks.slice(startIndex, endIndex);
    
    // Render only visible items
    this.container.innerHTML = visibleTasks
      .map((task, index) => this.renderTask(task, startIndex + index))
      .join('');
  }
}
Caching Strategy
Frontend Caching
javascript// Simple cache implementation
class Cache {
  constructor(maxAge = 5 * 60 * 1000) { // 5 minutes
    this.cache = new Map();
    this.maxAge = maxAge;
  }
  
  set(key, value) {
    this.cache.set(key, {
      value,
      timestamp: Date.now()
    });
  }
  
  get(key) {
    const item = this.cache.get(key);
    if (!item) return null;
    
    if (Date.now() - item.timestamp > this.maxAge) {
      this.cache.delete(key);
      return null;
    }
    
    return item.value;
  }
  
  invalidate(pattern) {
    for (const key of this.cache.keys()) {
      if (key.includes(pattern)) {
        this.cache.delete(key);
      }
    }
  }
}

export const apiCache = new Cache();
Backend Caching
javascript// In-memory cache for frequently accessed data
import NodeCache from 'node-cache';

const cache = new NodeCache({ stdTTL: 300 }); // 5 minutes

export async function getCachedUserProjects(userId) {
  const cacheKey = `user_projects_${userId}`;
  let projects = cache.get(cacheKey);
  
  if (!projects) {
    projects = await ProjectModel.findByUserId(userId);
    cache.set(cacheKey, projects);
  }
  
  return projects;
}

This comprehensive documentation provides everything needed to develop a minimal, monochrome project management tool for local hosting. The design emphasizes simplicity, performance, and functionality while maintaining a clean, professional appearance.
Key implementation notes:

Start with Phase 1 (Core Backend) to establish the foundation
Use the provided color palette and component styles for consistency
Implement the Kanban board early as it's a key differentiator
Focus on performance from the beginning with proper indexing and caching
Maintain the minimal design philosophy throughout development
