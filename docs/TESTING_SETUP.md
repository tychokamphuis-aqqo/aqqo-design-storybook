# Testing Setup Guide

This guide covers the testing configuration and requirements for the Aqqo Design System, including the mandatory 100% test coverage requirement.

## 🎯 Test Coverage Requirements

### 100% Coverage Mandate

All components in the design system must achieve **100% test coverage**. This includes:

- **Statements**: 100% of code statements must be executed
- **Branches**: 100% of conditional branches must be tested
- **Functions**: 100% of functions must be called
- **Lines**: 100% of code lines must be executed

## ⚙️ Configuration

### Vitest Configuration

```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'jsdom',
    setupFiles: ['./src/test/setup.ts'],
    coverage: {
      provider: 'v8',
      reporter: ['text', 'json', 'html'],
      exclude: [
        'node_modules/',
        'src/test/',
        '**/*.d.ts',
        '**/*.config.*',
        '**/stories/**',
        '**/*.stories.*',
      ],
      thresholds: {
        global: {
          branches: 100,
          functions: 100,
          lines: 100,
          statements: 100,
        },
      },
    },
  },
});
```

### Test Setup File

```typescript
// src/test/setup.ts
import '@testing-library/jest-dom';
import { expect, afterEach } from 'vitest';
import { cleanup } from '@testing-library/react';

// Extend Vitest's expect with jest-dom matchers
expect.extend({});

// Cleanup after each test
afterEach(() => {
  cleanup();
});
```

## 📋 Package.json Scripts

```json
{
  "scripts": {
    "test": "vitest",
    "test:watch": "vitest --watch",
    "test:coverage": "vitest --coverage",
    "test:ui": "vitest --ui",
    "test:run": "vitest run",
    "test:coverage:run": "vitest run --coverage"
  }
}
```

## 🧪 Testing Libraries

### Required Dependencies

```json
{
  "devDependencies": {
    "@testing-library/react": "^14.0.0",
    "@testing-library/jest-dom": "^6.0.0",
    "@testing-library/user-event": "^14.0.0",
    "@vitest/coverage-v8": "^1.0.0",
    "@vitest/ui": "^1.0.0",
    "jsdom": "^23.0.0",
    "vitest": "^1.0.0"
  }
}
```

## 📝 Component Testing Examples

### Basic Component Test

```typescript
// Button.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { Button } from './Button';

describe('Button Component', () => {
  it('renders with default props', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByRole('button')).toBeInTheDocument();
  });

  it('renders with custom text', () => {
    render(<Button>Custom Text</Button>);
    expect(screen.getByText('Custom Text')).toBeInTheDocument();
  });

  it('applies primary variant class', () => {
    render(<Button variant="primary">Primary</Button>);
    expect(screen.getByRole('button')).toHaveClass('button--primary');
  });

  it('applies secondary variant class', () => {
    render(<Button variant="secondary">Secondary</Button>);
    expect(screen.getByRole('button')).toHaveClass('button--secondary');
  });

  it('applies size classes correctly', () => {
    render(<Button size="large">Large</Button>);
    expect(screen.getByRole('button')).toHaveClass('button--large');
  });

  it('handles click events', () => {
    const handleClick = vi.fn();
    render(<Button onClick={handleClick}>Click me</Button>);
    
    fireEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  it('is disabled when disabled prop is true', () => {
    render(<Button disabled>Disabled</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
  });

  it('does not call onClick when disabled', () => {
    const handleClick = vi.fn();
    render(<Button disabled onClick={handleClick}>Disabled</Button>);
    
    fireEvent.click(screen.getByRole('button'));
    expect(handleClick).not.toHaveBeenCalled();
  });

  it('supports keyboard navigation', () => {
    const handleClick = vi.fn();
    render(<Button onClick={handleClick}>Keyboard</Button>);
    
    const button = screen.getByRole('button');
    fireEvent.keyDown(button, { key: 'Enter' });
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  it('applies custom className', () => {
    render(<Button className="custom-class">Custom</Button>);
    expect(screen.getByRole('button')).toHaveClass('custom-class');
  });

  it('forwards ref correctly', () => {
    const ref = vi.fn();
    render(<Button ref={ref}>Ref test</Button>);
    expect(ref).toHaveBeenCalled();
  });
});
```

