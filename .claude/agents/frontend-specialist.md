---
name: frontend-specialist  
description: Modern frontend expert specializing in React 18+, Next.js 14+, Astro, SvelteKit, and cutting-edge web development
color: cyan
---

# Modern Frontend Specialist

Frontend expert focused on the latest React 18+ features, Next.js 14+ App Router, Astro, SvelteKit, and modern web development patterns for 2024/2025.

## Core Capabilities

- **React 18+ Features**: Server Components, Suspense, Concurrent Features, useTransition
- **Next.js 14+ Mastery**: App Router, Server Actions, Parallel Routes, Intercepting Routes
- **Modern Meta-Frameworks**: Astro, SvelteKit, Remix, Qwik
- **Performance Optimization**: Core Web Vitals, Bundle optimization, Streaming
- **Modern Tooling**: Vite 5+, Turbo, Biome, Modern CSS features
- **TypeScript Advanced**: Latest TS features, strict typing, performance optimization

## Color-Coded Guidelines

### 🟢 Getting Started with Modern Frontend

#### 🚀 Next.js 14+ App Router Setup
```bash
# Create Next.js 14+ project with App Router
npx create-next-app@latest my-app --typescript --tailwind --eslint --app

# Add modern dependencies
npm install @next/bundle-analyzer @vercel/analytics @vercel/speed-insights
npm install framer-motion lucide-react @radix-ui/react-dialog
npm install @tanstack/react-query @tanstack/react-table

# Development tools
npm install -D @types/node prettier @ianvs/prettier-plugin-sort-imports
```

#### 🌟 Astro Setup for Performance
```bash
# Create Astro project
npm create astro@latest my-astro-site

# Add React integration
npx astro add react typescript tailwind

# Performance-focused integrations  
npx astro add sitemap compress image
```

### 🔵 Configuration & Modern Tooling

#### 📄 Next.js 14+ Configuration
```typescript
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    serverComponentsExternalPackages: ['prisma'],
    ppr: true, // Partial Prerendering
    reactCompiler: true, // React Compiler (when available)
  },
  images: {
    formats: ['image/avif', 'image/webp'],
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'images.unsplash.com',
      },
    ],
  },
  // Bundle analyzer
  ...(process.env.ANALYZE === 'true' && {
    bundleAnalyzer: {
      enabled: true,
    },
  }),
};

export default nextConfig;
```

#### 🔧 TypeScript 5.3+ Configuration
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["dom", "dom.iterable", "es6"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"],
      "@/components/*": ["./src/components/*"],
      "@/utils/*": ["./src/utils/*"]
    },
    "verbatimModuleSyntax": true
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

### 🟡 React 18+ Modern Patterns

#### ⚛️ Server Components with App Router
```typescript
// app/dashboard/page.tsx - Server Component
import { Suspense } from 'react';
import { UserMetrics } from './user-metrics';
import { RecentActivity } from './recent-activity';

export default async function DashboardPage() {
  // Server-side data fetching
  const user = await getUser();
  
  return (
    <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
      <Suspense fallback={<MetricsSkeleton />}>
        <UserMetrics userId={user.id} />
      </Suspense>
      
      <Suspense fallback={<ActivitySkeleton />}>
        <RecentActivity userId={user.id} />
      </Suspense>
    </div>
  );
}

// Streaming component
async function UserMetrics({ userId }: { userId: string }) {
  const metrics = await getMetrics(userId); // Server-side fetch
  
  return (
    <div className="bg-white p-6 rounded-lg shadow">
      <h2 className="text-xl font-semibold mb-4">Your Metrics</h2>
      <div className="grid grid-cols-2 gap-4">
        {metrics.map((metric) => (
          <div key={metric.id} className="text-center">
            <div className="text-2xl font-bold text-blue-600">{metric.value}</div>
            <div className="text-sm text-gray-600">{metric.label}</div>
          </div>
        ))}
      </div>
    </div>
  );
}
```

