# Scalable SCSS Design System

Welcome to the **Scalable SCSS Design System**! This repository provides a modular and scalable design system built with [**SCSS**](https://sass-lang.com/), designed for easy integration into any project.

### Key Features:

- **Design Tokens**: Centralized theme configuration for easy management of design tokens.
- **Token Application**: Generation of CSS custom properties from design tokens.
- **Dynamic Token Access**: Function for retrieving the CSS variable corresponding to a design token based on the specified property and value.
- **Custom Utilities**: Custom utility classes derived from design tokens.
- **Modular Structure**: Organized SCSS files for easy maintenance and scalability.

## Overview

The Scalable SCSS Design System is built with flexibility and scalability in mind. It centralizes your design tokens (such as colors, spacing, typography) into a theme configuration, which is applied consistently across your project.

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
│  ├─ _theme-accessor.scss      # Provides function to access and retrieve token values.
│  └─ ...                       # Other functions for formatting, clamping, etc.
├─ 20-mixins
│  └─ _theme-applier.scss       # Mixins to generate CSS variables and utility classes.
│  └─ media-query.scss          # Mixin for theme-based media queries
├─ 30-base                      # Base styles (e.g., reset, root, global styles).
├─ 40-layouts                   # Layout-related styles.
├─ 50-core-components           # Core UI components.
├─ 60-advanced-components       # More complex UI components.
├─ 70-third-party-plugins       # Styles for third-party plugins.
├─ 80-templates                 # Templates for specific pages or sections.
├─ 90-utilities                 # Utility classes generated from design tokens.
├─ advanced.scss                # Main SCSS entry point for advanced features.
├─ core.scss                    # Main SCSS entry point for core styles.
└─ print.scss                   # Print-specific styles.
```

### Detailed Breakdown:

- **[00-settings](./styles/00-settings)**: Houses [`_theme-config.scss`](./styles/00-settings/_theme-config.scss) for centralized theme configuration and design tokens, with modular files for each token type.
- **[10-functions](./styles/10-functions)**: Features [`_theme-accessor.scss`](./styles/10-functions/_theme-accessor.scss) for retrieving design token values, plus utility functions and helpers for various operations.
- **[20-mixins](./styles/20-mixins)**: Includes [`_theme-applier.scss`](./styles/20-mixins/_theme-applier.scss) for generating global CSS custom properties and utility classes, and [`media-query.scss`](./styles/20-mixins/media-query.scss) for responsive design using theme-defined breakpoints.
- **[30-base](./styles/30-base)**: Intended for global styles like resets, root styles, global typography, and default element styles.
- **[40-layouts](./styles/40-layouts)**: For layout-related styles, such as grid systems, spacing utilities, and layout-specific classes.
- **[50-core-components](./styles/50-core-components)**: Core UI components like buttons, forms, and basic navigation.
- **[60-advanced-components](./styles/60-advanced-components)**: More complex components that build on the core components.
- **[70-third-party-plugins](./styles/70-third-party-plugins)**: Styles specifically for third-party plugins or libraries.
- **[80-templates](./styles/80-templates)**: Contains template-specific styles for pages or sections.
- **[90-utilities](./styles/90-utilities)**: Auto-generated utility classes that can be used to quickly apply design token values.
- **[advanced.scss](./styles/advanced.scss)**: The main SCSS file that imports advanced features, such as complex components or layouts.
- **[core.scss](./styles/core.scss)**: The main SCSS file that imports core styles for basic setup.
- **[print.scss](./styles/print.scss)**: Handles styles for print-specific media.

## Installation

To use this design system in your project:

1. **Clone the Repository**:

   Clone the repository into the desired location within your project (e.g., `src` folder):

   ```bash
   git clone https://github.com/your-username/scalable-scss-design-system.git
   ```

2. **Install Dependencies**:

   Install Sass as a development dependency in your project:

   ```bash
   npm install --save-dev sass
   ```

3. **Include in SCSS Build**:

   Ensure that your build process includes the design system's SCSS files. This is generally handled automatically if you are using modern build tools like Vite or Astro.

## Usage

Once you have added the design system to your project, you can start using the design tokens, mixins, and utility classes provided.

### Importing the Styles

To include the styles in your HTML, use the following links:

```html
<!-- Core Stylesheet -->
<link rel="stylesheet" href="path/to/styles/core.css" />

<!-- Advanced Stylesheet (conditionally served) -->
<link
  rel="stylesheet"
  id="advanced-stylesheet"
  href="path/to/styles/advanced.css"
  media="
    only print,
    only all and (pointer: fine), only all and (pointer: coarse), only all and (pointer: none),
    only all and (min--moz-device-pixel-ratio:0) and (display-mode:browser), (min--moz-device-pixel-ratio:0) and (display-mode:fullscreen)
"
/>

<!-- Print Stylesheet -->
<link rel="stylesheet" href="path/to/styles/print.css" />
```

### Applying the Theme

To apply the theme to your project, you can generate CSS custom properties in one of two ways:

1. **Generate All Theme Variables:**

   To apply the full theme, include the `generateThemeVariables` mixin in your root element. This will generate global CSS custom properties for all design tokens defined in `_theme-config.scss`. Typically, this is added to the `:root` selector in your main SCSS file:

   ```scss
   :root {
     @include generateThemeVariables();
   }
   ```

2. **Generate Specific Token Variables with Optional Transformation:**

   If you need to generate CSS custom properties for specific token groups, you can use the `generateTokenVariables` mixin. This method allows you to focus on particular tokens and apply an optional transformation function. For example, to generate variables for the "colors" token group and apply the `toP3` transformation function:

   ```scss
   :root {
     @include generateTokenVariables("colors", "transformColorP3");
   }
   ```

### Applying Theme Values with the `get` Function

The Scalable SCSS Design System provides a `get` function within the `_theme-accessor.scss` file, enabling the dynamic application of theme values based on design tokens. This function allows you to consistently apply CSS variables across your styles with ease:

- **Retrieve CSS Variables**: The `get` function allows you to retrieve a CSS variable corresponding to a design token. For example, to apply the "primary" color token, use the following code:

  ```scss
  body {
    color: get("color", "primary");
  }
  ```

  This will fetch the CSS variable associated with the "primary" color, ensuring consistency and adherence to the theme throughout your project.

- **Dynamic Property Application**: The `get` function is versatile, supporting various properties and values. This flexibility ensures that your styles remain in alignment with the design tokens defined in the theme, regardless of the property being styled.

- **Error Handling**: To maintain design integrity, the get function includes built-in error handling. If an invalid property or value is specified, the function will issue a warning, aiding in debugging and ensuring that your styles remain consistent with the intended design system.

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

**Example: Using Generated Utility Classes**

After generating the utility classes, you can apply them directly in your HTML files. For instance, if your design tokens include a "primary" color, the generated utility class might look like this:

```scss
.u-color-primary {
  color: var(--color-primary);
}
```

You can then apply this class in your HTML:

```html
<p class="u-color-primary">This text is styled with the primary color.</p>
```

**Considerations**

Utility-first frameworks like Tailwind speed up styling, but a semantic approach often yields cleaner, more maintainable code. While utilities can be efficient, especially for less experienced developers or rapid development, semantic CSS fosters a deeper understanding and better long-term scalability.

## Customization

The design system is highly customizable. You can modify the design tokens in `_theme-config.scss` to match your project's branding and design requirements. Simply update the values in the theme map and recompile your styles.

<!-- ## Contributing

Contributions are welcome! If you'd like to contribute to this project, please fork the repository, create a new branch, and submit a pull request. -->

<!-- ## License
This project is licensed under the MIT License. See the LICENSE file for details. -->
