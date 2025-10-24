# Aqqo Design System

A modern design system built with Next.js and Storybook, providing a comprehensive collection of reusable UI components for consistent and scalable web applications.

## 🚀 Features

- **Modern Tech Stack**: Built with Next.js 16, React 19, and TypeScript
- **Component Documentation**: Interactive component library powered by Storybook
- **Design System Ready**: Structured for scalable component development
- **Accessibility First**: Built-in accessibility testing with Storybook addons
- **Testing Integration**: Vitest and Playwright for comprehensive testing
- **Styling**: Tailwind CSS for utility-first styling
- **Type Safety**: Full TypeScript support for better development experience

## 📦 Tech Stack

- **Framework**: Next.js 16 with App Router
- **UI Library**: React 19
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS 4
- **Documentation**: Storybook 9
- **Testing**: Vitest + Playwright
- **Linting**: ESLint with Storybook plugin

## 🛠️ Getting Started

### Prerequisites

- Node.js 18+ 
- npm, yarn, pnpm, or bun

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd aqqo-design-storybook
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   # or
   pnpm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000) to view the Next.js application.

4. **Start Storybook**
   ```bash
   npm run storybook
   ```
   Open [http://localhost:6006](http://localhost:6006) to view the component library.

## 📁 Project Structure

```
aqqo-design-storybook/
├── app/                    # Next.js app directory
│   ├── globals.css        # Global styles
│   ├── layout.tsx         # Root layout
│   └── page.tsx           # Home page
├── stories/               # Storybook stories and components
│   ├── assets/           # Images and icons
│   ├── Button.tsx        # Button component
│   ├── Button.stories.ts # Button stories
│   ├── Header.tsx        # Header component
│   ├── Header.stories.ts # Header stories
│   └── Configure.mdx     # Storybook configuration guide
├── public/               # Static assets
└── package.json          # Dependencies and scripts
```

## 🎨 Component Development

### Creating New Components

1. **Create the component file** in the `stories/` directory:
   ```typescript
   // stories/MyComponent.tsx
   export interface MyComponentProps {
     title: string;
     variant?: 'primary' | 'secondary';
   }
   
   export const MyComponent = ({ title, variant = 'primary' }: MyComponentProps) => {
     return (
       <div className={`my-component my-component--${variant}`}>
         {title}
       </div>
     );
   };
   ```

2. **Create the story file**:
   ```typescript
   // stories/MyComponent.stories.ts
   import type { Meta, StoryObj } from '@storybook/nextjs-vite';
   import { MyComponent } from './MyComponent';
   
   const meta = {
     title: 'Components/MyComponent',
     component: MyComponent,
     tags: ['autodocs'],
     argTypes: {
       variant: {
         control: { type: 'select' },
         options: ['primary', 'secondary'],
       },
     },
   } satisfies Meta<typeof MyComponent>;
   
   export default meta;
   type Story = StoryObj<typeof meta>;
   
   export const Primary: Story = {
     args: {
       title: 'Primary Component',
       variant: 'primary',
     },
   };
   ```

### Component Guidelines

- **TypeScript**: All components must be fully typed
- **Props Interface**: Define clear prop interfaces with JSDoc comments
- **Accessibility**: Follow WCAG guidelines and use semantic HTML
- **Responsive**: Design for mobile-first, then enhance for larger screens
- **Consistent Naming**: Use kebab-case for CSS classes, PascalCase for components

## 📚 Storybook Usage

### Available Scripts

- `npm run storybook` - Start Storybook development server
- `npm run build-storybook` - Build static Storybook for deployment

### Story Organization

Stories are organized by category:
- **Example**: Demo components and patterns
- **Components**: Core UI components
- **Layout**: Layout and structural components
- **Forms**: Form-related components

### Writing Stories

Each component should have multiple stories showcasing different states:
- **Default**: Basic usage
- **Variants**: Different visual styles
- **States**: Hover, focus, disabled, etc.
- **Sizes**: Different size options
- **Edge Cases**: Empty states, error states, etc.

## 🧪 Testing

### Running Tests

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run tests with coverage (100% required)
npm run test:coverage
```

### Test Coverage Requirements

**100% Test Coverage Required**: All components must achieve 100% test coverage. This is enforced through:

- **Coverage Thresholds**: Configured in `vitest.config.ts` to require 100% coverage
- **CI/CD Integration**: Coverage checks in continuous integration
- **Pre-commit Hooks**: Coverage validation before code commits
- **Coverage Reports**: Detailed coverage reports for all components

### Testing Strategy

- **100% Test Coverage**: All components must achieve 100% test coverage
- **Unit Tests**: Component logic and utilities
- **Integration Tests**: Component interactions
- **Visual Regression**: Storybook visual testing
- **Accessibility Tests**: Automated a11y testing
- **Coverage Monitoring**: Automated coverage reporting in CI/CD

## 🎨 Styling

### Tailwind CSS

This project uses Tailwind CSS 4 for styling. Key features:
- Utility-first CSS framework
- Responsive design utilities
- Dark mode support
- Custom design tokens

### CSS Architecture

- **Global Styles**: `app/globals.css`
- **Component Styles**: Co-located with components
- **Design Tokens**: CSS custom properties for consistency

## 🚀 Deployment

### Building for Production

```bash
# Build Next.js application
npm run build

# Build Storybook
npm run build-storybook
```

### Deployment Options

- **Vercel**: Recommended for Next.js applications
- **Netlify**: Alternative deployment platform
- **Static Hosting**: Deploy Storybook as static site

## 🤝 Contributing

### Development Workflow

1. Create a feature branch
2. Develop your component with stories
3. Write tests for your component
4. Update documentation
5. Submit a pull request

### Code Standards

- Follow TypeScript best practices
- Use ESLint and Prettier for code formatting
- Write meaningful commit messages
- Include tests for new features

## 📖 Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Storybook Documentation](https://storybook.js.org/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [React Documentation](https://react.dev)

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