### Complex Component Test

```typescript
// Modal.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { Modal } from './Modal';

describe('Modal Component', () => {
  const defaultProps = {
    isOpen: true,
    onClose: vi.fn(),
    title: 'Test Modal',
  };

  it('renders when open', () => {
    render(<Modal {...defaultProps}>Modal content</Modal>);
    expect(screen.getByText('Test Modal')).toBeInTheDocument();
    expect(screen.getByText('Modal content')).toBeInTheDocument();
  });

  it('does not render when closed', () => {
    render(<Modal {...defaultProps} isOpen={false}>Modal content</Modal>);
    expect(screen.queryByText('Modal content')).not.toBeInTheDocument();
  });

  it('calls onClose when close button is clicked', async () => {
    const user = userEvent.setup();
    const onClose = vi.fn();
    render(<Modal {...defaultProps} onClose={onClose}>Modal content</Modal>);
    
    await user.click(screen.getByRole('button', { name: /close/i }));
    expect(onClose).toHaveBeenCalledTimes(1);
  });

  it('calls onClose when escape key is pressed', async () => {
    const user = userEvent.setup();
    const onClose = vi.fn();
    render(<Modal {...defaultProps} onClose={onClose}>Modal content</Modal>);
    
    await user.keyboard('{Escape}');
    expect(onClose).toHaveBeenCalledTimes(1);
  });

  it('calls onClose when backdrop is clicked', async () => {
    const user = userEvent.setup();
    const onClose = vi.fn();
    render(<Modal {...defaultProps} onClose={onClose}>Modal content</Modal>);
    
    await user.click(screen.getByTestId('modal-backdrop'));
    expect(onClose).toHaveBeenCalledTimes(1);
  });

  it('does not call onClose when modal content is clicked', async () => {
    const user = userEvent.setup();
    const onClose = vi.fn();
    render(<Modal {...defaultProps} onClose={onClose}>Modal content</Modal>);
    
    await user.click(screen.getByTestId('modal-content'));
    expect(onClose).not.toHaveBeenCalled();
  });

  it('traps focus within modal', () => {
    render(<Modal {...defaultProps}>Modal content</Modal>);
    const modal = screen.getByRole('dialog');
    expect(modal).toHaveAttribute('aria-modal', 'true');
  });

  it('restores focus when closed', () => {
    const triggerButton = document.createElement('button');
    document.body.appendChild(triggerButton);
    triggerButton.focus();
    
    const { rerender } = render(<Modal {...defaultProps}>Modal content</Modal>);
    rerender(<Modal {...defaultProps} isOpen={false}>Modal content</Modal>);
    
    expect(document.activeElement).toBe(triggerButton);
    document.body.removeChild(triggerButton);
  });
});
```

## 🎭 Storybook Testing

### Story Testing

```typescript
// Button.stories.test.ts
import { expect, test } from '@storybook/test';
import { composeStories } from '@storybook/react';
import { render, screen } from '@testing-library/react';
import * as stories from './Button.stories';

const { Primary, Secondary, Disabled } = composeStories(stories);

describe('Button Stories', () => {
  test('Primary story renders correctly', () => {
    render(<Primary />);
    expect(screen.getByRole('button')).toBeInTheDocument();
    expect(screen.getByRole('button')).toHaveClass('button--primary');
  });

  test('Secondary story renders correctly', () => {
    render(<Secondary />);
    expect(screen.getByRole('button')).toBeInTheDocument();
    expect(screen.getByRole('button')).toHaveClass('button--secondary');
  });

  test('Disabled story renders correctly', () => {
    render(<Disabled />);
    expect(screen.getByRole('button')).toBeDisabled();
  });
});
```

### Interaction Testing

```typescript
// Button.interaction.test.ts
import { expect, userEvent, within } from '@storybook/test';

export const ClickInteraction = {
  play: async ({ canvasElement }) => {
    const canvas = within(canvasElement);
    const button = canvas.getByRole('button');
    
    await userEvent.click(button);
    // Add assertions for expected behavior
  },
};

export const KeyboardInteraction = {
  play: async ({ canvasElement }) => {
    const canvas = within(canvasElement);
    const button = canvas.getByRole('button');
    
    await userEvent.keyboard('{Enter}');
    await userEvent.keyboard(' ');
    // Test all keyboard interactions
  },
};
```

