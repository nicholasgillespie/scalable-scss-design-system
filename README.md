# Scalable SCSS Design System

Welcome to the **Scalable SCSS Design System**. This repository offers a modular and scalable design system built with [SCSS](https://sass-lang.com/), designed for easy integration into any project.

Inspired by [Andy Bell's](https://set.studio/) [CUBE CSS Boilerplate](https://github.com/Set-Creative-Studio/cube-boilerplate/blob/main/README.md) and incorporating the [CUBE CSS methodology](https://cube.fyi/), this system provides consistent design application and maintainability. It integrates the file architecture and class naming conventions from the in-development [W3C design system](https://design-system.w3.org/), providing an organized and efficient structure.

This system uses layout classes from [Every Layout](https://every-layout.dev/), simplifying layout with native CSS algorithms.

### Key Features:

- **Design Tokens**: Centralized theme configuration for streamlined management of design tokens.
- **Theme Application**: Generates CSS variables from design tokens for consistent theming.
- **Theme Access**: Provides a function for retrieving CSS variables corresponding to design tokens based on specified properties and values.
- **Theme Utilities**: Includes utility classes derived from the theme configuration for efficient styling.
- **Layout Classes**: Versatile, composable classes for responsive designs from [Every Layout](https://every-layout.dev/).

## Overview

The **Scalable SCSS Design System** is designed with flexibility and scalability in mind. It centralizes design tokens (such as colors, spacing, and typography) into a theme configuration, ensuring consistent application across your project.

## Table of Contents

- [Folder Structure](#folder-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Customization](#customization)

## Folder Structure

The project is structured as follows:

```
styles
├─ 00-settings
│  ├─ _theme-config.scss        # Centralizes design tokens and configuration.
│  └─ ...                       # Token files (e.g., colors, spacing, font-size)
├─ 10-functions
│  ├─ _theme-accessor.scss      # Function for retrieving token values.
│  └─ ...                       # Other utility functions for formatting, clamping, etc.
├─ 20-mixins
│  ├─ _theme-applier.scss       # Mixins for generating CSS variables and utility classes.
│  └─ media-query.scss          # Mixin for theme-based media queries.
├─ 30-base                      # Base styles (e.g., reset, root, global styles).
├─ 40-layouts                   # Layout-related styles.
├─ 50-core-components           # Core UI components.
├─ 60-advanced-components       # More complex UI components.
├─ 70-third-party-plugins       # Styles for third-party plugins.
├─ 80-templates                 # Templates for specific pages or sections.
├─ 90-utilities                 # Utility classes generated from design tokens.
├─ advanced.scss                # SCSS entry point for advanced features.
├─ core.scss                    # SCSS entry point for core styles.
└─ print.scss                   # Print-specific styles.
```

### Detailed Breakdown:

- **[00-settings](./styles/00-settings)**: Contains [`_theme-config.scss`](./styles/00-settings/_theme-config.scss) for centralized theme tokens and configuration.
- **[10-functions](./styles/10-functions)**: Includes [`_theme-accessor.scss`](./styles/10-functions/_theme-accessor.scss) for accessing token values and utility functions.
- **[20-mixins](./styles/20-mixins)**: Features [`_theme-applier.scss`](./styles/20-mixins/_theme-applier.scss) for generating CSS variables and [`media-query.scss`](./styles/20-mixins/media-query.scss) for responsive design.
- **[30-base](./styles/30-base)**: For global styles including resets, typography, and root styles.
- **[40-layouts](./styles/40-layouts)**: Includes layout styles like grids and spacing utilities.
- **[50-core-components](./styles/50-core-components)**: Core UI components such as buttons and forms.
- **[60-advanced-components](./styles/60-advanced-components)**: Advanced components building on core styles.
- **[70-third-party-plugins](./styles/70-third-party-plugins)**: Styles for third-party plugins and libraries.
- **[80-templates](./styles/80-templates)**: Styles for page and section templates.
- **[90-utilities](./styles/90-utilities)**: Auto-generated utility classes from design tokens.
- **[advanced.scss](./styles/advanced.scss)**: Main entry point for advanced features.
- **[core.scss](./styles/core.scss)**: Main entry point for core styles.
- **[print.scss](./styles/print.scss)**: Styles for print media.

## Installation

To integrate this design system into your project:

1. **Clone the Repository**:

   Clone the repository into your desired project location (e.g., `src` folder):

   ```bash
   git clone https://github.com/your-username/scalable-scss-design-system.git
   ```

2. **Install Dependencies**:

   Install Sass as a development dependency:

   ```bash
   npm install --save-dev sass
   ```

3. **Include in SCSS Build**:

   Ensure your build process includes the design system’s SCSS files. This is typically handled automatically by modern build tools like [Vite](https://vitejs.dev/) or [Astro](https://astro.build/).

## Usage

After adding the design system to your project, you can start using the design tokens, mixins, and utility classes provided.

### Importing the Styles

To ensure compatibility and progressive enhancement, it's recommended to consider the [CSS Only Mustard Cut](https://github.com/Fall-Back/CSS-Mustard-Cut?tab=readme-ov-file#css-only-mustard-cut). This method conditionally serves advanced styles based on feature support while providing a basic, functional experience across all browsers. However, you are free to choose the setup that best fits your choice.

Include the styles in your HTML as follows:

```html
<!-- Core Stylesheet -->
<link rel="stylesheet" href="path/to/styles/core.scss" />

<!-- Advanced Stylesheet (conditionally served) -->
<link
  rel="stylesheet"
  id="advanced-stylesheet"
  href="path/to/styles/advanced.scss"
  media="
    only print,
    only all and (pointer: fine), only all and (pointer: coarse), only all and (pointer: none),
    only all and (min--moz-device-pixel-ratio:0) and (display-mode:browser), (min--moz-device-pixel-ratio:0) and (display-mode:fullscreen)
"
/>

<!-- Print Stylesheet -->
<link rel="stylesheet" href="path/to/styles/print.scss" />
```

### Applying the Theme

To apply the theme to your project, generate CSS custom properties as follows:

1. **Generate Theme Variables:**

   To apply the full theme, include the `generateThemeVariables` mixin in your root element. This generates global CSS custom properties for all design tokens defined in `_theme-config.scss`. Typically, this is added to the `:root` selector in your main SCSS file:

   ```scss
   :root {
     @include generateThemeVariables();
   }
   ```

   Alternatively, generate CSS custom properties for specific token types such as "global" or "contextual-generic" tokens. Token types are defined in the `_theme-applier.scss` file.

   ```scss
   :root {
     @include generateThemeVariables("contextual-generic");
   }
   ```

2. **Generate Specific Token Variables with Optional Transformation:**

   To generate variables for a specific token, use the `generateTokenVariables` mixin. For example, to generate variables for the "colors" token group and apply the `transformColorP3` transformation function:

   ```scss
   :root {
     @include generateTokenVariables("colors", "transformColorP3");
   }
   ```

### Accessing Theme Values with the `get` Function

The design system includes the `get` function in `_theme-accessor.scss`, allowing dynamic application of theme values:

- **Retrieve CSS Variables**: Use the `get` function to fetch the CSS variable associated with a design token:

  ```scss
  body {
    color: get("color", "global");
    background-color: get("background", "global");
  }
  ```

- **Dynamic Property Application**: The `get` function supports various properties and values, ensuring alignment with the defined theme.

- **Error Handling**: Includes built-in error handling to maintain design integrity and aid debugging.

### Generating Utility Classes

To generate utility classes, add the necessary mixins to the [`90-utilities/_index.scss`](./90-utilities/_index.scss) file:

```scss
@use "../20-mixins/theme-applier" as *;

// Import specific utility classes (e.g., visually-hidden)
@use "./visually-hidden";

// Generate utility classes from theme and custom utilities
@include generateThemeUtilities();
@include generateThemeSpacingUtilities();
```

**Example Usage**

After generating the utility classes, apply them directly in your HTML. For instance, if your design tokens include a "primary" color:

```scss
.u-color-primary {
  color: var(--color-primary);
}
```

```html
<p class="u-color-primary">This text is styled with the primary color.</p>
```

**Considerations**

While utility-first frameworks like [Tailwind](https://tailwindcss.com/) offer rapid styling options, a semantic approach often results in cleaner, more maintainable code. Utilities can be efficient for quick development but semantic CSS promotes a deeper understanding and better long-term scalability.

## Customization

The design system is highly customizable. Modify the design tokens in `_theme-config.scss`to match your project’s branding and design requirements. Update the values in the theme map and recompile your styles as needed.
