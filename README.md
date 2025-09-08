# tailwind

# Tailwind CSS

A utility-first CSS framework for rapidly building custom user interfaces.

## Table of Contents

- [About](#about)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Usage Examples](#usage-examples)
- [Best Practices](#best-practices)
- [Customization](#customization)
- [Production Build](#production-build)
- [Browser Support](#browser-support)
- [Resources](#resources)
- [Contributing](#contributing)

## About

Tailwind CSS is a utility-first CSS framework packed with classes like `flex`, `pt-4`, `text-center` and `rotate-90` that can be composed to build any design, directly in your markup.

### Key Features

- **Utility-First**: Build complex components from a constrained set of primitive utilities
- **Responsive Design**: Every utility class can be applied conditionally at different breakpoints
- **Component-Friendly**: Easily extract components with utilities using your favorite tools
- **Customizable**: Customize your design system and extend Tailwind to fit your brand
- **Modern**: Built for modern development workflows with features like JIT compilation

## Installation

### Using npm

```bash
npm install -D tailwindcss
npx tailwindcss init
```

### Using Yarn

```bash
yarn add -D tailwindcss
npx tailwindcss init
```

### Using pnpm

```bash
pnpm install -D tailwindcss
npx tailwindcss init
```

### CDN (Not recommended for production)

```html
<script src="https://cdn.tailwindcss.com"></script>
```

## Quick Start

1. **Install Tailwind CSS** (see installation above)

2. **Configure your template paths** in `tailwind.config.js`:

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,js}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

3. **Add Tailwind directives** to your CSS file:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

4. **Start the build process**:

```bash
npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch
```

5. **Start using Tailwind** in your HTML:

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="./dist/output.css" rel="stylesheet">
</head>
<body>
  <h1 class="text-3xl font-bold underline text-blue-600">
    Hello world!
  </h1>
</body>
</html>
```

## Configuration

### Basic Configuration

The `tailwind.config.js` file allows you to customize your Tailwind installation:

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{html,js,ts,jsx,tsx}",
    "./components/**/*.{html,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        'brand-blue': '#1fb6ff',
        'brand-purple': '#7e5bef',
        'brand-pink': '#ff49db',
      },
      fontFamily: {
        'sans': ['Inter', 'sans-serif'],
      },
      spacing: {
        '128': '32rem',
        '144': '36rem',
      },
    },
  },
  plugins: [
    require('@tailwindcss/forms'),
    require('@tailwindcss/typography'),
    require('@tailwindcss/aspect-ratio'),
  ],
  darkMode: 'class', // or 'media'
}
```

### Framework Integration

#### React/Next.js

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

#### Vue/Nuxt.js

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

## Usage Examples

### Layout

```html
<!-- Flexbox Layout -->
<div class="flex items-center justify-between p-4">
  <h1 class="text-xl font-semibold">Header</h1>
  <button class="bg-blue-500 text-white px-4 py-2 rounded">Button</button>
</div>

<!-- Grid Layout -->
<div class="grid grid-cols-1 md:grid-cols-3 gap-4">
  <div class="bg-white p-6 rounded-lg shadow">Card 1</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 2</div>
  <div class="bg-white p-6 rounded-lg shadow">Card 3</div>
</div>
```

### Components

```html
<!-- Button Component -->
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline transition duration-200">
  Click me
</button>

<!-- Card Component -->
<div class="max-w-sm rounded overflow-hidden shadow-lg bg-white">
  <img class="w-full h-48 object-cover" src="image.jpg" alt="Card image">
  <div class="px-6 py-4">
    <h2 class="font-bold text-xl mb-2 text-gray-900">Card Title</h2>
    <p class="text-gray-700 text-base">
      Card description goes here...
    </p>
  </div>
</div>
```

### Responsive Design

```html
<!-- Responsive Text -->
<h1 class="text-lg md:text-2xl lg:text-4xl font-bold">
  Responsive Heading
</h1>

<!-- Responsive Grid -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
  <!-- Grid items -->
</div>

<!-- Responsive Utilities -->
<div class="block md:hidden">Only visible on mobile</div>
<div class="hidden md:block">Hidden on mobile</div>
```

### Dark Mode

```html
<!-- Dark mode classes -->
<div class="bg-white dark:bg-gray-800 text-gray-900 dark:text-gray-100">
  <h1 class="text-2xl font-bold">Dark mode support</h1>
  <p class="text-gray-600 dark:text-gray-400">
    This text adapts to dark mode
  </p>
</div>
```

## Best Practices

### 1. Use Semantic Class Names for Components

```html
<!-- Instead of repeating utilities -->
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  Button 1
</button>
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  Button 2
</button>

<!-- Create a component class -->
<style>
.btn-primary {
  @apply bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded;
}
</style>

<button class="btn-primary">Button 1</button>
<button class="btn-primary">Button 2</button>
```

### 2. Use the @layer Directive

```css
@layer components {
  .btn-primary {
    @apply py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75;
  }
}
```

### 3. Organize Your Utilities

```html
<!-- Group related utilities together -->
<div class="
  flex items-center justify-between
  w-full max-w-md mx-auto
  p-6 bg-white rounded-lg shadow-md
  hover:shadow-lg transition-shadow duration-200
">
  Content here
</div>
```

## Customization

### Custom Colors

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          100: '#dbeafe',
          500: '#3b82f6',
          900: '#1e3a8a',
        }
      }
    }
  }
}
```

### Custom Spacing

```javascript
module.exports = {
  theme: {
    extend: {
      spacing: {
        '72': '18rem',
        '84': '21rem',
        '96': '24rem',
      }
    }
  }
}
```

### Custom Fonts

```javascript
module.exports = {
  theme: {
    extend: {
      fontFamily: {
        'heading': ['Montserrat', 'sans-serif'],
        'body': ['Open Sans', 'sans-serif'],
      }
    }
  }
}
```

## Production Build

### Purging Unused CSS

Tailwind automatically removes unused styles in production:

```javascript
module.exports = {
  content: [
    "./src/**/*.{html,js,ts,jsx,tsx}",
  ],
  // ... rest of config
}
```

### Build Command

```bash
npx tailwindcss -i ./src/input.css -o ./dist/output.css --minify
```

### File Size Optimization

- Use PurgeCSS (built-in)
- Enable minification in production
- Use tree-shaking with bundlers

## Browser Support

Tailwind CSS supports all modern browsers:

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

For older browser support, consider using:
- Autoprefixer for vendor prefixes
- PostCSS plugins for additional compatibility

## Resources

### Official Links

- [Documentation](https://tailwindcss.com/docs)
- [Playground](https://play.tailwindcss.com)
- [GitHub Repository](https://github.com/tailwindlabs/tailwindcss)

### Tools & Extensions

- [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) - VS Code extension
- [Headless UI](https://headlessui.dev) - Unstyled, accessible UI components
- [Heroicons](https://heroicons.com) - SVG icons by Tailwind team
- [Tailwind UI](https://tailwindui.com) - Premium component library

### Community

- [Discord](https://discord.gg/tailwindcss)
- [Twitter](https://twitter.com/tailwindcss)
- [YouTube](https://www.youtube.com/tailwindlabs)

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup

```bash
git clone https://github.com/tailwindlabs/tailwindcss.git
cd tailwindcss
npm install
npm run build
npm test
```

## License

Tailwind CSS is licensed under the [MIT License](LICENSE).

---

**Happy styling with Tailwind CSS! 🎨**
