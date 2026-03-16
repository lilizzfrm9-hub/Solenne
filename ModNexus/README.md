# ModNexus Application

## Project Structure

```
ModNexus/
├── src/
│   ├── components/
│   │   ├── Header/
│   │   ├── Footer/
│   │   └── Dashboard/
│   ├── pages/
│   │   ├── Home.js
│   │   └── Login.js
│   ├── utils/
│   │   └── api.js
│   ├── App.js
│   └── index.js
├── public/
│   └── index.html
├── server/
│   ├── config/
│   ├── controllers/
│   ├── models/
│   └── routes/
├── database/
│   └── schema.sql
├── .gitignore
├── README.md
└── package.json
```

## Database Schema

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE comments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    post_id INT NOT NULL,
    user_id INT NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (post_id) REFERENCES posts(id),
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE sessions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    token VARCHAR(255) NOT NULL UNIQUE,
    expires_at DATETIME NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

## API Endpoints

### Authentication
- `POST /api/auth/login`: Log in a user
- `POST /api/auth/register`: Register a new user
- `POST /api/auth/logout`: Log out a user

### Posts
- `GET /api/posts`: Retrieve all posts
- `POST /api/posts`: Create a new post
- `GET /api/posts/:id`: Retrieve a specific post
- `PUT /api/posts/:id`: Update a specific post
- `DELETE /api/posts/:id`: Delete a specific post

### Comments
- `GET /api/posts/:id/comments`: Retrieve comments for a post
- `POST /api/posts/:id/comments`: Create a comment for a post

## UI Components
### Header
- Logout button
- Navigation links

### Footer
- Copyright notice

### Dashboard
- List of posts
- Button to create a new post

## CI/CD Workflows
1. **Continuous Integration**:
   - On pull request: run tests and linting.
   - Build and test the application.

2. **Continuous Deployment**:
   - On push to main: deploy to the production server.
   - Use tools like GitHub Actions to automate workflows.
