# Design Tokens

Design tokens are the visual design atoms of the design system — specifically, they are named entities that store visual design attributes. We use them in place of hard-coded values to maintain a scalable and consistent visual system.

## 🎨 Color System

### Primary Colors

```css
:root {
  /* Primary Brand Colors */
  --color-primary-50: #eff6ff;
  --color-primary-100: #dbeafe;
  --color-primary-200: #bfdbfe;
  --color-primary-300: #93c5fd;
  --color-primary-400: #60a5fa;
  --color-primary-500: #3b82f6;
  --color-primary-600: #2563eb;
  --color-primary-700: #1d4ed8;
  --color-primary-800: #1e40af;
  --color-primary-900: #1e3a8a;
  --color-primary-950: #172554;
}
```

### Secondary Colors

```css
:root {
  /* Secondary Brand Colors */
  --color-secondary-50: #f8fafc;
  --color-secondary-100: #f1f5f9;
  --color-secondary-200: #e2e8f0;
  --color-secondary-300: #cbd5e1;
  --color-secondary-400: #94a3b8;
  --color-secondary-500: #64748b;
  --color-secondary-600: #475569;
  --color-secondary-700: #334155;
  --color-secondary-800: #1e293b;
  --color-secondary-900: #0f172a;
  --color-secondary-950: #020617;
}
```

### Semantic Colors

```css
:root {
  /* Success Colors */
  --color-success-50: #f0fdf4;
  --color-success-100: #dcfce7;
  --color-success-200: #bbf7d0;
  --color-success-300: #86efac;
  --color-success-400: #4ade80;
  --color-success-500: #22c55e;
  --color-success-600: #16a34a;
  --color-success-700: #15803d;
  --color-success-800: #166534;
  --color-success-900: #14532d;

  /* Warning Colors */
  --color-warning-50: #fffbeb;
  --color-warning-100: #fef3c7;
  --color-warning-200: #fde68a;
  --color-warning-300: #fcd34d;
  --color-warning-400: #fbbf24;
  --color-warning-500: #f59e0b;
  --color-warning-600: #d97706;
  --color-warning-700: #b45309;
  --color-warning-800: #92400e;
  --color-warning-900: #78350f;

  /* Error Colors */
  --color-error-50: #fef2f2;
  --color-error-100: #fee2e2;
  --color-error-200: #fecaca;
  --color-error-300: #fca5a5;
  --color-error-400: #f87171;
  --color-error-500: #ef4444;
  --color-error-600: #dc2626;
  --color-error-700: #b91c1c;
  --color-error-800: #991b1b;
  --color-error-900: #7f1d1d;

  /* Info Colors */
  --color-info-50: #eff6ff;
  --color-info-100: #dbeafe;
  --color-info-200: #bfdbfe;
  --color-info-300: #93c5fd;
  --color-info-400: #60a5fa;
  --color-info-500: #3b82f6;
  --color-info-600: #2563eb;
  --color-info-700: #1d4ed8;
  --color-info-800: #1e40af;
  --color-info-900: #1e3a8a;
}
```

### Neutral Colors

```css
:root {
  /* Neutral Colors */
  --color-neutral-50: #fafafa;
  --color-neutral-100: #f5f5f5;
  --color-neutral-200: #e5e5e5;
  --color-neutral-300: #d4d4d4;
  --color-neutral-400: #a3a3a3;
  --color-neutral-500: #737373;
  --color-neutral-600: #525252;
  --color-neutral-700: #404040;
  --color-neutral-800: #262626;
  --color-neutral-900: #171717;
  --color-neutral-950: #0a0a0a;
}
```

## 📏 Spacing System

### Base Spacing Scale

```css
:root {
  /* Spacing Scale (based on 4px grid) */
  --spacing-0: 0;
  --spacing-1: 0.25rem;  /* 4px */
  --spacing-2: 0.5rem;   /* 8px */
  --spacing-3: 0.75rem;  /* 12px */
  --spacing-4: 1rem;     /* 16px */
  --spacing-5: 1.25rem;  /* 20px */
  --spacing-6: 1.5rem;   /* 24px */
  --spacing-8: 2rem;     /* 32px */
  --spacing-10: 2.5rem;  /* 40px */
  --spacing-12: 3rem;    /* 48px */
  --spacing-16: 4rem;    /* 64px */
  --spacing-20: 5rem;    /* 80px */
  --spacing-24: 6rem;    /* 96px */
  --spacing-32: 8rem;    /* 128px */
  --spacing-40: 10rem;   /* 160px */
  --spacing-48: 12rem;   /* 192px */
  --spacing-56: 14rem;   /* 224px */
  --spacing-64: 16rem;   /* 256px */
}
```

### Semantic Spacing

