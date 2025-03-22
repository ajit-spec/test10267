# MEAN Stack Application

## Project Overview
This is a full-stack JavaScript application built using the MEAN stack architecture. It provides a robust framework for developing modern web applications with a NoSQL database, RESTful API backend, and a dynamic frontend.

The application demonstrates best practices for building scalable web applications with proper separation of concerns, authentication, data validation, and responsive design.

## Technologies Used

### Core MEAN Stack
- **MongoDB**: A NoSQL database used to store application data in JSON-like documents
- **Express.js**: A web application framework for Node.js that handles API requests and routes
- **Angular**: A platform and framework for building client-side applications with TypeScript
- **Node.js**: A JavaScript runtime environment that executes server-side code

### Additional Technologies
- **Mongoose**: ODM (Object Data Modeling) library for MongoDB and Node.js
- **JSON Web Tokens (JWT)**: For secure authentication and authorization
- **Angular Material**: UI component library implementing Material Design
- **ngRx**: State management library for Angular applications
- **Jasmine/Karma**: Testing frameworks for Angular
- **Mocha/Chai**: Testing frameworks for Node.js
- **Docker**: For containerization and deployment

## Prerequisites
Before you begin, ensure you have the following installed:

- Node.js (v14.0.0 or higher)
- npm (v6.0.0 or higher)
- MongoDB (v4.0.0 or higher)
- Angular CLI (v12.0.0 or higher)
- Git

## Installation Instructions

### Clone the Repository
```bash
git clone https://github.com/yourusername/mean-stack-app.git
cd mean-stack-app
```

### Backend Setup
```bash
# Navigate to the server directory
cd server

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env file with your configuration

# Start the development server
npm run dev
```

### Frontend Setup
```bash
# Navigate to the client directory
cd client

# Install dependencies
npm install

# Start the Angular development server
ng serve
```

### Database Setup
```bash
# Make sure MongoDB is running
mongod --dbpath=/path/to/data/db

# To seed the database with sample data (optional)
npm run seed
```

## Project Structure
```
mean-stack-app/
├── client/                 # Angular frontend application
│   ├── src/                # Source files
│   │   ├── app/            # Application components
│   │   │   ├── components/ # Reusable UI components
│   │   │   ├── pages/      # Page components
│   │   │   ├── services/   # Angular services
│   │   │   ├── models/     # TypeScript interfaces
│   │   │   ├── guards/     # Route guards
│   │   │   └── store/      # ngRx store (actions, reducers, effects)
│   │   ├── assets/         # Static assets
│   │   └── environments/   # Environment configurations
│   ├── angular.json        # Angular CLI configuration
│   └── package.json        # Frontend dependencies
│
├── server/                 # Node.js/Express backend
│   ├── config/             # Configuration files
│   ├── controllers/        # Request handlers
│   ├── middleware/         # Express middleware
│   ├── models/             # Mongoose models
│   ├── routes/             # API routes
│   ├── services/           # Business logic
│   ├── utils/              # Utility functions
│   ├── tests/              # Backend tests
│   └── package.json        # Backend dependencies
│
├── .gitignore              # Git ignore file
├── docker-compose.yml      # Docker composition
├── Dockerfile              # Docker configuration
├── package.json            # Root dependencies and scripts
└── README.md               # Project documentation
```

## API Endpoints

### Authentication
- **POST /api/auth/register** - Register a new user
  - Body: `{ "name": "User Name", "email": "user@example.com", "password": "password123" }`
- **POST /api/auth/login** - Login and get an access token
  - Body: `{ "email": "user@example.com", "password": "password123" }`
- **GET /api/auth/profile** - Get user profile (requires authentication)

### Users
- **GET /api/users** - Get all users (admin only)
- **GET /api/users/:id** - Get specific user by ID
- **PUT /api/users/:id** - Update user (authenticated user or admin)
- **DELETE /api/users/:id** - Delete user (admin only)

### Items (Example Resource)
- **GET /api/items** - Get all items
  - Query params: `limit`, `page`, `sort`, `search`
- **GET /api/items/:id** - Get specific item by ID
- **POST /api/items** - Create a new item (requires authentication)
  - Body: `{ "title": "Item Name", "description": "Item description", "price": 99.99 }`
- **PUT /api/items/:id** - Update an item (requires authentication)
- **DELETE /api/items/:id** - Delete an item (requires authentication)

## Usage Examples

### User Authentication
```typescript
// Login example
this.http.post<{token: string, userId: string}>('/api/auth/login', {
  email: 'user@example.com',
  password: 'password123'
}).subscribe(response => {
  localStorage.setItem('token', response.token);
  localStorage.setItem('userId', response.userId);
});
```

### Making Authenticated Requests
```typescript
// Get user profile with authorization header
const token = localStorage.getItem('token');
this.http.get('/api/auth/profile', {
  headers: { Authorization: `Bearer ${token}` }
}).subscribe(profile => {
  console.log(profile);
});
```

### Create and Retrieve Items
```typescript
// Create an item
this.http.post('/api/items', {
  title: 'New Item',
  description: 'Item description',
  price: 99.99
}, {
  headers: { Authorization: `Bearer ${token}` }
}).subscribe(newItem => {
  console.log('Created:', newItem);
});

// Get all items
this.http.get('/api/items').subscribe(items => {
  console.log('Items:', items);
});
```

## Testing

### Backend Testing
```bash
# Navigate to the server directory
cd server

# Run all tests
npm test

# Run tests with coverage
npm run test:coverage

# Run a specific test file
npm test -- --grep="Auth Controller"
```

### Frontend Testing
```bash
# Navigate to the client directory
cd client

# Run unit tests
ng test

# Run end-to-end tests
ng e2e

# Run tests with coverage
ng test --code-coverage
```

## Deployment

### Using Docker
```bash
# Build Docker images
docker-compose build

# Start the application
docker-compose up

# To run in detached mode
docker-compose up -d
```

### Manual Deployment

#### Backend
```bash
cd server
npm run build
npm start
```

#### Frontend
```bash
cd client
ng build --prod
```
After building the frontend, deploy the contents of the `dist/` directory to a web server such as Nginx or Apache.

### Cloud Deployment Options
- **Heroku**: Use the provided Procfile for easy deployment
- **AWS**: Deploy using Elastic Beanstalk or EC2
- **Google Cloud**: Deploy using App Engine or Compute Engine
- **MongoDB Atlas**: For managed MongoDB hosting

## Contributing Guidelines

### Getting Started
1. Fork the repository
2. Clone your forked repository
3. Create a new branch (`git checkout -b feature/AmazingFeature`)
4. Make your changes
5. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
6. Push to the branch (`git push origin feature/AmazingFeature`)
7. Open a Pull Request

### Coding Standards
- Follow the [Angular Style Guide](https://angular.io/guide/styleguide) for frontend code
- Use ESLint and Prettier for code formatting
- Write meaningful commit messages following [Conventional Commits](https://www.conventionalcommits.org/)
- Document all public methods and components
- Write tests for new features

### Pull Request Process
1. Update the README.md with details of changes if applicable
2. Update the package.json version following [Semantic Versioning](https://semver.org/)
3. The PR must be approved by at least one reviewer
4. PR will be merged once CI checks pass

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Express.js Documentation](https://expressjs.com/)
- [Angular Documentation](https://angular.io/docs)
- [Node.js Documentation](https://nodejs.org/en/docs/)

