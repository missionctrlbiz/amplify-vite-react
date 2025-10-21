# AWS Amplify Gen 2 + Vite + React Starter

A modern full-stack application built with AWS Amplify Gen 2, Vite, React, and TypeScript. This starter template includes authentication, a GraphQL API, and a real-time database.

## Features

- ⚡️ **Vite** - Lightning-fast build tool and dev server
- ⚛️ **React 19** - Latest React with TypeScript support
- 🔐 **AWS Amplify Gen 2 Auth** - Built-in authentication with email sign-up
- 📊 **GraphQL API** - Type-safe data layer with real-time subscriptions
- 🎨 **Amplify UI Components** - Pre-built, customizable UI components
- 🔒 **Type Safety** - Full TypeScript support throughout the stack

## Prerequisites

- Node.js 18.x or later
- npm 10.x or later
- An AWS account (for deployment)

## Getting Started

### 1. Install Dependencies

```bash
npm install
```

### 2. Local Development

To run the app locally:

```bash
npm run dev
```

This will start the Vite development server at `http://localhost:5173`.

> **Note**: For local development without deploying to AWS, the app uses a placeholder configuration in `amplify_outputs.json`. To use real AWS services, follow the deployment steps below.

### 3. Deploy to AWS (Optional)

To deploy your backend to AWS Amplify:

```bash
# Install the Amplify CLI (if not already installed)
npm install -g @aws-amplify/cli

# Deploy the backend
npx ampx sandbox
```

This will:
- Create a new Amplify app in your AWS account
- Deploy authentication (Amazon Cognito)
- Deploy the GraphQL API (AWS AppSync)
- Generate the `amplify_outputs.json` configuration file

## Project Structure

```
amplify-vite-react/
├── amplify/                 # Amplify Gen 2 backend configuration
│   ├── auth/               # Authentication configuration
│   │   └── resource.ts     # Auth resource definition
│   ├── data/               # Data/API configuration
│   │   └── resource.ts     # GraphQL schema and API definition
│   ├── backend.ts          # Backend entry point
│   └── tsconfig.json       # TypeScript config for backend
├── src/                    # React frontend source
│   ├── App.tsx            # Main app component with auth and data
│   ├── App.css            # App styles
│   ├── main.tsx           # App entry point
│   └── index.css          # Global styles
├── amplify_outputs.json   # Amplify configuration (generated)
├── package.json           # Project dependencies
└── vite.config.ts         # Vite configuration
```

## Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build locally
- `npm run lint` - Run ESLint

## Backend Configuration

### Authentication

The app uses email-based authentication. Users can sign up and sign in with their email address. The configuration is defined in `amplify/auth/resource.ts`.

### Data API

The app includes a simple Todo data model with real-time subscriptions. The GraphQL schema is defined in `amplify/data/resource.ts`.

Example operations:
- Create a todo: Click "+ new" button
- Delete a todo: Click on the todo item
- Real-time updates: Changes are automatically synced across all clients

## Customization

### Adding New Data Models

Edit `amplify/data/resource.ts` to add new models:

```typescript
const schema = a.schema({
  Todo: a.model({
    content: a.string(),
  }),
  // Add your new model here
  Note: a.model({
    title: a.string(),
    body: a.string(),
  }).authorization((allow) => [allow.owner()]),
});
```

### Modifying Authentication

Edit `amplify/auth/resource.ts` to customize authentication:

```typescript
export const auth = defineAuth({
  loginWith: {
    email: true,
    // Add other login methods
    phone: true,
    // Or use social providers
    externalProviders: {
      google: {
        clientId: 'your-client-id',
        clientSecret: 'your-client-secret',
      },
    },
  },
});
```

## Learn More

- [AWS Amplify Gen 2 Documentation](https://docs.amplify.aws/gen2/)
- [Amplify UI Components](https://ui.docs.amplify.aws/)
- [Vite Documentation](https://vitejs.dev/)
- [React Documentation](https://react.dev/)

## Deployment

### Deploying to AWS Amplify Hosting

1. Push your code to a Git repository (GitHub, GitLab, Bitbucket, or AWS CodeCommit)
2. Go to the [AWS Amplify Console](https://console.aws.amazon.com/amplify/)
3. Click "New app" > "Host web app"
4. Connect your repository
5. Amplify will automatically detect the build settings
6. Click "Save and deploy"

Your app will be deployed with a URL like `https://main.xxx.amplifyapp.com`

## License

MIT
