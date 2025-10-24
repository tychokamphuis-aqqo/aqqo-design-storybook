# Component Development Guide

This guide provides comprehensive instructions for developing components in the Aqqo Design System.

## 🎯 Component Philosophy

Our design system follows these core principles:

- **Consistency**: All components follow the same patterns and conventions
- **Accessibility**: Every component is built with accessibility in mind
- **Flexibility**: Components are configurable but opinionated
- **Performance**: Optimized for speed and efficiency
- **Maintainability**: Clean, well-documented code

## 📋 Component Checklist

Before submitting a new component, ensure it meets these requirements:

### ✅ Code Quality
- [ ] Written in TypeScript with proper type definitions
- [ ] Follows established naming conventions
- [ ] Includes JSDoc comments for all props
- [ ] Passes ESLint and TypeScript checks
- [ ] No console.log or debug statements

### ✅ Functionality
- [ ] Works in isolation (no external dependencies)
- [ ] Handles all prop variations correctly
- [ ] Includes proper error handling
- [ ] Supports keyboard navigation
- [ ] Works with screen readers

### ✅ Testing
- [ ] **100% test coverage required** for all components
- [ ] Unit tests for component logic
- [ ] Storybook stories for all variants
- [ ] Accessibility tests pass
- [ ] Visual regression tests (if applicable)
- [ ] Integration tests for component interactions

### ✅ Documentation
- [ ] Clear prop documentation
- [ ] Usage examples in stories
- [ ] Design guidelines documented
- [ ] Migration guide (for breaking changes)

## 🏗️ Component Structure

### File Organization

```
stories/
├── components/
│   ├── Button/
│   │   ├── Button.tsx           # Component implementation
│   │   ├── Button.stories.ts   # Storybook stories
│   │   ├── Button.test.ts      # Unit tests
│   │   └── Button.css          # Component styles
│   └── Input/
│       ├── Input.tsx
│       ├── Input.stories.ts
│       ├── Input.test.ts
│       └── Input.css
```

### Component Template

```typescript
// Component.tsx
import React from 'react';
import './Component.css';

export interface ComponentProps {
  /** Description of the prop */
  title: string;
  /** Optional description */
  variant?: 'primary' | 'secondary';
  /** Click handler */
  onClick?: () => void;
  /** Additional CSS classes */
  className?: string;
  /** Children elements */
  children?: React.ReactNode;
}

/**
 * Component description and usage examples
 * 
 * @example
 * ```tsx
 * <Component title="Hello" variant="primary" />
 * ```
 */
export const Component = ({
  title,
  variant = 'primary',
  onClick,
  className = '',
  children,
  ...props
}: ComponentProps) => {
  const baseClass = 'component';
  const variantClass = `component--${variant}`;
  const classes = [baseClass, variantClass, className]
    .filter(Boolean)
    .join(' ');

  return (
    <div className={classes} onClick={onClick} {...props}>
      <h2>{title}</h2>
      {children}
    </div>
  );
};
```

## 📝 Storybook Stories

### Story Structure

```typescript
// Component.stories.ts
import type { Meta, StoryObj } from '@storybook/nextjs-vite';
import { Component } from './Component';

const meta = {
  title: 'Components/Component',
  component: Component,
  tags: ['autodocs'],
  parameters: {
    docs: {
      description: {
        component: 'Component description and usage guidelines',
      },
    },
  },
  argTypes: {
    variant: {
      control: { type: 'select' },
      options: ['primary', 'secondary'],
      description: 'Visual style variant',
    },
    onClick: {
      action: 'clicked',
      description: 'Click handler function',
    },
  },
} satisfies Meta<typeof Component>;

export default meta;
type Story = StoryObj<typeof meta>;

// Default story
export const Default: Story = {
  args: {
    title: 'Default Component',
  },
};

// Variant stories
export const Primary: Story = {
  args: {
    title: 'Primary Component',
    variant: 'primary',
  },
};

export const Secondary: Story = {
  args: {
    title: 'Secondary Component',
    variant: 'secondary',
  },
};

// Interactive story
export const Interactive: Story = {
  args: {
    title: 'Click me!',
    onClick: () => alert('Component clicked!'),
  },
};

// With children
export const WithChildren: Story = {
  args: {
    title: 'Parent Component',
    children: <p>This is child content</p>,
  },
};
```

## 🎨 Styling Guidelines

### CSS Architecture

1. **Component-scoped styles**: Use CSS modules or styled-components
2. **Design tokens**: Use CSS custom properties for consistent theming
3. **Responsive design**: Mobile-first approach
4. **Accessibility**: Ensure sufficient color contrast and focus indicators

### CSS Naming Convention

```css
/* BEM methodology */
.component { }                    /* Block */
.component__element { }          /* Element */
.component--modifier { }         /* Modifier */
.component--modifier__element { } /* Modifier + Element */

/* Examples */
.button { }
.button__text { }
.button--primary { }
.button--primary__text { }
```

