# CSS Generation from Brand Guide

This reference explains how to translate a `brand-guide.json` into CSS custom properties and apply them consistently in frontend code.

## Step 1: Generate the Root Variables

Every frontend output starts with a `:root` block containing ALL brand tokens as CSS custom properties. This is non-negotiable — it ensures every value is centralized and traceable.

### Color Variables

```css
:root {
  /* Primary */
  --color-primary: [colors.primary.base];
  --color-primary-light: [colors.primary.light];
  --color-primary-dark: [colors.primary.dark];
  --color-primary-contrast: [colors.primary.contrast];

  /* Secondary */
  --color-secondary: [colors.secondary.base];
  --color-secondary-light: [colors.secondary.light];
  --color-secondary-dark: [colors.secondary.dark];
  --color-secondary-contrast: [colors.secondary.contrast];

  /* Accent (if defined) */
  --color-accent: [colors.accent.base];

  /* Neutral scale */
  --color-neutral-50: [colors.neutral.50];
  --color-neutral-100: [colors.neutral.100];
  /* ... full scale through 950 ... */

  /* Semantic */
  --color-success: [colors.semantic.success];
  --color-warning: [colors.semantic.warning];
  --color-error: [colors.semantic.error];
  --color-info: [colors.semantic.info];

  /* Backgrounds */
  --bg-primary: [colors.background.primary];
  --bg-secondary: [colors.background.secondary];
  --bg-tertiary: [colors.background.tertiary];

  /* Text */
  --text-primary: [colors.text.primary];
  --text-secondary: [colors.text.secondary];
  --text-tertiary: [colors.text.tertiary];
  --text-inverse: [colors.text.inverse];

  /* Borders */
  --border-default: [colors.border.default];
  --border-strong: [colors.border.strong];
  --border-subtle: [colors.border.subtle];
}
```

### Typography Variables

```css
:root {
  /* Font families */
  --font-heading: '[typography.headingFont]', [fallback-stack];
  --font-body: '[typography.bodyFont]', [fallback-stack];
  --font-mono: '[typography.monoFont]', monospace;

  /* Type scale */
  --text-xs: [typography.scale.xs];
  --text-sm: [typography.scale.sm];
  --text-base: [typography.scale.base];
  --text-lg: [typography.scale.lg];
  --text-xl: [typography.scale.xl];
  --text-2xl: [typography.scale.2xl];
  --text-3xl: [typography.scale.3xl];
  --text-4xl: [typography.scale.4xl];
  --text-5xl: [typography.scale.5xl];

  /* Line heights */
  --leading-tight: [typography.lineHeights.tight];
  --leading-normal: [typography.lineHeights.normal];
  --leading-relaxed: [typography.lineHeights.relaxed];

  /* Font weights */
  --font-regular: [typography.weights.regular];
  --font-medium: [typography.weights.medium];
  --font-semibold: [typography.weights.semibold];
  --font-bold: [typography.weights.bold];
}
```

### Spacing Variables

```css
:root {
  --space-0: 0;
  --space-px: 1px;
  --space-0-5: [spacing.scale[0.5]];
  --space-1: [spacing.scale[1]];
  --space-2: [spacing.scale[2]];
  --space-3: [spacing.scale[3]];
  --space-4: [spacing.scale[4]];
  --space-5: [spacing.scale[5]];
  --space-6: [spacing.scale[6]];
  --space-8: [spacing.scale[8]];
  --space-10: [spacing.scale[10]];
  --space-12: [spacing.scale[12]];
  --space-16: [spacing.scale[16]];
  --space-20: [spacing.scale[20]];
  --space-24: [spacing.scale[24]];

  /* Layout */
  --container-max: [spacing.containerMax];
  --content-max: [spacing.contentMax];
}
```

### Shape Variables

```css
:root {
  /* Border radius */
  --radius-none: 0;
  --radius-sm: [borders.radius.sm];
  --radius-md: [borders.radius.md];
  --radius-lg: [borders.radius.lg];
  --radius-xl: [borders.radius.xl];
  --radius-full: 9999px;

  /* Shadows */
  --shadow-sm: [borders.shadows.sm];
  --shadow-md: [borders.shadows.md];
  --shadow-lg: [borders.shadows.lg];
  --shadow-xl: [borders.shadows.xl];
  --shadow-inner: [borders.shadows.inner];
  --shadow-none: none;

  /* Border */
  --border-width: [borders.width];
}
```

### Motion Variables

