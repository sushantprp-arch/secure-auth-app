# Secure Auth App

A full-stack authentication app with user registration, login, and two ways to recover a forgotten password: **email OTP** or **security questions**.

## Features

- **Registration:** name, username, email, password, and recovery details (previous school, date of birth)
- **Login:** sign in with username or email, using an HttpOnly session cookie
- **Password recovery:**
  - Email OTP: 6-digit code, 5-minute expiry, single use, max 5 attempts
  - Security questions: previous school name and date of birth
- **Security:** bcrypt hashing for passwords, security answers and OTPs; rate limiting; responses that don't reveal whether an account exists; sessions revoked after a password reset
- **Responsive UI** with light and dark mode

## Tech Stack

- **Backend:** Node.js, Express
- **Security:** bcryptjs
- **Email:** Nodemailer (SMTP)
- **Storage:** JSON file (`data/users.json`)
- **Frontend:** HTML, CSS, vanilla JavaScript

## Getting Started

Requires Node.js 16 or later.

```bash
git clone https://github.com/<your-username>/secure-auth-app.git
cd secure-auth-app
npm install
cp .env.example .env
npm start
```

Open http://localhost:3000

## Configuration

Edit `.env` with your SMTP details:

| Variable    | Description                         |
| ----------- | ----------------------------------- |
| `PORT`      | Server port (default 3000)          |
| `SMTP_HOST` | SMTP server host                    |
| `SMTP_PORT` | SMTP port (587 or 465)              |
| `SMTP_USER` | SMTP username                       |
| `SMTP_PASS` | SMTP password or app password       |
| `SMTP_FROM` | Sender name and email               |

For Gmail, enable 2-Step Verification and use an App Password as `SMTP_PASS`.

## API Endpoints

| Method | Endpoint                 | Description                     |
| ------ | ------------------------ | ------------------------------- |
| POST   | `/api/register`          | Create an account               |
| POST   | `/api/login`             | Sign in                         |
| GET    | `/api/me`                | Get the current user            |
| POST   | `/api/logout`            | Sign out                        |
| POST   | `/api/forgot/otp/send`   | Email an OTP                    |
| POST   | `/api/forgot/otp/verify` | Verify an OTP                   |
| POST   | `/api/forgot/security`   | Verify security answers         |
| POST   | `/api/forgot/reset`      | Set a new password              |

## Production Notes

- Replace the JSON file with a database
- Serve over HTTPS and set the `Secure` cookie flag
- Store sessions in Redis or a database
- Add CSRF protection and a dedicated rate limiter
- Never commit your `.env` file

## License

MIT