```css
:root {
  /* Component Spacing */
  --spacing-xs: var(--spacing-1);    /* 4px */
  --spacing-sm: var(--spacing-2);   /* 8px */
  --spacing-md: var(--spacing-4);    /* 16px */
  --spacing-lg: var(--spacing-6);    /* 24px */
  --spacing-xl: var(--spacing-8);    /* 32px */
  --spacing-2xl: var(--spacing-12); /* 48px */
  --spacing-3xl: var(--spacing-16);  /* 64px */

  /* Layout Spacing */
  --spacing-container: var(--spacing-4);
  --spacing-section: var(--spacing-16);
  --spacing-page: var(--spacing-8);
}
```

## 🔤 Typography

### Font Families

```css
:root {
  /* Font Families */
  --font-family-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --font-family-serif: 'Georgia', 'Times New Roman', serif;
  --font-family-mono: 'JetBrains Mono', 'Fira Code', 'Monaco', 'Consolas', monospace;
}
```

### Font Sizes

```css
:root {
  /* Font Sizes */
  --font-size-xs: 0.75rem;    /* 12px */
  --font-size-sm: 0.875rem;   /* 14px */
  --font-size-base: 1rem;     /* 16px */
  --font-size-lg: 1.125rem;   /* 18px */
  --font-size-xl: 1.25rem;    /* 20px */
  --font-size-2xl: 1.5rem;    /* 24px */
  --font-size-3xl: 1.875rem;  /* 30px */
  --font-size-4xl: 2.25rem;   /* 36px */
  --font-size-5xl: 3rem;      /* 48px */
  --font-size-6xl: 3.75rem;   /* 60px */
  --font-size-7xl: 4.5rem;    /* 72px */
  --font-size-8xl: 6rem;      /* 96px */
  --font-size-9xl: 8rem;      /* 128px */
}
```

### Font Weights

```css
:root {
  /* Font Weights */
  --font-weight-thin: 100;
  --font-weight-extralight: 200;
  --font-weight-light: 300;
  --font-weight-normal: 400;
  --font-weight-medium: 500;
  --font-weight-semibold: 600;
  --font-weight-bold: 700;
  --font-weight-extrabold: 800;
  --font-weight-black: 900;
}
```

### Line Heights

```css
:root {
  /* Line Heights */
  --line-height-none: 1;
  --line-height-tight: 1.25;
  --line-height-snug: 1.375;
  --line-height-normal: 1.5;
  --line-height-relaxed: 1.625;
  --line-height-loose: 2;
}
```

### Letter Spacing

```css
:root {
  /* Letter Spacing */
  --letter-spacing-tighter: -0.05em;
  --letter-spacing-tight: -0.025em;
  --letter-spacing-normal: 0em;
  --letter-spacing-wide: 0.025em;
  --letter-spacing-wider: 0.05em;
  --letter-spacing-widest: 0.1em;
}
```

## 🔲 Border Radius

```css
:root {
  /* Border Radius */
  --radius-none: 0;
  --radius-sm: 0.125rem;   /* 2px */
  --radius-base: 0.25rem;   /* 4px */
  --radius-md: 0.375rem;    /* 6px */
  --radius-lg: 0.5rem;      /* 8px */
  --radius-xl: 0.75rem;     /* 12px */
  --radius-2xl: 1rem;       /* 16px */
  --radius-3xl: 1.5rem;     /* 24px */
  --radius-full: 9999px;
}
```

## 🌊 Shadows

```css
:root {
  /* Box Shadows */
  --shadow-xs: 0 1px 2px 0 rgb(0 0 0 / 0.05);
  --shadow-sm: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
  --shadow-base: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
  --shadow-md: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
  --shadow-lg: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
  --shadow-xl: 0 25px 50px -12px rgb(0 0 0 / 0.25);
  --shadow-2xl: 0 25px 50px -12px rgb(0 0 0 / 0.25);
  --shadow-inner: inset 0 2px 4px 0 rgb(0 0 0 / 0.05);
}
```

## ⚡ Transitions

```css
:root {
  /* Transition Durations */
  --duration-75: 75ms;
  --duration-100: 100ms;
  --duration-150: 150ms;
  --duration-200: 200ms;
  --duration-300: 300ms;
  --duration-500: 500ms;
  --duration-700: 700ms;
  --duration-1000: 1000ms;

  /* Transition Timing Functions */
  --ease-linear: linear;
  --ease-in: cubic-bezier(0.4, 0, 1, 1);
  --ease-out: cubic-bezier(0, 0, 0.2, 1);
  --ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
}
```

## 📱 Breakpoints