```css
:root {
  --duration-fast: [motion.durations.fast];
  --duration-normal: [motion.durations.normal];
  --duration-slow: [motion.durations.slow];

  --ease-default: [motion.easings.default];
  --ease-enter: [motion.easings.enter];
  --ease-exit: [motion.easings.exit];
}

@media (prefers-reduced-motion: reduce) {
  :root {
    --duration-fast: 0ms;
    --duration-normal: 0ms;
    --duration-slow: 0ms;
  }
}
```

## Step 2: Import Fonts

Place the Google Fonts import at the top of the HTML or CSS. Build the URL from the guide's font specifications:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=[headingFont]:wght@[weights]&family=[bodyFont]:wght@[weights]&family=[monoFont]&display=swap" rel="stylesheet">
```

Replace spaces in font names with `+` in the URL.

## Step 3: Apply Base Styles

After the variables, set base typography and color on the body:

```css
body {
  font-family: var(--font-body);
  font-size: var(--text-base);
  line-height: var(--leading-normal);
  color: var(--text-primary);
  background-color: var(--bg-primary);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-heading);
  line-height: var(--leading-tight);
  color: var(--text-primary);
}

h1 { font-size: var(--text-4xl); font-weight: var(--font-bold); }
h2 { font-size: var(--text-3xl); font-weight: var(--font-semibold); }
h3 { font-size: var(--text-2xl); font-weight: var(--font-semibold); }
h4 { font-size: var(--text-xl); font-weight: var(--font-medium); }

code, pre {
  font-family: var(--font-mono);
}
```

## Step 4: Component Patterns

When building components, always reference the `components` section of the brand guide for styling decisions. Apply tokens, not raw values.

### Example: Button from brand guide

If the guide says buttons are "pill-shaped, primary fill, subtle lift on hover":

```css
.btn-primary {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  font-weight: var(--font-semibold);
  padding: var(--space-2) var(--space-5);
  background-color: var(--color-primary);
  color: var(--color-primary-contrast);
  border: none;
  border-radius: var(--radius-full);
  cursor: pointer;
  transition: transform var(--duration-fast) var(--ease-default),
              box-shadow var(--duration-fast) var(--ease-default);
}

.btn-primary:hover {
  transform: translateY(-1px);
  box-shadow: var(--shadow-md);
}
```

Every value traces back to a brand token. Nothing is invented.

## Step 5: Tailwind / Utility Class Translation

If the user is using Tailwind, map brand tokens to Tailwind's theme:

```js
// tailwind.config.js (reference, not generated)
module.exports = {
  theme: {
    colors: {
      primary: {
        DEFAULT: 'var(--color-primary)',
        light: 'var(--color-primary-light)',
        dark: 'var(--color-primary-dark)',
      },
      // ... etc
    },
    fontFamily: {
      heading: 'var(--font-heading)',
      body: 'var(--font-body)',
      mono: 'var(--font-mono)',
    },
  }
}
```

For artifacts using Tailwind utility classes, you cannot customize the theme at runtime. Instead, use inline styles via `style` attributes for brand-specific values, or use the CSS custom properties in a `<style>` block alongside Tailwind classes.

## Step 6: Self-Audit Checklist

Before delivering any frontend output, verify:

- [ ] `:root` block contains all brand tokens
- [ ] Fonts are imported correctly
- [ ] No hardcoded color values (search for `#`, `rgb(`, `hsl(`)
- [ ] No hardcoded font-family (search for `font-family:` not using `var(--font-`)
- [ ] Spacing uses scale values (no arbitrary px/rem values)
- [ ] Border radii use tokens
- [ ] Shadows use tokens
- [ ] Motion durations and easings use tokens
- [ ] `prefers-reduced-motion` is respected
- [ ] No violations of the "don'ts" list from the guide

If any check fails, fix it before presenting to the user.

## React / JSX Specifics

When building React artifacts, apply brand tokens through a combination of:

1. A `<style>` tag in the component with the `:root` variables
2. Inline styles referencing `var(--token-name)` where Tailwind classes can't cover it
3. Tailwind classes for layout and common utilities

```jsx
const styles = {
  button: {
    backgroundColor: 'var(--color-primary)',
    color: 'var(--color-primary-contrast)',
    borderRadius: 'var(--radius-full)',
    padding: 'var(--space-2) var(--space-5)',
    fontFamily: 'var(--font-body)',
    fontWeight: 'var(--font-semibold)',
    fontSize: 'var(--text-sm)',
    border: 'none',
    cursor: 'pointer',
    transition: `transform var(--duration-fast) var(--ease-default)`,
  }
};
```
