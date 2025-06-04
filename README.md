# Tasork Web Application

A modern task management system built with Next.js that integrates with the Tasork backend API. Tasork helps teams manage tasks, track progress, and collaborate efficiently.

Backend: https://github.com/Ghaby-X/tasork-backend
LiveURL: https://main.d36ea14wabu2og.amplifyapp.com/

## Features

- User authentication with AWS Cognito
- Task management (create, view, update, delete)
- Task assignment and status tracking
- User management and invitations
- Notifications system
- Dashboard with task statistics
- Responsive design for desktop and mobile

## Tech Stack

- Next.js 14 with App Router
- TypeScript
- Tailwind CSS for styling
- Zustand for state management
- Axios for API requests
- LocalStorage for token management

## Authentication Flow

Tasork uses token-based authentication:
- Login/Registration through AWS Cognito
- Tokens (access_token, id_token, refresh_token) stored in localStorage
- Protected API calls include x-id-token header
- Token refresh mechanism for extended sessions

## Getting Started

### Prerequisites

- Node.js 18+ and npm
- Tasork backend API running (Go with Chi router)

### Installation

1. Clone the repository
   ```bash
   git clone https://github.com/Ghaby-X/tasork-web.git
   cd tasork-web
   ```

2. Install dependencies
   ```bash
   npm install
   ```

3. Create a `.env.local` file with the following variables
   ```
   NEXT_PUBLIC_API_URL=http://localhost:8080
   ```

### Development

Run the development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Building for Production

```bash
npm run build
npm start
```

## Backend Integration

This frontend is designed to work with the Tasork backend API. The backend should:

1. Handle CORS properly for preflight requests:
   ```go
   corsMiddleware := cors.New(cors.Options{
       AllowedOrigins:   []string{"http://localhost:3000"},
       AllowedMethods:   []string{"GET", "POST", "PUT", "DELETE", "OPTIONS"},
       AllowedHeaders:   []string{"Accept", "Authorization", "Content-Type", "X-CSRF-Token", "x-id-token", "x-refresh-token"},
       ExposedHeaders:   []string{"Link"},
       AllowCredentials: true,
       MaxAge:           300,
   })
   r.Use(corsMiddleware.Handler)
   ```

2. Validate the x-id-token header for protected routes
3. Return new tokens when appropriate (e.g., after registration)

## Deployment

This application can be deployed to AWS Amplify using the included amplify.yml configuration file.

## Project Structure

- `/app` - Next.js App Router pages and layouts
- `/components` - Reusable UI components
- `/lib` - Utilities, API client, and state management
- `/public` - Static assets

## License

[MIT License](LICENSE)
