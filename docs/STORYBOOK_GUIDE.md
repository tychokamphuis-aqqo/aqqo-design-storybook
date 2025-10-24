# Storybook Guide

This guide covers how to use Storybook effectively in the Aqqo Design System for component development, documentation, and testing.

## 🎯 What is Storybook?

Storybook is a tool for building UI components and pages in isolation. It allows you to:

- Develop components in isolation
- Document component APIs and usage
- Test components in different states
- Share components with your team
- Catch visual regressions

## 🚀 Getting Started

### Starting Storybook

```bash
# Development mode
npm run storybook

# Build static version
npm run build-storybook
```

Storybook will be available at `http://localhost:6006`

## 📖 Understanding Stories

### What are Stories?

Stories are functions that return a component in a specific state. Each story represents a single use case or variation of a component.

```typescript
// Button.stories.ts
export const Primary: Story = {
  args: {
    primary: true,
    label: 'Button',
  },
};
```

### Story Structure

```typescript
import type { Meta, StoryObj } from '@storybook/nextjs-vite';
import { Button } from './Button';

// Meta configuration
const meta = {
  title: 'Components/Button',        // Story hierarchy
  component: Button,                // Component to document
  tags: ['autodocs'],               // Auto-generate docs
  parameters: {                     // Story parameters
    layout: 'centered',             // Layout configuration
  },
  argTypes: {                       // Control configuration
    backgroundColor: { control: 'color' },
  },
} satisfies Meta<typeof Button>;

export default meta;
type Story = StoryObj<typeof meta>;

// Individual stories
export const Primary: Story = {
  args: {
    primary: true,
    label: 'Button',
  },
};
```

## 🎨 Story Organization

### Naming Convention

```
Components/
├── Button/
│   ├── Default
│   ├── Primary
│   ├── Secondary
│   └── Disabled
├── Input/
│   ├── Default
│   ├── With Label
│   ├── Error State
│   └── Disabled
└── Modal/
    ├── Default
    ├── Large
    └── With Actions
```

### Story Categories

- **Components**: Core UI components
- **Layout**: Layout and structural components
- **Forms**: Form-related components
- **Navigation**: Navigation components
- **Feedback**: Alerts, notifications, loading states
- **Data Display**: Tables, lists, cards

## 📝 Writing Effective Stories

### Story Best Practices

1. **Show Real Use Cases**: Stories should represent actual usage scenarios
2. **Cover All States**: Include loading, error, empty, and success states
3. **Use Meaningful Names**: Story names should describe the state or use case
4. **Include Interactions**: Show how components respond to user actions

### Example: Comprehensive Button Stories

```typescript
// Button.stories.ts
export const Default: Story = {
  args: {
    label: 'Button',
  },
};

export const Primary: Story = {
  args: {
    primary: true,
    label: 'Primary Button',
  },
};

export const Secondary: Story = {
  args: {
    label: 'Secondary Button',
  },
};

export const Large: Story = {
  args: {
    size: 'large',
    label: 'Large Button',
  },
};

export const Small: Story = {
  args: {
    size: 'small',
    label: 'Small Button',
  },
};

export const Disabled: Story = {
  args: {
    disabled: true,
    label: 'Disabled Button',
  },
};

export const WithIcon: Story = {
  args: {
    label: 'Button with Icon',
    icon: 'arrow-right',
  },
};

export const Loading: Story = {
  args: {
    label: 'Loading Button',
    loading: true,
  },
};
```

## 🎛️ Controls and Interactions

### Controls

Controls allow you to interact with component props in real-time:

```typescript
const meta = {
  argTypes: {
    variant: {
      control: { type: 'select' },
      options: ['primary', 'secondary', 'danger'],
      description: 'Button variant',
    },
    size: {
      control: { type: 'select' },
      options: ['small', 'medium', 'large'],
      description: 'Button size',
    },
    disabled: {
      control: 'boolean',
      description: 'Disable the button',
    },
    backgroundColor: {
      control: 'color',
      description: 'Custom background color',
    },
  },
};
```

### Actions

Actions capture events and display them in the Actions panel:

```typescript
import { fn } from 'storybook/test';

const meta = {
  args: {
    onClick: fn(), // Captures click events
    onSubmit: fn(), // Captures form submissions
  },
};
```

### Decorators

Decorators wrap stories with additional functionality:

```typescript
// Theme decorator
const withTheme = (Story, context) => {
  const theme = context.globals.theme;
  return (
    <ThemeProvider theme={theme}>
      <Story />
    </ThemeProvider>
  );
};

export const parameters = {
  decorators: [withTheme],
};
```

## 📚 Documentation

### Auto-generated Docs

Enable automatic documentation generation:

```typescript
const meta = {
  tags: ['autodocs'], // Enables auto-generated docs
  parameters: {
    docs: {
      description: {
        component: 'A reusable button component with multiple variants and sizes.',
      },
    },
  },
};
```

### Custom Documentation

Create custom documentation pages:

```typescript
// Button.mdx
import { Meta, Story, Canvas, Controls } from '@storybook/blocks';
import { Button } from './Button';

<Meta title="Components/Button" component={Button} />

# Button Component

The Button component is used for user interactions and actions.

## Usage

```tsx
<Button variant="primary" size="large">
  Click me
</Button>
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| variant | 'primary' \| 'secondary' | 'primary' | Button style variant |
| size | 'small' \| 'medium' \| 'large' | 'medium' | Button size |

<Canvas>
  <Story name="Primary" args={{ variant: 'primary', label: 'Primary Button' }} />
</Canvas>