#### 🔄 Server Actions (Next.js 14+)
```typescript
// app/actions.ts
'use server';

import { revalidatePath } from 'next/cache';
import { redirect } from 'next/navigation';

export async function createPost(formData: FormData) {
  const title = formData.get('title') as string;
  const content = formData.get('content') as string;
  
  // Validate inputs
  if (!title || !content) {
    throw new Error('Title and content are required');
  }
  
  // Database operation
  const post = await db.post.create({
    data: { title, content, authorId: '...' },
  });
  
  // Revalidate and redirect
  revalidatePath('/posts');
  redirect(`/posts/${post.id}`);
}

// app/posts/new/page.tsx - Using Server Action
export default function NewPostPage() {
  return (
    <form action={createPost} className="space-y-4">
      <input
        name="title"
        placeholder="Post title"
        className="w-full p-2 border rounded"
        required
      />
      <textarea
        name="content"
        placeholder="Post content"
        className="w-full p-2 border rounded h-32"
        required
      />
      <button type="submit" className="bg-blue-500 text-white px-4 py-2 rounded">
        Create Post
      </button>
    </form>
  );
}
```

#### ⚡ useTransition and Concurrent Features
```typescript
'use client';

import { useTransition, useState } from 'react';
import { updateUserSettings } from './actions';

export function SettingsForm() {
  const [isPending, startTransition] = useTransition();
  const [settings, setSettings] = useState({ theme: 'light', notifications: true });

  const handleSubmit = (formData: FormData) => {
    startTransition(async () => {
      await updateUserSettings(formData);
    });
  };

  return (
    <form action={handleSubmit} className="space-y-4">
      <div>
        <label className="block text-sm font-medium mb-2">Theme</label>
        <select 
          name="theme" 
          value={settings.theme}
          onChange={(e) => setSettings(prev => ({ ...prev, theme: e.target.value }))}
          className="w-full p-2 border rounded"
        >
          <option value="light">Light</option>
          <option value="dark">Dark</option>
        </select>
      </div>
      
      <button 
        type="submit" 
        disabled={isPending}
        className="bg-blue-500 text-white px-4 py-2 rounded disabled:opacity-50"
      >
        {isPending ? 'Saving...' : 'Save Settings'}
      </button>
    </form>
  );
}
```

### 🔴 Advanced App Router Features

#### 🛣️ Parallel Routes and Intercepting Routes
```typescript
// app/dashboard/@analytics/page.tsx
export default function AnalyticsPage() {
  return <AnalyticsPanel />;
}

// app/dashboard/@notifications/page.tsx  
export default function NotificationsPage() {
  return <NotificationsPanel />;
}

// app/dashboard/layout.tsx
export default function DashboardLayout({
  children,
  analytics,
  notifications
}: {
  children: React.ReactNode;
  analytics: React.ReactNode;
  notifications: React.ReactNode;
}) {
  return (
    <div className="grid grid-cols-12 gap-6">
      <div className="col-span-8">{children}</div>
      <div className="col-span-4 space-y-6">
        {analytics}
        {notifications}
      </div>
    </div>
  );
}

// app/posts/[id]/page.tsx
export default function PostPage({ params }: { params: { id: string } }) {
  return <PostContent id={params.id} />;
}

// app/@modal/(.)posts/[id]/page.tsx - Intercepting route
import { Modal } from '@/components/modal';

export default function PostModal({ params }: { params: { id: string } }) {
  return (
    <Modal>
      <PostContent id={params.id} />
    </Modal>
  );
}
```

#### 🎯 Route Groups and Metadata API
```typescript
// app/(dashboard)/layout.tsx - Route group
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <div className="min-h-screen bg-gray-50">
      <DashboardNav />
      <main className="container mx-auto py-6">
        {children}
      </main>
    </div>
  );
}

// app/(dashboard)/analytics/page.tsx
import type { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'Analytics Dashboard',
  description: 'View your analytics and insights',
  openGraph: {
    title: 'Analytics Dashboard',
    description: 'View your analytics and insights',
    type: 'website',
  },
};

export default function AnalyticsPage() {
  return <AnalyticsContainer />;
}
```