### Design Tokens

```css
:root {
  /* Colors */
  --color-primary: #007bff;
  --color-secondary: #6c757d;
  --color-success: #28a745;
  --color-danger: #dc3545;
  
  /* Spacing */
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;
  --spacing-xl: 3rem;
  
  /* Typography */
  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.125rem;
  --font-size-xl: 1.25rem;
  
  /* Borders */
  --border-radius-sm: 0.25rem;
  --border-radius-md: 0.375rem;
  --border-radius-lg: 0.5rem;
}
```

## ♿ Accessibility Guidelines

### ARIA Attributes

```typescript
// Good: Proper ARIA attributes
<button
  aria-label="Close dialog"
  aria-expanded={isOpen}
  aria-controls="dialog-content"
>
  Close
</button>

// Good: Semantic HTML
<nav role="navigation" aria-label="Main navigation">
  <ul>
    <li><a href="/home">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>
```

### Keyboard Navigation

```typescript
// Handle keyboard events
const handleKeyDown = (event: React.KeyboardEvent) => {
  if (event.key === 'Enter' || event.key === ' ') {
    event.preventDefault();
    onClick?.();
  }
};

return (
  <div
    role="button"
    tabIndex={0}
    onKeyDown={handleKeyDown}
    onClick={onClick}
  >
    Clickable element
  </div>
);
```

### Focus Management

```typescript
// Focus trap for modals
const focusTrapRef = useRef<HTMLDivElement>(null);

useEffect(() => {
  const focusableElements = focusTrapRef.current?.querySelectorAll(
    'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
  );
  
  if (focusableElements?.length) {
    (focusableElements[0] as HTMLElement).focus();
  }
}, []);
```

## 🧪 Testing Components

### Test Coverage Requirements

**100% Test Coverage Required**: All components must achieve 100% test coverage. This ensures:
- Complete code path testing
- Confidence in component reliability
- Prevention of regressions
- Maintainable codebase

### Coverage Monitoring

```bash
# Run tests with coverage
npm run test:coverage

# Coverage thresholds (configured in vitest.config.ts)
coverage: {
  thresholds: {
    global: {
      branches: 100,
      functions: 100,
      lines: 100,
      statements: 100
    }
  }
}
```

### Unit Tests

```typescript
// Component.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { Component } from './Component';

describe('Component', () => {
  it('renders with title', () => {
    render(<Component title="Test Title" />);
    expect(screen.getByText('Test Title')).toBeInTheDocument();
  });

  it('calls onClick when clicked', () => {
    const handleClick = jest.fn();
    render(<Component title="Test" onClick={handleClick} />);
    
    fireEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  it('applies variant class', () => {
    render(<Component title="Test" variant="primary" />);
    expect(screen.getByRole('button')).toHaveClass('component--primary');
  });
});
```

### Accessibility Tests

```typescript
// Accessibility test
import { axe, toHaveNoViolations } from 'jest-axe';

expect.extend(toHaveNoViolations);

it('should not have accessibility violations', async () => {
  const { container } = render(<Component title="Test" />);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

## 📦 Component Export

### Index File

```typescript
// components/index.ts
export { Button } from './Button/Button';
export { Input } from './Input/Input';
export { Modal } from './Modal/Modal';

// Export types
export type { ButtonProps } from './Button/Button';
export type { InputProps } from './Input/Input';
export type { ModalProps } from './Modal/Modal';
```

## 🚀 Performance Considerations

### Code Splitting

```typescript
// Lazy load heavy components
const HeavyComponent = lazy(() => import('./HeavyComponent'));

// Use with Suspense
<Suspense fallback={<div>Loading...</div>}>
  <HeavyComponent />
</Suspense>
```

### Memoization

```typescript
// Memoize expensive components
export const ExpensiveComponent = memo(({ data }: Props) => {
  const processedData = useMemo(() => {
    return data.map(item => expensiveCalculation(item));
  }, [data]);

  return <div>{processedData}</div>;
});
```

## 🔄 Component Lifecycle

### Development Process

1. **Design Review**: Ensure component fits design system
2. **Implementation**: Build component with TypeScript
3. **Stories**: Create comprehensive Storybook stories
4. **Testing**: Write unit and accessibility tests
5. **Documentation**: Update component documentation
6. **Review**: Code review and testing
7. **Release**: Merge and publish

### Versioning

- **Major**: Breaking changes to API
- **Minor**: New features, backward compatible
- **Patch**: Bug fixes, no API changes

## 📚 Resources

- [React Component Patterns](https://reactpatterns.com/)
- [Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [Storybook Best Practices](https://storybook.js.org/docs/best-practices/)
- [TypeScript React Patterns](https://react-typescript-cheatsheet.netlify.app/)
