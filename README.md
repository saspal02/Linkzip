# LinkZip - URL Shortener

A full-stack URL shortener application that allows users to create short, memorable links, track click analytics, and manage their shortened URLs.

## Demo

[Watch the demo on YouTube](https://youtu.be/AA5Ili0Q_xg)

## Screenshots

### Home Page
![Screenshot 1](./screenshots/sc1.png)

### URL Shortener
![Screenshot 2](./screenshots/sc2.png)

### Analytics Dashboard
![Screenshot 3](./screenshots/sc3.png)

### Link Details
![Screenshot 4](./screenshots/sc4.png)

### Login / Auth
![Screenshot 5](./screenshots/sc5.png)

### Mobile View
![Screenshot 6](./screenshots/sc6.png)

## Features

- **URL Shortening** - Generate 8-character random alphanumeric short codes for any long URL
- **User Authentication** - JWT-based register/login with BCrypt password hashing
- **Analytics Dashboard** - Bar chart visualization of click counts over time using Chart.js
- **Click Tracking** - Every redirect records a click event with timestamp for analytics
- **Link Management** - View, manage, and track all your shortened URLs
- **Subdomain Routing** - Supports both main domain (`linkzip.com/go/{slug}`) and subdomain (`url.linkzip.com/{slug}`) patterns
- **Responsive Design** - Mobile-friendly UI with Tailwind CSS
- **Copy to Clipboard** - Generated short URLs are automatically copied to clipboard
- **Protected Routes** - Dashboard and URL management require authentication

## Tech Stack

### Frontend
- React 19
- Vite 7
- Tailwind CSS 4
- React Router DOM 7
- TanStack React Query v5
- Axios
- React Hook Form
- Chart.js + react-chartjs-2
- Material UI (Modals)
- Framer Motion
- React Hot Toast
- Day.js

### Backend
- Java 21
- Spring Boot 3.5.6
- Spring Security
- Spring Data JPA
- MySQL
- JWT (jjwt 0.13.0)
- Lombok
- Maven
- Docker

## Project Structure

```
LinkZip/
├── url-shortener-react/          # React frontend (Vite)
│   ├── src/
│   │   ├── api/                  # Axios configuration
│   │   ├── components/           # React components
│   │   │   ├── Dashboard/        # Dashboard components
│   │   │   ├── LoginPage.jsx
│   │   │   ├── RegisterPage.jsx
│   │   │   ├── LandingPage.jsx
│   │   │   └── ...
│   │   ├── contextApi/           # React Context for auth
│   │   ├── hooks/                # Custom React Query hooks
│   │   ├── utils/                # Helpers and constants
│   │   ├── App.jsx
│   │   ├── AppRouter.jsx
│   │   └── main.jsx
│   ├── .env
│   ├── package.json
│   └── vite.config.js
│
└── url-shortener-sb/             # Spring Boot backend
    ├── src/main/java/com/linkzip/urlshortener/
    │   ├── controller/           # REST controllers
    │   ├── dtos/                 # Data transfer objects
    │   ├── model/                # JPA entities
    │   ├── repository/           # Spring Data repositories
    │   ├── security/             # JWT & Spring Security config
    │   └── service/              # Business logic
    ├── src/main/resources/
    │   └── application.properties
    ├── .env
    ├── .env.prod
    ├── Dockerfile
    └── pom.xml
```

## API Endpoints

### Authentication (Public)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/public/register` | Register new user |
| POST | `/api/auth/public/login` | Login user |

### URL Management (Authenticated)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/urls/shorten` | Create a short URL |
| GET | `/api/urls/myurls` | Get all user's URLs |
| GET | `/api/urls/analytics/{shortUrl}` | Get click analytics (query: `startDate`, `endDate`) |
| GET | `/api/urls/totalClicks` | Get total clicks (query: `startDate`, `endDate`) |

### Redirect (Public)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/{shortUrl}` | Redirect to original URL (302) + records click |

## Database Schema

**Tables:**
- `users` - `id`, `email`, `username`, `password`, `role`
- `url_mapping` - `id`, `original_url`, `short_url`, `click_count`, `created_date`, `user_id` (FK)
- `click_event` - `id`, `click_date`, `url_mapping_id` (FK)

**Relationships:** `User` 1:N `UrlMapping` 1:N `ClickEvent`

## Getting Started

### Prerequisites

- Node.js 18+ and npm
- Java 21
- MySQL

### Frontend Setup

```bash
cd url-shortener-react

# Install dependencies
npm install

# Create .env file with the following variables:
# VITE_BACKEND_URL=http://localhost:8080
# VITE_REACT_FRONT_END_URL=http://localhost:5173
# VITE_REACT_SUBDOMAIN=http://url.localhost:5173

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Lint code
npm run lint
```

### Backend Setup

```bash
cd url-shortener-sb

# Create .env file with your database credentials:
# DATABASE_URL=jdbc:mysql://localhost:3306/urlshortenerdb
# DATABASE_USERNAME=root
# DATABASE_PASSWORD=your_password
# JWT_SECRET=your_base64_encoded_secret
# FRONTEND_URL=http://localhost:5173

# Run with Maven wrapper
./mvnw spring-boot:run

# Or build JAR and run
./mvnw clean package -DskipTests
java -jar target/url-shortener-sb-0.0.1-SNAPSHOT.jar
```

### Docker (Backend)

```bash
# Build image
docker build -t linkzip-backend .

# Run container
docker run -p 8080:8080 --env-file .env linkzip-backend
```

## Deployment

- **Frontend**: Deployed on Netlify with `_redirects` for SPA routing
- **Backend**: Deployed on Render
- **Database**: Production MySQL hosted on Aiven Cloud

## Security

- Passwords hashed with BCrypt
- JWT tokens for authentication (Bearer token in Authorization header)
- Spring Security filter chain validates JWT on protected endpoints
- CORS configured to allow requests only from the configured frontend URL
- CSRF disabled (stateless JWT API)
- JWT expiration: 48 hours

## Connect with Me

[![LinkedIn](https://img.shields.io/badge/LinkedIn‑Saswat%20Pal-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/saswat-pal/)
[![X / Twitter](https://img.shields.io/badge/X‑@saspal02-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/saspal02)


