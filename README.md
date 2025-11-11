# Job Seeking Frontend Application

A modern, full-featured job seeking platform built with Next.js that connects job seekers with employers. This application provides separate interfaces for candidates and recruiters, featuring job search, CV analysis, real-time chat, notifications, and AI-powered job/candidate recommendations.

## 🚀 Features

### For Job Seekers (Candidates)
- **Job Search & Discovery**
  - Advanced job search with filters (keyword, location, category)
  - Browse jobs by categories
  - Featured jobs and companies
  - Job recommendations powered by AI
  - Save and manage favorite jobs
  - Track applied jobs

- **Profile Management**
  - Create and manage candidate profile
  - Upload and analyze CV/Resume
  - View profile analytics
  - Change password

- **Application Management**
  - Apply to jobs with one click
  - Track application status
  - View application history

- **Communication**
  - Real-time chat with recruiters
  - Notification system for job updates
  - Availability status management

### For Employers (Recruiters)
- **Job Management**
  - Post and manage job listings
  - Edit job details
  - View job applications
  - Track job performance

- **Candidate Management**
  - Browse candidate profiles
  - AI-powered candidate recommendations
  - Save favorite candidates
  - Search and filter candidates

- **Company Management**
  - Register and manage company profile
  - View company details
  - Manage company information

- **Communication**
  - Real-time chat with candidates
  - Notification system
  - Candidate availability tracking

### Additional Features
- **Authentication**
  - Email/password authentication
  - OAuth integration (Google, GitHub)
  - Session management with NextAuth

- **Admin Panel**
  - System operations management
  - Administrative controls

- **Real-time Features**
  - Live chat functionality
  - Push notifications
  - Real-time updates

## 🛠️ Tech Stack

- **Framework**: Next.js 15.0.1 (React 18.3.1)
- **Styling**: Tailwind CSS 3.4.1
- **Authentication**: NextAuth.js 4.24.11
- **Database**: Prisma ORM with PostgreSQL
- **Real-time**: Firebase 11.6.0
- **PDF Processing**: react-pdf, pdfjs-dist, jspdf
- **Charts**: Chart.js with react-chartjs-2
- **UI Components**: 
  - Heroicons
  - React Icons
  - React Select
  - Swiper
- **Payments**: Stripe (React Stripe.js)
- **Image Processing**: html2canvas

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v18 or higher)
- npm, yarn, pnpm, or bun
- PostgreSQL database (or your preferred database)
- Backend API server running on `http://localhost:8080`

## 🔧 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd jobapp
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   # or
   pnpm install
   ```

3. **Set up environment variables**
   
   Create a `.env.local` file in the root directory with the following variables:
   ```env
   # NextAuth Configuration
   NEXTAUTH_URL=http://localhost:3000
   NEXTAUTH_SECRET=your-nextauth-secret-key

   # OAuth Providers
   GOOGLE_CLIENT_ID=your-google-client-id
   GOOGLE_CLIENT_SECRET=your-google-client-secret
   GITHUB_CLIENT_ID=your-github-client-id
   GITHUB_CLIENT_SECRET=your-github-client-secret

   # Database (if using Prisma directly)
   DATABASE_URL=your-database-connection-string

   # Firebase (for real-time features)
   FIREBASE_API_KEY=your-firebase-api-key
   FIREBASE_AUTH_DOMAIN=your-firebase-auth-domain
   FIREBASE_PROJECT_ID=your-firebase-project-id
   FIREBASE_STORAGE_BUCKET=your-firebase-storage-bucket
   FIREBASE_MESSAGING_SENDER_ID=your-firebase-messaging-sender-id
   FIREBASE_APP_ID=your-firebase-app-id

   # Stripe (for payments)
   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=your-stripe-publishable-key
   ```

4. **Set up Prisma (if using)**
   ```bash
   npx prisma generate
   npx prisma migrate dev
   ```

## 🚀 Running the Application

### Development Mode

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to see the application.

### Production Build

```bash
# Build the application
npm run build

