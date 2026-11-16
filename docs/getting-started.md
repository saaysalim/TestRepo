# Getting Started Guide

This guide will help you set up and start using TestRepo.

## Prerequisites

Before you begin, ensure you have installed:
- **Node.js** (v16.x or higher) - [Download](https://nodejs.org/)
- **npm** or **yarn** (comes with Node.js)
- **Git** - [Download](https://git-scm.com/)

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/saaysalim/TestRepo.git
cd TestRepo
```

### 2. Install Dependencies

```bash
npm install
# or
yarn install
```

### 3. Configure Environment

Create a `.env.local` file in the project root:

```env
VITE_API_URL=http://localhost:3000
VITE_ENV=development
```

### 4. Start Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:5173`

## Available Scripts

### Development
```bash
npm run dev        # Start development server
npm run dev:host   # Start with network access
```

### Building
```bash
npm run build      # Build for production
npm run preview    # Preview production build locally
```

### Testing & Quality
```bash
npm test           # Run tests
npm run test:watch # Run tests in watch mode
npm run lint       # Run ESLint
npm run format     # Format code with Prettier
```

### Database & Migrations
```bash
npm run db:migrate # Run database migrations
npm run db:seed    # Seed database with sample data
```

## Project Structure

```
TestRepo/
├── .github/
│   └── workflows/           # GitHub Actions CI/CD pipelines
├── src/
│   ├── components/          # Reusable React components
│   ├── pages/               # Page-level components
│   ├── utils/               # Utility functions
│   ├── App.tsx              # Main app component
│   └── main.tsx             # Entry point
├── docs/                    # Documentation files
├── tests/                   # Test files
├── public/                  # Static assets
├── package.json             # Project dependencies
├── tsconfig.json            # TypeScript configuration
├── vite.config.ts           # Vite configuration
└── README.md                # Project overview
```

## Common Tasks

### Adding a New Component

1. Create component file: `src/components/MyComponent.tsx`
2. Create test file: `tests/MyComponent.test.tsx`
3. Export from: `src/components/index.ts`

### Adding a New Page

1. Create page file: `src/pages/MyPage.tsx`
2. Add route in: `src/App.tsx`
3. Create tests if needed

### Running Tests

```bash
# Run all tests
npm test

# Run specific test
npm test -- MyComponent.test.tsx

# Run with coverage
npm test -- --coverage
```

## Troubleshooting

### Port Already in Use
```bash
# Kill process on port 5173
# Windows
netstat -ano | findstr :5173
taskkill /PID <PID> /F

# macOS/Linux
lsof -i :5173
kill -9 <PID>
```

### Dependencies Not Installing
```bash
# Clear npm cache
npm cache clean --force

# Remove node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

### Build Errors
```bash
# Check TypeScript errors
npx tsc --noEmit

# Clear build cache
rm -rf dist
npm run build
```

## Next Steps

- Read the [API Reference](./api-reference.md)
- Check the [CI/CD Documentation](./cicd.md)
- Review [Contributing Guidelines](../CONTRIBUTING.md)

## Getting Help

- 📚 Check [documentation](../docs)
- 🐛 Report issues on [GitHub Issues](https://github.com/saaysalim/TestRepo/issues)
- 💬 Ask questions on [GitHub Discussions](https://github.com/saaysalim/TestRepo/discussions)

---

Happy coding! 🚀