```css
:root {
  /* Breakpoints */
  --breakpoint-sm: 640px;
  --breakpoint-md: 768px;
  --breakpoint-lg: 1024px;
  --breakpoint-xl: 1280px;
  --breakpoint-2xl: 1536px;
}
```

## 🎭 Z-Index Scale

```css
:root {
  /* Z-Index Scale */
  --z-index-hide: -1;
  --z-index-auto: auto;
  --z-index-base: 0;
  --z-index-docked: 10;
  --z-index-dropdown: 1000;
  --z-index-sticky: 1100;
  --z-index-banner: 1200;
  --z-index-overlay: 1300;
  --z-index-modal: 1400;
  --z-index-popover: 1500;
  --z-index-skipLink: 1600;
  --z-index-toast: 1700;
  --z-index-tooltip: 1800;
}
```

## 🌙 Dark Mode Tokens

```css
[data-theme="dark"] {
  /* Dark Mode Color Overrides */
  --color-primary-50: #1e3a8a;
  --color-primary-100: #1e40af;
  --color-primary-200: #1d4ed8;
  --color-primary-300: #2563eb;
  --color-primary-400: #3b82f6;
  --color-primary-500: #60a5fa;
  --color-primary-600: #93c5fd;
  --color-primary-700: #bfdbfe;
  --color-primary-800: #dbeafe;
  --color-primary-900: #eff6ff;

  /* Background Colors */
  --color-background: var(--color-neutral-900);
  --color-surface: var(--color-neutral-800);
  --color-surface-elevated: var(--color-neutral-700);

  /* Text Colors */
  --color-text-primary: var(--color-neutral-50);
  --color-text-secondary: var(--color-neutral-300);
  --color-text-tertiary: var(--color-neutral-400);
}
```

## 🛠️ Usage Examples

### CSS Custom Properties

```css
.button {
  background-color: var(--color-primary-500);
  color: var(--color-neutral-50);
  padding: var(--spacing-3) var(--spacing-6);
  border-radius: var(--radius-md);
  font-size: var(--font-size-base);
  font-weight: var(--font-weight-medium);
  transition: all var(--duration-200) var(--ease-in-out);
}

.button:hover {
  background-color: var(--color-primary-600);
  box-shadow: var(--shadow-md);
}
```

### JavaScript Usage

```typescript
// Get design token values
const primaryColor = getComputedStyle(document.documentElement)
  .getPropertyValue('--color-primary-500');

// Set design token values
document.documentElement.style.setProperty('--color-primary-500', '#3b82f6');
```

### React Hook

```typescript
// useDesignTokens hook
import { useEffect, useState } from 'react';

export const useDesignTokens = () => {
  const [tokens, setTokens] = useState<Record<string, string>>({});

  useEffect(() => {
    const computedStyle = getComputedStyle(document.documentElement);
    const tokenMap: Record<string, string> = {};

    // Extract all CSS custom properties
    Array.from(computedStyle).forEach(property => {
      if (property.startsWith('--')) {
        tokenMap[property] = computedStyle.getPropertyValue(property);
      }
    });

    setTokens(tokenMap);
  }, []);

  return tokens;
};
```

## 📦 Token Management

### JSON Format

```json
{
  "color": {
    "primary": {
      "50": "#eff6ff",
      "100": "#dbeafe",
      "500": "#3b82f6",
      "900": "#1e3a8a"
    }
  },
  "spacing": {
    "xs": "0.25rem",
    "sm": "0.5rem",
    "md": "1rem",
    "lg": "1.5rem"
  },
  "typography": {
    "fontSize": {
      "sm": "0.875rem",
      "base": "1rem",
      "lg": "1.125rem"
    }
  }
}
```

### TypeScript Types

```typescript
export interface DesignTokens {
  color: {
    primary: Record<string, string>;
    secondary: Record<string, string>;
    neutral: Record<string, string>;
  };
  spacing: Record<string, string>;
  typography: {
    fontSize: Record<string, string>;
    fontWeight: Record<string, number>;
    lineHeight: Record<string, string>;
  };
  borderRadius: Record<string, string>;
  shadow: Record<string, string>;
}
```

## 🔄 Token Updates

### Versioning

- **Major**: Breaking changes to token structure
- **Minor**: New tokens added
- **Patch**: Token value updates

### Migration Guide

When updating tokens:

1. **Document Changes**: List all modified tokens
2. **Provide Migration Script**: Automated token updates
3. **Test Components**: Ensure visual consistency
4. **Update Documentation**: Reflect changes in docs

## 📚 Resources

- [Design Tokens W3C Specification](https://design-tokens.github.io/community-group/format/)
- [Style Dictionary](https://amzn.github.io/style-dictionary/)
- [Theo](https://github.com/salesforce-ux/theo)
- [Design Tokens Community](https://spectrum.chat/design-tokens)
