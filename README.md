# Forgot Password & Reset Password System

A complete authentication system with forgot password and reset password functionality built with Node.js, Express.js, MongoDB, and JWT tokens.

## Features

- **User Registration & Login** with secure password hashing (bcrypt)
- **JWT Authentication** for secure session management
- **Forgot Password** functionality with email integration
- **Reset Password** with secure token validation
- **Email Integration** using Nodemailer with Gmail SMTP
- **Responsive Frontend** built with HTML and Tailwind CSS
- **Real-time Password Strength Indicator**
- **Token Expiration** (15 minutes for security)
- **Email Templates** with professional styling

## Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - MongoDB ODM
- **JWT** - JSON Web Tokens for authentication
- **bcryptjs** - Password hashing
- **Nodemailer** - Email sending
- **CORS** - Cross-origin resource sharing
- **dotenv** - Environment variables

### Frontend
- **HTML5** - Markup
- **Tailwind CSS** - Styling framework
- **Vanilla JavaScript** - Client-side functionality

## Project Structure

```
forgot-password-system/
├── config/
│   └── database.js          # MongoDB connection
├── middleware/
│   └── auth.js              # JWT authentication middleware
├── models/
│   └── User.js              # User schema and methods
├── public/
│   ├── index.html           # Login/Register page
│   ├── forgot-password.html # Forgot password form
│   ├── reset-password.html  # Reset password form
│   └── dashboard.html       # User dashboard
├── routes/
│   └── auth.js              # Authentication routes
├── utils/
│   └── email.js             # Email sending utilities
├── .env                     # Environment variables
├── package.json             # Dependencies and scripts
├── server.js                # Main server file
└── README.md                # This file
```

## Installation & Setup

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local or cloud instance)
- Gmail account with App Password enabled

### 1. Clone the Repository
```bash
git clone <repository-url>
cd forgot-password-system
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Environment Configuration

Create a `.env` file in the root directory with the following variables:

```env
# MongoDB Configuration
MONGODB_URI=mongodb://localhost:27017/forgot-password-db

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
JWT_RESET_EXPIRE=15m

# Server Configuration
PORT=3000

# Email Configuration (Gmail SMTP)
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-password
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587

# Frontend URL (for reset links)
FRONTEND_URL=http://localhost:3000
```

### 4. Gmail App Password Setup

1. Enable 2-Factor Authentication on your Gmail account
2. Go to Google Account Settings → Security → App passwords
3. Generate an app password for "Mail"
4. Use this app password in the `EMAIL_PASS` environment variable

### 5. MongoDB Setup

**Option A: Local MongoDB**
- Install MongoDB locally
- Start MongoDB service
- Use connection string: `mongodb://localhost:27017/forgot-password-db`

**Option B: MongoDB Atlas (Cloud)**
- Create a free account at [MongoDB Atlas](https://www.mongodb.com/atlas)
- Create a cluster and get the connection string
- Replace `MONGODB_URI` in `.env` with your Atlas connection string

### 6. Start the Application

**Development Mode:**
```bash
npm run dev
```

**Production Mode:**
```bash
npm start
```

The application will be available at `http://localhost:3000`

## API Endpoints

### Authentication Routes (`/api/auth`)

| Method | Endpoint | Description | Body |
|--------|----------|-------------|------|
| POST | `/register` | Register new user | `{ name, email, password }` |
| POST | `/login` | User login | `{ email, password }` |
| POST | `/forgot-password` | Request password reset | `{ email }` |
| POST | `/reset-password/:token` | Reset password | `{ password, confirmPassword }` |
| GET | `/me` | Get current user | Headers: `Authorization: Bearer <token>` |

### Example API Usage

**Register User:**
```javascript
POST /api/auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword123"
}
```

**Login:**
```javascript
POST /api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "securepassword123"
}
```

**Forgot Password:**
```javascript
POST /api/auth/forgot-password
Content-Type: application/json

{
  "email": "john@example.com"
}
```

**Reset Password:**
```javascript
POST /api/auth/reset-password/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Content-Type: application/json

{
  "password": "newpassword123",
  "confirmPassword": "newpassword123"
}
```

## Frontend Pages

### 1. Login/Register Page (`/`)
- User login form
- User registration form
- Toggle between login and register
- "Forgot Password?" link

### 2. Forgot Password Page (`/forgot-password`)
- Email input form
- Send reset link functionality
- Success message with instructions
- Back to login link

### 3. Reset Password Page (`/reset-password/:token`)
- New password form with confirmation
- Real-time password strength indicator
- Password requirements checklist
- Token validation

### 4. Dashboard Page (`/dashboard`)
- Welcome message
- User information display
- Logout functionality
- Feature overview

## Security Features

### Password Security
- **bcrypt hashing** with salt rounds of 12
- **Minimum length** requirement (6 characters)
- **Password strength indicator** with real-time feedback
- **Password confirmation** validation

### Token Security
- **JWT tokens** for authentication
- **Separate reset tokens** with short expiration (15 minutes)
- **Token validation** on both client and server
- **Automatic token cleanup** after use

### Email Security
- **Secure SMTP** connection with TLS
- **Professional email templates** with HTML styling
- **Reset link expiration** for security
- **Confirmation emails** for password changes

## Testing the System

### 1. User Registration
1. Go to `http://localhost:3000`
2. Click "create a new account"
3. Fill in the registration form
4. Submit and verify successful registration

### 2. User Login
1. Use registered credentials to login
2. Verify redirect to dashboard
3. Check user information display

### 3. Forgot Password Flow
1. On login page, click "Forgot your password?"
2. Enter registered email address
3. Check email inbox for reset link
4. Click the reset link in email
5. Enter new password
6. Verify password reset success
7. Login with new password

### 4. Password Reset Security
1. Try using an expired token (wait 15+ minutes)
2. Try using an invalid token
3. Verify proper error handling

## Troubleshooting

### Common Issues

**1. Email not sending:**
- Verify Gmail app password is correct
- Check if 2FA is enabled on Gmail account
- Ensure EMAIL_USER and EMAIL_PASS are set correctly
- Check spam/junk folder

**2. MongoDB connection error:**
- Verify MongoDB is running (local setup)
- Check connection string format
- Ensure database permissions (Atlas setup)

**3. JWT token errors:**
- Verify JWT_SECRET is set in .env
- Check token expiration settings
- Clear browser localStorage if needed

**4. CORS errors:**
- Verify CORS is properly configured
- Check frontend and backend URLs match

### Debug Mode

Enable debug logging by adding to your `.env`:
```env
NODE_ENV=development
DEBUG=true
```

## Deployment

### Environment Variables for Production
```env
NODE_ENV=production
MONGODB_URI=your-production-mongodb-uri
JWT_SECRET=your-very-secure-jwt-secret-key
FRONTEND_URL=https://yourdomain.com
```

### Deployment Platforms
- **Heroku**: Add environment variables in dashboard
- **Vercel**: Configure environment variables in project settings
- **DigitalOcean**: Use App Platform with environment variables
- **AWS**: Use Elastic Beanstalk or EC2 with environment configuration

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

If you encounter any issues or have questions:

1. Check the troubleshooting section above
2. Review the console logs for error messages
3. Verify all environment variables are set correctly
4. Ensure all dependencies are installed

## Acknowledgments

- **Tailwind CSS** for the beautiful UI components
- **Nodemailer** for reliable email sending
- **MongoDB** for flexible data storage
- **JWT** for secure authentication
- **bcrypt** for password security
#   f o r g e t - i d - p a s s w o r d  
 