<Controls of={Button} />
```

## 🧪 Testing with Storybook

### Test Coverage Requirements

**100% Test Coverage Required**: All Storybook stories and components must achieve 100% test coverage. This includes:

- **Story Coverage**: Every story must be tested
- **Component Coverage**: All component code paths must be tested
- **Interaction Coverage**: All user interactions must be tested
- **Accessibility Coverage**: All accessibility features must be tested

### Visual Testing

Use Storybook for visual regression testing:

```typescript
// Button.visual.test.ts
import { test, expect } from '@playwright/test';

test('Button visual regression', async ({ page }) => {
  await page.goto('/iframe.html?id=components-button--primary');
  await expect(page).toHaveScreenshot('button-primary.png');
});
```

### Interaction Testing

Test user interactions with 100% coverage:

```typescript
// Button.interaction.test.ts
import { expect, userEvent, within } from '@storybook/test';

export const ClickTest = {
  play: async ({ canvasElement }) => {
    const canvas = within(canvasElement);
    const button = canvas.getByRole('button');
    
    await userEvent.click(button);
    // Assert expected behavior
  },
};

// Ensure all interaction paths are tested
export const KeyboardTest = {
  play: async ({ canvasElement }) => {
    const canvas = within(canvasElement);
    const button = canvas.getByRole('button');
    
    await userEvent.keyboard('{Enter}');
    await userEvent.keyboard(' ');
    // Test all keyboard interactions
  },
};
```

### Accessibility Testing

Test accessibility with the a11y addon:

```typescript
// Button.stories.ts
export const AccessibilityTest: Story = {
  args: {
    label: 'Accessible Button',
  },
  parameters: {
    a11y: {
      config: {
        rules: [
          {
            id: 'color-contrast',
            enabled: true,
          },
        ],
      },
    },
  },
};
```

## 🎨 Theming and Styling

### Theme Switching

```typescript
// .storybook/preview.ts
export const parameters = {
  backgrounds: {
    default: 'light',
    values: [
      { name: 'light', value: '#ffffff' },
      { name: 'dark', value: '#333333' },
    ],
  },
};

// Theme decorator
const withTheme = (Story, context) => {
  const theme = context.globals.theme;
  return (
    <div data-theme={theme}>
      <Story />
    </div>
  );
};
```

### CSS-in-JS Support

```typescript
// With styled-components
import styled from 'styled-components';

const StyledButton = styled.button`
  background: ${props => props.primary ? 'blue' : 'gray'};
  color: white;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
`;
```

## 🔧 Advanced Configuration

### Custom Addons

```typescript
// .storybook/main.ts
export default {
  addons: [
    '@storybook/addon-essentials',
    '@storybook/addon-a11y',
    '@storybook/addon-docs',
    'storybook-addon-themes',
  ],
};
```

### Custom Parameters

```typescript
// Global parameters
export const parameters = {
  actions: { argTypesRegex: '^on[A-Z].*' },
  controls: {
    matchers: {
      color: /(background|color)$/i,
      date: /Date$/,
    },
  },
  docs: {
    toc: true,
  },
};
```

### Viewport Configuration

```typescript
// .storybook/preview.ts
export const parameters = {
  viewport: {
    viewports: {
      mobile: {
        name: 'Mobile',
        styles: {
          width: '375px',
          height: '667px',
        },
      },
      tablet: {
        name: 'Tablet',
        styles: {
          width: '768px',
          height: '1024px',
        },
      },
      desktop: {
        name: 'Desktop',
        styles: {
          width: '1024px',
          height: '768px',
        },
      },
    },
  },
};
```

## 🚀 Deployment

### Static Build

```bash
# Build static Storybook
npm run build-storybook

# Deploy to hosting service
npx storybook-to-ghpages
```

### Chromatic Integration

```bash
# Install Chromatic
npm install --save-dev chromatic

# Publish to Chromatic
npx chromatic --project-token=your-token
```

### Netlify Deployment

```yaml
# netlify.toml
[build]
  command = "npm run build-storybook"
  publish = "storybook-static"
```

## 📊 Analytics and Monitoring

### Usage Analytics

```typescript
// .storybook/preview.ts
import { addons } from '@storybook/manager-api';

addons.register('storybook/analytics', () => {
  // Track story views and interactions
});
```

### Performance Monitoring

```typescript
// Monitor component performance
export const PerformanceTest: Story = {
  parameters: {
    performance: {
      maxRenders: 100,
    },
  },
};
```

## 🎯 Best Practices

### Story Organization

1. **Group Related Stories**: Use consistent naming and grouping
2. **Show Edge Cases**: Include error states, empty states, and loading states
3. **Document Interactions**: Show how components respond to user actions
4. **Keep Stories Simple**: Each story should focus on one aspect

### Performance

1. **Lazy Load Heavy Components**: Use dynamic imports for large components
2. **Optimize Images**: Use appropriate image formats and sizes
3. **Minimize Bundle Size**: Only import what you need
4. **Use Memoization**: Prevent unnecessary re-renders

### Accessibility

1. **Test with Screen Readers**: Ensure components work with assistive technology
2. **Keyboard Navigation**: Test all interactive elements
3. **Color Contrast**: Verify sufficient contrast ratios
4. **Focus Management**: Ensure proper focus indicators

## 📚 Resources

- [Storybook Documentation](https://storybook.js.org/docs)
- [Storybook Best Practices](https://storybook.js.org/docs/best-practices)
- [Component Testing Guide](https://storybook.js.org/docs/writing-tests)
- [Accessibility Testing](https://storybook.js.org/docs/writing-tests/accessibility-testing)
- [Visual Testing](https://storybook.js.org/docs/writing-tests/visual-testing)
