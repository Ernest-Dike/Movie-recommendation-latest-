MovieRecs - A Full-Stack Movie Recommendation App (V2)This project is a complete, full-stack movie recommendation application built with a separate React frontend and a Node.js/Express.js backend connected to a PostgreSQL database. This version addresses the architectural and security requirements of a production-grade application.Project ArchitectureThe application is structured into two main parts:/backend: A Node.js application using Express.js to provide a RESTful API for user authentication and data management./frontend: A React single-page application that consumes the backend API and provides the user interface.FeaturesSecure User Authentication:Registration with bcrypt password hashing.Login with secure password comparison.JWT (JSON Web Token) based sessions for stateless authentication.RESTful Backend API:Built with Express.js and connects to a PostgreSQL database.Protected routes that require a valid JWT for access.Movie Discovery & Filtering:Fetches data from the TMDB API.Search movies by title.Filter movies by minimum rating and sort by popularity, rating, or release date.User Features:Add/remove movies to a personal Favorites list or Watchlist.A Profile Page to view user details and curated movie lists.Responsive UI:Modern, responsive, dark-themed UI built with React and Tailwind CSS.Setup and InstallationFollow these instructions carefully to run the entire application locally.PrerequisitesNode.js and npmPostgreSQLA code editor (e.g., VS Code)A TMDB API Key (Get one here)Step 1: Backend SetupNavigate to the backend directory:cd backend
Install dependencies:npm install
Set up PostgreSQL Database:Log in to psql and create a new database:CREATE DATABASE movierecs_db;
Connect to the new database (\c movierecs_db) and run the following SQL to create the tables:CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE user_movies (
    id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    movie_id INTEGER NOT NULL,
    title VARCHAR(255) NOT NULL,
    poster_path VARCHAR(255),
    list_type VARCHAR(50) NOT NULL, -- 'favorite' or 'watchlist'
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(user_id, movie_id)
);
Create Environment File:Create a file named .env in the backend directory.Add the following variables, replacing the placeholders with your actual credentials.# .env (in backend/)

# PostgreSQL Connection URL
DATABASE_URL="postgresql://YOUR_DB_USER:YOUR_DB_PASSWORD@localhost:5432/movierecs_db"

# JWT Secret (use a long, random string)
JWT_SECRET="YOUR_SUPER_SECRET_RANDOM_STRING_FOR_JWT"

# Server Port
PORT=5000
Start the Backend Server:npm start
The backend API will be running at http://localhost:5000.Step 2: Frontend SetupOpen a new terminal and navigate to the frontend directory:cd frontend
Install dependencies:npm install
Create Environment File:Create a file named .env in the frontend directory.Add the following variables, providing your TMDB API key.# .env (in frontend/)

# URL for your backend API
REACT_APP_API_URL="http://localhost:5000/api"

# Your TMDB API Key
REACT_APP_TMDB_API_KEY="YOUR_TMDB_API_KEY_HERE"
Start the Frontend Application:npm start
The React app will open in your browser at http://localhost:3000.You now have the full-stack application running! You can register a new user, log in, and start exploring features.
