# Storybook-Specific Cursor Rules

This file contains Storybook-specific rules and guidelines for the Aqqo Design System project.

## 📚 Storybook Development Rules

### Story File Requirements
- Every component MUST have a corresponding `.stories.tsx` file
- Stories must be placed in the same directory as the component
- Use the naming convention: `ComponentName.stories.tsx`
- Include comprehensive story coverage for all component states

### Story Structure Requirements
```typescript
// Required story structure
import type { Meta, StoryObj } from '@storybook/nextjs-vite';
import { fn } from 'storybook/test';
import { Component } from './Component';

const meta = {
  title: 'Components/ComponentName', // Follow this hierarchy
  component: Component,
  tags: ['autodocs'], // Always include for documentation
  parameters: {
    docs: {
      description: {
        component: 'Component description and usage guidelines',
      },
    },
  },
  argTypes: {
    // Define controls for all props
    variant: {
      control: { type: 'select' },
      options: ['primary', 'secondary'],
      description: 'Visual style variant',
    },
  },
  args: {
    // Default args
  },
} satisfies Meta<typeof Component>;

export default meta;
type Story = StoryObj<typeof meta>;
```

### Required Story Variations
Every component must include these story variations:

```typescript
// 1. Default story
export const Default: Story = {};

// 2. Variant stories
export const Primary: Story = { args: { variant: 'primary' } };
export const Secondary: Story = { args: { variant: 'secondary' } };

// 3. Size stories
export const Small: Story = { args: { size: 'small' } };
export const Large: Story = { args: { size: 'large' } };

// 4. State stories
export const Disabled: Story = { args: { disabled: true } };
export const Loading: Story = { args: { loading: true } };

// 5. Interactive stories
export const Interactive: Story = {
  play: async ({ canvasElement }) => {
    const canvas = within(canvasElement);
    const button = canvas.getByRole('button');
    await userEvent.click(button);
  },
};
```

### Story Organization Rules
- Use clear, descriptive story names
- Group related stories together
- Include edge cases and error states
- Add stories for different screen sizes
- Include accessibility-focused stories

### Story Documentation Requirements
- Include component descriptions in story parameters
- Add usage examples in story descriptions
- Document prop combinations and use cases
- Include accessibility notes
- Add design guidelines and best practices

### Interaction Testing Rules
- Use `play` functions for interaction testing
- Test all user interactions (click, keyboard, form)
- Include accessibility interaction tests
- Test error states and edge cases
- Verify proper event handling

### Storybook Configuration Rules
- Use proper addon configuration
- Include accessibility addon for a11y testing
- Configure proper viewport settings
- Set up proper theming and styling
- Include proper decorators for context

### Performance Rules
- Use dynamic imports for large components
- Implement proper story organization
- Optimize story loading and rendering
- Use proper asset optimization
- Implement proper caching strategies

### Documentation Rules
- Use `tags: ['autodocs']` for automatic documentation
- Include comprehensive prop documentation
- Add usage examples and guidelines
- Document design decisions and rationale
- Include accessibility information

### Testing Rules
- Include interaction tests in stories
- Test all component states and variations
- Include accessibility testing
- Test responsive behavior
- Include error state testing

### Code Quality Rules
- Follow TypeScript best practices
- Use proper imports and exports
- Include proper error handling
- Use meaningful variable names
- Follow established patterns

### Accessibility Rules
- Include accessibility testing in stories
- Test keyboard navigation
- Test screen reader compatibility
- Test color contrast and visual accessibility
- Include ARIA attribute testing

### Design System Rules
- Use design tokens consistently
- Follow established design patterns
- Include theming and customization options
- Test different themes and variants
- Include responsive design testing

### Component Integration Rules
- Test component integration with other components
- Include composition examples
- Test different prop combinations
- Include real-world usage examples
- Test component lifecycle and state management

### Storybook Addon Rules
- Use appropriate addons for testing
- Configure addons properly
- Include accessibility addon
- Use controls addon effectively
- Include actions addon for event testing

### Deployment Rules
- Ensure stories work in production build
- Test static storybook build
- Include proper asset optimization
- Test different deployment scenarios
- Include proper error handling

### Maintenance Rules
- Keep stories up to date with component changes
- Update documentation when components change
- Test stories after component updates
- Include proper versioning for stories
- Maintain story consistency across components

### Collaboration Rules
- Use clear story naming conventions
- Include proper documentation for other developers
- Test stories in different environments
- Include proper error handling and edge cases
- Maintain consistent story structure

### Quality Assurance Rules
- Review all stories before merging
- Test stories in different browsers
- Include proper error handling
- Test accessibility compliance
- Verify proper documentation

### Best Practices
- Use meaningful story names
- Include comprehensive test coverage
- Document all story variations
- Include real-world usage examples
- Test edge cases and error states
- Maintain consistent story structure
- Include proper accessibility testing
- Use proper TypeScript typing
- Follow established patterns and conventions
- Include proper documentation and examples