# Start the production server
npm start
```

### Linting

```bash
npm run lint
```

## 📁 Project Structure

```
jobapp/
├── public/                 # Static assets
│   └── pdf.worker.min.js  # PDF.js worker
├── src/
│   ├── app/               # Next.js App Router pages
│   │   ├── admin/        # Admin panel
│   │   ├── auth/         # Authentication (NextAuth)
│   │   ├── candidate/    # Candidate-specific pages
│   │   │   ├── login/    # Candidate login
│   │   │   ├── register/ # Candidate registration
│   │   │   └── chat.js   # Candidate chat
│   │   ├── common/       # Shared components
│   │   │   ├── chatbox.js
│   │   │   ├── customtopbar.js
│   │   │   ├── footer.js
│   │   │   ├── searchbar.js
│   │   │   └── ...
│   │   ├── company/      # Company pages
│   │   ├── components/   # Reusable React components
│   │   ├── context/      # React Context providers
│   │   ├── cv/           # CV/Resume pages
│   │   ├── job/          # Job-related pages
│   │   │   ├── applied/  # Applied jobs
│   │   │   ├── apply/    # Job application
│   │   │   ├── detail/   # Job details
│   │   │   └── saved/    # Saved jobs
│   │   ├── job-recommendation/ # AI job recommendations
│   │   ├── profile/      # User profile pages
│   │   ├── recruiter/    # Recruiter-specific pages
│   │   │   ├── candidate-recommendation/
│   │   │   ├── candidates/
│   │   │   ├── jobs-management/
│   │   │   ├── my-company/
│   │   │   └── saved-candidates/
│   │   ├── services/     # Service utilities
│   │   ├── utils/        # Utility functions
│   │   │   └── api.js    # API helper functions
│   │   ├── layout.js     # Root layout
│   │   ├── page.js       # Home page
│   │   └── globals.css   # Global styles
│   ├── components/       # Shared components
│   ├── middleware.js     # Next.js middleware
│   └── pages/            # Pages directory (if using)
├── next.config.js        # Next.js configuration
├── tailwind.config.js    # Tailwind CSS configuration
├── postcss.config.mjs    # PostCSS configuration
├── jsconfig.json         # JavaScript configuration
└── package.json          # Dependencies
```

## 🔌 API Configuration

The application is configured to proxy API requests to a backend server. By default, it expects the backend to run on `http://localhost:8080`. This is configured in `next.config.js`:

```javascript
async rewrites() {
  return [
    {
      source: '/api/:path*',
      destination: 'http://localhost:8080/api/:path*',
    },
    {
      source: '/api/v1/:path*',
      destination: 'http://localhost:8080/api/v1/:path*',
    },
  ];
}
```

Make sure your backend API server is running before starting the frontend application.

## 🎨 Key Features Breakdown

### Authentication Flow
- Supports multiple authentication methods (email/password, OAuth)
- Session management with NextAuth
- Protected routes for authenticated users
- Role-based access (candidate, recruiter, admin)

### Job Search
- Real-time search with debouncing
- Multi-filter support (keyword, location, category)
- Search result persistence
- Pagination support

### CV Analysis
- PDF upload and parsing
- Automated CV analysis
- Scheduled analysis jobs
- CV recommendations based on job requirements

### Real-time Chat
- WebSocket-based chat (via Firebase)
- Message history
- Online/offline status
- Notification badges

### Notifications
- Real-time push notifications
- Notification dropdown
- Toast notifications
- Notification context management

## 🧪 Development Notes

- The application uses React Strict Mode disabled in development
- Hydration warnings are suppressed for better compatibility with browser extensions
- PDF.js worker is configured for client-side PDF processing
- Custom webpack configuration handles Node.js module fallbacks

## 📝 Environment Variables

Make sure to set up all required environment variables in `.env.local`. Refer to the Installation section for the complete list.

## 🚢 Deployment

### Vercel (Recommended)

The easiest way to deploy this Next.js app is using [Vercel](https://vercel.com):

1. Push your code to GitHub
2. Import your repository to Vercel
3. Add environment variables in Vercel dashboard
4. Deploy

### Other Platforms

You can also deploy to other platforms that support Next.js:
- Netlify
- AWS Amplify
- DigitalOcean App Platform
- Railway
- Render

Make sure to:
- Set all environment variables
- Configure API proxy settings if needed
- Set up database connections
- Configure OAuth redirect URLs

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is private and proprietary.

## 🆘 Support

For issues and questions:
- Check existing issues in the repository
- Create a new issue with detailed information
- Contact the development team

## 🔄 Version

Current version: 0.1.0

---

Built with ❤️ using Next.js and React