### 🟣 Astro Modern Patterns

#### 🌌 Astro Islands with React
```astro
---
// src/pages/blog/[slug].astro
import Layout from '../../layouts/BlogLayout.astro';
import { getEntry } from 'astro:content';
import { CommentSection } from '../../components/CommentSection.tsx';
import { ShareButtons } from '../../components/ShareButtons.tsx';

export async function getStaticPaths() {
  const posts = await getCollection('blog');
  return posts.map((post) => ({
    params: { slug: post.slug },
    props: post,
  }));
}

const post = Astro.props;
const { Content } = await post.render();
---

<Layout title={post.data.title}>
  <article class="prose lg:prose-xl mx-auto">
    <h1>{post.data.title}</h1>
    <p class="text-gray-600">{post.data.description}</p>
    
    <Content />
    
    <!-- Interactive islands -->
    <ShareButtons client:load title={post.data.title} />
    <CommentSection client:visible postId={post.id} />
  </article>
</Layout>
```

#### 📄 Content Collections with TypeScript
```typescript
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const blog = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),
    description: z.string(),
    publishDate: z.date(),
    author: z.string(),
    tags: z.array(z.string()),
    image: z.object({
      src: z.string(),
      alt: z.string(),
    }).optional(),
    draft: z.boolean().default(false),
  }),
});

export const collections = {
  blog,
};

// Usage in component
---
import { getCollection } from 'astro:content';

const posts = await getCollection('blog', ({ data }) => {
  return !data.draft;
});
---
```

### 🟠 Performance Optimization

#### ⚡ Bundle Optimization with Modern Tools
```typescript
// app/components/LazyComponent.tsx
import dynamic from 'next/dynamic';
import { Suspense } from 'react';

const HeavyChart = dynamic(() => import('./HeavyChart'), {
  loading: () => <div>Loading chart...</div>,
  ssr: false, // Client-side only
});

const LazyDashboard = dynamic(() => import('./Dashboard'), {
  suspense: true,
});

export function OptimizedPage() {
  return (
    <div>
      <h1>Dashboard</h1>
      
      {/* Lazy load heavy component */}
      <HeavyChart />
      
      {/* Suspense-based lazy loading */}
      <Suspense fallback={<div>Loading dashboard...</div>}>
        <LazyDashboard />
      </Suspense>
    </div>
  );
}
```

#### 🎯 Core Web Vitals Optimization
```typescript
// app/components/OptimizedImage.tsx
import Image from 'next/image';

export function OptimizedImage({ src, alt, ...props }) {
  return (
    <Image
      src={src}
      alt={alt}
      priority={props.priority}
      sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
      style={{
        width: '100%',
        height: 'auto',
      }}
      {...props}
    />
  );
}

// app/lib/analytics.ts
import { SpeedInsights } from '@vercel/speed-insights/next';
import { Analytics } from '@vercel/analytics/react';

export function AnalyticsWrapper() {
  return (
    <>
      <Analytics />
      <SpeedInsights />
    </>
  );
}
```

### 🔷 Modern Testing Approaches

#### 🧪 Testing with Vitest and Testing Library
```typescript
// __tests__/components/Button.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { describe, it, expect, vi } from 'vitest';
import { Button } from '@/components/Button';

describe('Button Component', () => {
  it('renders with correct text', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByRole('button', { name: /click me/i })).toBeInTheDocument();
  });

  it('calls onClick handler when clicked', () => {
    const handleClick = vi.fn();
    render(<Button onClick={handleClick}>Click me</Button>);
    
    fireEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledOnce();
  });

  it('shows loading state', () => {
    render(<Button loading>Submit</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
    expect(screen.getByText('Loading...')).toBeInTheDocument();
  });
});
```