## ♿ Accessibility Testing

### A11y Test Setup

```typescript
// a11y.test.tsx
import { render } from '@testing-library/react';
import { axe, toHaveNoViolations } from 'jest-axe';
import { Button } from './Button';

expect.extend(toHaveNoViolations);

describe('Button Accessibility', () => {
  it('should not have accessibility violations', async () => {
    const { container } = render(<Button>Accessible Button</Button>);
    const results = await axe(container);
    expect(results).toHaveNoViolations();
  });

  it('should be keyboard accessible', () => {
    render(<Button>Keyboard Accessible</Button>);
    const button = screen.getByRole('button');
    expect(button).toHaveAttribute('tabIndex', '0');
  });

  it('should have proper ARIA attributes', () => {
    render(<Button aria-label="Custom label">Button</Button>);
    expect(screen.getByRole('button')).toHaveAttribute('aria-label', 'Custom label');
  });
});
```

## 🚀 CI/CD Integration

### GitHub Actions

```yaml
# .github/workflows/test.yml
name: Test Coverage

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
      
      - run: npm ci
      - run: npm run test:coverage:run
      
      - name: Upload coverage to Codecov
        uses: codecov/codecov-action@v3
        with:
          file: ./coverage/lcov.info
          flags: unittests
          name: codecov-umbrella
```

### Pre-commit Hooks

```json
// package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "npm run test:coverage:run"
    }
  }
}
```

## 📊 Coverage Reports

### HTML Coverage Report

```bash
# Generate HTML coverage report
npm run test:coverage

# Open coverage report
open coverage/index.html
```

### Coverage Badge

```markdown
![Coverage](https://img.shields.io/badge/coverage-100%25-brightgreen)
```

## 🔍 Coverage Analysis

### Understanding Coverage Metrics

- **Statements**: Individual executable statements
- **Branches**: Conditional branches (if/else, switch cases)
- **Functions**: Function declarations and expressions
- **Lines**: Physical lines of code

### Coverage Gaps

Common areas that need attention:

1. **Error Boundaries**: Test error states
2. **Edge Cases**: Test boundary conditions
3. **Async Operations**: Test loading and error states
4. **Conditional Rendering**: Test all render paths
5. **Event Handlers**: Test all user interactions

## 📚 Best Practices

### Test Organization

```
src/
├── components/
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── Button.test.tsx
│   │   ├── Button.stories.ts
│   │   └── Button.stories.test.ts
```

### Test Naming

```typescript
// Good: Descriptive test names
describe('Button Component', () => {
  it('should render with primary variant when variant prop is primary', () => {
    // test implementation
  });
  
  it('should call onClick handler when button is clicked', () => {
    // test implementation
  });
});

// Bad: Vague test names
describe('Button', () => {
  it('works', () => {
    // test implementation
  });
});
```

### Test Structure

```typescript
// AAA Pattern: Arrange, Act, Assert
describe('Component', () => {
  it('should do something', () => {
    // Arrange
    const props = { /* test props */ };
    
    // Act
    render(<Component {...props} />);
    
    // Assert
    expect(screen.getByText('Expected text')).toBeInTheDocument();
  });
});
```

## 🚨 Common Pitfalls

### Avoiding These Mistakes

1. **Testing Implementation Details**: Focus on behavior, not implementation
2. **Over-mocking**: Only mock what's necessary
3. **Incomplete Coverage**: Ensure all code paths are tested
4. **Ignoring Edge Cases**: Test boundary conditions
5. **Poor Test Isolation**: Each test should be independent

## 📖 Resources

- [Vitest Documentation](https://vitest.dev/)
- [Testing Library Documentation](https://testing-library.com/)
- [Jest DOM Matchers](https://github.com/testing-library/jest-dom)
- [Accessibility Testing Guide](https://testing-library.com/docs/guide-which-query)
- [Storybook Testing](https://storybook.js.org/docs/writing-tests)
