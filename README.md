# Aganitha Starter App

A comprehensive starter kit for Next.js applications that provides customizable authentication UI with social login options, email OTP authentication, LDAP authentication, middleware for protected routes, and an integrated navigation bar component.

## Features

### Authentication Component
- 🔐 Built-in support for Google, GitHub, and LinkedIn authentication
- 📧 Email OTP authentication for passwordless login
- 🔑 LDAP authentication for enterprise environments
- 🎨 Fully customizable with Tailwind CSS
- 🚀 CLI tool for automatic setup and configuration
- 📦 Easy to install and integrate

### Navigation Bar Component
- 📱 Responsive navigation bar with mobile menu support
- 📋 Dropdown menu support for nested navigation items
- 🎨 Fixed styling to ensure a consistent look across projects
- 🎭 Color theming via CSS variables
- 📝 TypeScript support for type-safe props
- 📜 Scroll-aware behavior (hides on scroll down, shows on scroll up)

## Installation

```bash
# Run the setup wizard
npx aganitha-starter-app
```

## Quick Start Guide

### Option 1: Create a New Next.js Project with Aganitha Starter App

Running `npx aganitha-starter-app` without an existing Next.js project will:
1. Create a new Next.js application
2. Install and configure authentication components
3. Set up necessary files and environment variables
4. Install the Aganitha Nav Bar component

```bash
npx aganitha-starter-app
```

The setup wizard will guide you through the installation process.

### Option 2: Add Aganitha Starter App to an Existing Next.js Project

If you already have a Next.js project:

```bash
# Navigate to your project
cd your-nextjs-project

# Run the setup wizard
npx aganitha-starter-app
```

## What the Setup Wizard Does

The Aganitha Starter App setup wizard performs the following tasks:

1. **Creates Authentication Routes**:
   - Sets up NextAuth route at `app/api/auth/[...nextauth]/route.ts`
   - Creates OTP authentication endpoints:
     - `/api/auth/request-otp`
     - `/api/auth/verify-otp`

2. **Adds Middleware**:
   - Creates a `middleware.ts` file for route protection
   - Configures protected routes and authentication redirects

3. **Sets Up Utility Files**:
   - `utils/auth.ts` - Authentication helper functions
   - `utils/db.ts` - Database utilities for OTP storage
   - `utils/email.ts` - Email sending functionality for OTP

4. **Creates App Files**:
   - Creates or updates `app/layout.tsx` (existing files are renamed to `layout.old.tsx`)
   - Creates `app/login/page.tsx` with pre-configured AuthLogin component
   - Installs and configures the Aganitha Nav Bar component

5. **Configures Environment Variables**:
   - Creates or updates `.env` file with necessary configuration

6. **Handles File Conflicts**:
   - If files already exist, they are renamed to `{filename}.old.{extension}`
   - Preserves your existing code while adding new functionality

## Authentication Methods

### Social Authentication

Aganitha Starter App supports the following social authentication providers:

- **Google** - OAuth 2.0 authentication with Google accounts
- **GitHub** - OAuth authentication with GitHub accounts
- **LinkedIn** - OAuth authentication with LinkedIn accounts

### Email OTP Authentication

Passwordless authentication using one-time passwords sent via email:

1. User enters their email address
2. A one-time code is sent to their email
3. User enters the code to authenticate
4. A session is created upon successful verification

### LDAP Authentication

Enterprise authentication using LDAP protocol:

1. User enters their username and password
2. The credentials are verified against your LDAP server
3. A session is created upon successful authentication
4. User is redirected to the dashboard

## Using the AuthLogin Component

```jsx
"use client"

import { AuthLogin } from 'aganitha-starter-app';

export default function LoginPage() {
  return (
    <AuthLogin
      redirectUrl="/dashboard"
      logoUrl="/your-logo.svg"
      title="Welcome Back"
      subtitle="Sign in to continue"
      showGoogle={true}
      showGithub={true}
      showLinkedin={true}
      showOTP={true}
      showLDAP={true}
      ldapDomain="example.com"
      buttonClassName="custom-button-class"
      containerClassName="custom-container-class"
    />
  );
}
```

### AuthLogin Component Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `className` | string | "" | Additional CSS classes for the root element |
| `redirectUrl` | string | "/" | URL to redirect after successful login |
| `title` | string | "Welcome to Aganitha" | Main title text |
| `subtitle` | string | "You can sign in using your preferred login method" | Subtitle text |
| `showGoogle` | boolean | true | Toggle Google login button |
| `showGithub` | boolean | true | Toggle GitHub login button |
| `showLinkedin` | boolean | true | Toggle LinkedIn login button |
| `showOTP` | boolean | true | Toggle Email OTP authentication |
| `showLDAP` | boolean | false | Toggle LDAP authentication |
| `ldapDomain` | string | "" | Domain to display for LDAP login (e.g., "example.com") |
| `buttonClassName` | string | "" | Additional CSS classes for buttons |
| `containerClassName` | string | "" | Additional CSS classes for container |
| `termsUrl` | string | "#" | URL to terms of service |
| `privacyUrl` | string | "#" | URL to privacy policy |
| `logoUrl` | string | "https://www.aganitha.ai/wp-content/uploads/2023/07/logo-crop.svg" | URL to your logo |
| `logoClassName` | string | "" | Additional CSS classes for logo |

## Using the Aganitha Nav Bar Component

The Aganitha Nav Bar is automatically installed as part of the Aganitha Starter App. You can use it in your pages or layouts:

```tsx
// app/layout.tsx
import { NavBar } from 'aganitha-nav-bar';
import Link from 'next/link';
import { ArrowRight } from 'lucide-react';

// Navigation configuration
const navItems = [
  { label: 'Home', path: '#hero' },
  {
    label: 'About',
    path: '#about',
    dropdown: [
      { label: 'Our Team', path: '#team' },
      { label: 'Our Mission', path: '#mission' }
    ]
  },
  { label: 'Features', path: '#features' },
  { label: 'Contact', path: '#contact' }
];

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  const handleNavigate = (path: string) => {
    console.log(`Navigating to ${path}`);
  };

  return (
    <html lang="en">
      <body>
        <NavBar
          logoUrl="https://www.aganitha.ai/wp-content/uploads/2023/05/aganitha-logo.png"
          appName="Aganitha"
          navItems={navItems}
          onNavigate={handleNavigate}
          button={
            <Link
              href="/login"
              className="group flex items-center px-4 py-2 bg-[var(--primary)] text-[var(--primary-foreground)] rounded-full hover:bg-[var(--primary)] hover:opacity-80 transition-opacity duration-150 shadow-md"
            >
              Login
              <ArrowRight className="ml-2 h-4 w-4" />
            </Link>
          }
          colors={{
            background: "var(--background)",
            foreground: "var(--foreground)",
            primary: "var(--primary)",
            primaryForeground: "var(--primary-foreground)",
          }}
        />
        {children}
      </body>
    </html>
  );
}
```

### NavBar Component Props

| Prop | Type | Description | Default |
|------|------|-------------|---------|
| appName | string | The name of the application to display next to the logo. | undefined |
| logoUrl | string | URL of the logo image to display. Supports both external and local URLs. | undefined |
| navItems | NavItem[] | Array of navigation items. Supports dropdowns. See NavItem type below. | [] |
| onNavigate | (path: string) => void | Callback function triggered on navigation item click. | undefined |
| button | React.ReactNode | Custom button to display on the right side of the nav bar. | undefined |
| colors | ColorProps | Object to specify CSS variable names for theming. See ColorProps below. | { background: "var(--background)", foreground: "var(--foreground)", primary: "var(--primary)", primaryForeground: "var(--primary-foreground)" } |

### NavItem Type

```tsx
interface NavItem {
  label: string;
  path?: string;
  dropdown?: DropdownItem[];
  type?: string;
  hidden?: boolean;
}

interface DropdownItem {
  label: string;
  path: string;
}
```

### ColorProps Type

The colors prop allows you to specify CSS variable names for theming. Only the variable names (e.g., var(--background)) should be provided; additional styling is not allowed.

```tsx
interface ColorProps {
  background?: string;        // e.g., "var(--background)"
  foreground?: string;        // e.g., "var(--foreground)"
  primary?: string;           // e.g., "var(--primary)"
  primaryForeground?: string; // e.g., "var(--primary-foreground)"
}
```

## Route Protection with Middleware

Aganitha Starter App includes a middleware configuration that protects routes based on authentication status:

```typescript
// middleware.ts (automatically created by setup wizard)
export const config = {
  matcher: ['/', '/dashboard/:path*', '/profile/:path*']
};
```

You can customize the protected routes by modifying the `matcher` array.


## Environment Configuration

Update your `.env` file with your OAuth credentials and LDAP configuration:

```
# Authentication
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-key-here

# Google OAuth
GOOGLE_ID=your-google-client-id
GOOGLE_SECRET=your-google-client-secret

# GitHub OAuth
GITHUB_ID=your-github-client-id
GITHUB_SECRET=your-github-client-secret

# LinkedIn OAuth
LINKEDIN_CLIENT_ID=your-linkedin-client-id
LINKEDIN_CLIENT_SECRET=your-linkedin-client-secret

# Email (for OTP)
EMAIL_SERVER=smtp://username:password@smtp.example.com:587
EMAIL_FROM=noreply@example.com

# LDAP Configuration
LDAP_URI=ldap://ldap.example.com
LDAP_USER_DN=ou=people,dc=example,dc=com
LDAP_EMAIL_DOMAIN=example.com
```

## Advanced Usage

### Custom Email Templates

You can customize the OTP email template by modifying the `utils/email.ts` file:

```typescript
// Customize the email content and styling
const html = `
  <div style="...">
    <h1>Your Authentication Code</h1>
    <p>Your one-time password is: <strong>${otp}</strong></p>
    <p>This code will expire in 10 minutes.</p>
  </div>
`;
```

### Database Integration

By default, Aganitha Starter App uses a SQLite database for OTP storage. You can customize the database configuration in `utils/db.ts`.

### Styling Customization

Components are built with Tailwind CSS and are customizable through props:

- Use the `className`, `buttonClassName`, and `containerClassName` props for AuthLogin
- Use the `colors` prop for NavBar to customize the color theme
- All components use a modern, responsive design that adapts to different screen sizes

## Requirements

- Next.js 13+ (App Router)
- React 18+
- Node.js 16+
- Tailwind CSS 3+
- lucide-react (for icons)

## Troubleshooting

### File Conflicts

If you encounter file conflicts during setup, Aganitha Starter App will rename existing files to `{filename}.old.{extension}` and create new ones. You can:

1. Compare the old and new files to merge your changes
2. Delete the `.old` files once you've verified everything works

### OAuth Configuration

For social login to work correctly:

1. Create OAuth applications with the respective providers
2. Configure the correct redirect URIs:
   - Google: `https://your-domain.com/api/auth/callback/google`
   - GitHub: `https://your-domain.com/api/auth/callback/github`
   - LinkedIn: `https://your-domain.com/api/auth/callback/linkedin`

## License

MIT License © Aganitha