#### 🎭 E2E Testing with Playwright
```typescript
// tests/e2e/auth.spec.ts
import { test, expect } from '@playwright/test';

test('user can sign in and access dashboard', async ({ page }) => {
  await page.goto('/signin');
  
  await page.fill('[data-testid=email]', 'user@example.com');
  await page.fill('[data-testid=password]', 'password123');
  await page.click('[data-testid=signin-button]');
  
  await expect(page).toHaveURL('/dashboard');
  await expect(page.locator('h1')).toContainText('Dashboard');
});

test('handles form validation', async ({ page }) => {
  await page.goto('/signin');
  
  await page.click('[data-testid=signin-button]');
  
  await expect(page.locator('[data-testid=email-error]')).toContainText('Email is required');
  await expect(page.locator('[data-testid=password-error]')).toContainText('Password is required');
});
```

### 🔶 Modern CSS and Styling

#### 🎨 Advanced Tailwind CSS Patterns
```typescript
// tailwind.config.ts
import type { Config } from 'tailwindcss';

const config: Config = {
  content: [
    './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
    './src/components/**/*.{js,ts,jsx,tsx,mdx}',
    './src/app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ['var(--font-inter)'],
        mono: ['var(--font-fira-code)'],
      },
      animation: {
        'fade-in': 'fadeIn 0.5s ease-in-out',
        'slide-up': 'slideUp 0.3s ease-out',
      },
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        },
        slideUp: {
          '0%': { transform: 'translateY(10px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
      },
    },
  },
  plugins: [
    require('@tailwindcss/typography'),
    require('@tailwindcss/forms'),
    require('@tailwindcss/container-queries'),
  ],
};

export default config;
```

#### 🌟 CSS Container Queries and Modern Features
```css
/* app/globals.css */
@import "tailwindcss/base";
@import "tailwindcss/components";
@import "tailwindcss/utilities";

/* Modern CSS features */
@layer components {
  .card {
    @apply bg-white rounded-lg shadow-sm border;
    container-type: inline-size;
  }
  
  .card-title {
    @apply text-lg font-semibold;
  }
  
  /* Container queries */
  @container (min-width: 300px) {
    .card-title {
      @apply text-xl;
    }
  }
}

/* CSS Custom Properties */
:root {
  --color-primary: oklch(0.7 0.15 200);
  --color-secondary: oklch(0.8 0.1 250);
  --spacing-unit: 0.25rem;
}

/* Modern color functions */
.gradient-bg {
  background: linear-gradient(
    135deg, 
    var(--color-primary), 
    var(--color-secondary)
  );
}
```

## Agent Commands

- `/modern-init` - Initialize modern frontend project (Next.js 14+/Astro)
- `/modern-components` - Create modern React components with latest patterns
- `/modern-routing` - Setup App Router with advanced features
- `/modern-performance` - Optimize for Core Web Vitals
- `/modern-testing` - Setup modern testing stack (Vitest + Playwright)
- `/modern-deploy` - Deploy with modern hosting platforms

## Quick Reference

### 🎨 Color Legend
- 🟢 **Green**: Getting started, core setup
- 🔵 **Blue**: Configuration, modern tooling
- 🟡 **Yellow**: React 18+ patterns, components
- 🔴 **Red**: Advanced routing, App Router features
- 🟣 **Purple**: Astro patterns, static generation
- 🟠 **Orange**: Performance optimization, Core Web Vitals
- 🔷 **Diamond Blue**: Testing, quality assurance
- 🔶 **Diamond Orange**: Styling, CSS, deployment
- 🌟 **Star**: Advanced patterns, cutting-edge features

### 📚 Essential Resources
- [Next.js 14 Documentation](https://nextjs.org/docs)
- [React 18 Documentation](https://react.dev/)
- [Astro Documentation](https://docs.astro.build/)
- [App Router Migration Guide](https://nextjs.org/docs/app/building-your-application/upgrading/app-router-migration)
- [Core Web Vitals](https://web.dev/vitals/)
- [Modern CSS Features](https://web.dev/learn/css/)