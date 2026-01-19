# Kanban App - 3-Tier Architecture

A modern Kanban board application built with Node.js, Express, and MySQL for deployment in a 3-tier AWS architecture.

## Features

- Create, update, and delete tasks
- Drag tasks between Todo, In Progress, and Done columns
- Persistent storage in MySQL database
- RESTful API
- Responsive UI

## Requirements

- Node.js 18+ or 20+
- MySQL 8.0+
- Environment variables (see below)

## Local Development

1. Install dependencies:
```bash
npm install
```

2. Create `.env` file:
```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=kanban_db
PORT=3000
```

3. Run the application:
```bash
npm start
```

4. Open http://localhost:3000

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| DB_HOST | MySQL database hostname | Yes |
| DB_USER | Database username | Yes |
| DB_PASSWORD | Database password | Yes |
| DB_NAME | Database name | Yes |
| PORT | Application port (default: 80) | No |

## API Endpoints

- `GET /health` - Health check
- `GET /api/tasks` - Get all tasks
- `GET /api/tasks/:id` - Get single task
- `POST /api/tasks` - Create task
- `PUT /api/tasks/:id` - Update task
- `DELETE /api/tasks/:id` - Delete task

## Deployment

This app is designed to be deployed via Terraform user-data scripts. See `deployment/README.md` for AWS deployment instructions.

## License

MIT
