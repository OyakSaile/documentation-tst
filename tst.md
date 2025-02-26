# CaptionTypography Component

## Overview

The `CaptionTypography` component is a versatile text component designed for rendering caption text with customizable styling options. It's part of the UI component library and follows the design system guidelines.

## Installation

```bash
npm install @ccr/ui-components-web
```

## Import

```jsx
import { CaptionTypography } from "@ccr/ui-components-web";
```

## Basic Usage

```jsx
// Basic usage with default props
<CaptionTypography>Default caption text</CaptionTypography>

// With size variant
<CaptionTypography size="large">Large caption text</CaptionTypography>

// With custom HTML element
<CaptionTypography as="span">Caption as span</CaptionTypography>
```

## Props

| Prop        | Type                                 | Default    | Description                             |
| ----------- | ------------------------------------ | ---------- | --------------------------------------- |
| `children`  | ReactNode                            | -          | The content to be displayed             |
| `size`      | `"small"` \| `"large"`               | `"small"`  | Controls the font size and line height  |
| `as`        | ElementType                          | `"p"`      | HTML element to render the component as |
| `disabled`  | boolean                              | `false`    | Whether the text should appear disabled |
| `color`     | string                               | -          | Custom text color (CSS color value)     |
| `className` | string                               | -          | Additional CSS classes to apply         |
| `alignment` | `"left"` \| `"center"` \| `"right"`  | `"left"`   | Text alignment                          |
| `weight`    | `"normal"` \| `"medium"` \| `"bold"` | `"normal"` | Font weight                             |

Additionally, the component accepts all standard HTML attributes for the rendered element.

## Variants

### Size Variants

```jsx
// Small (default)
<CaptionTypography size="small">Small caption text</CaptionTypography>

// Large
<CaptionTypography size="large">Large caption text</CaptionTypography>
```

### Text Alignment

```jsx
// Left aligned (default)
<CaptionTypography alignment="left">Left aligned text</CaptionTypography>

// Center aligned
<CaptionTypography alignment="center">Center aligned text</CaptionTypography>

// Right aligned
<CaptionTypography alignment="right">Right aligned text</CaptionTypography>
```

### Font Weight

```jsx
// Normal weight (default)
<CaptionTypography weight="normal">Normal weight text</CaptionTypography>

// Medium weight
<CaptionTypography weight="medium">Medium weight text</CaptionTypography>

// Bold weight
<CaptionTypography weight="bold">Bold weight text</CaptionTypography>
```

### Disabled State

```jsx
<CaptionTypography disabled>Disabled caption text</CaptionTypography>
```

### Custom Color

```jsx
<CaptionTypography color="#8B5CF6">Purple caption text</CaptionTypography>
```

## Combining Props

You can combine multiple props to achieve the desired styling:

```jsx
<CaptionTypography
  size="large"
  weight="bold"
  alignment="center"
  color="#EF4444"
>
  Bold, large, centered, red text
</CaptionTypography>
```

## Custom HTML Element

The component can be rendered as any HTML element using the `as` prop:

```jsx
// As a span
<CaptionTypography as="span">Caption as span</CaptionTypography>

// As a label
<CaptionTypography as="label" htmlFor="input-id">Form label</CaptionTypography>

// As a heading
<CaptionTypography as="h6">Small heading</CaptionTypography>
```

## Styling

The component uses Tailwind CSS for styling with the following base styles:

- Font family: Sora
- Text transform: Uppercase
- Letter spacing: Wide
- Default font weight: Normal

### Size-specific styles:

- Small: 12px font size (text-xs) with 16px line height (leading-4)
- Large: 14px font size (text-sm) with 20px line height (leading-5)

### State-specific styles:

- Default: Gray-900 text color
- Disabled: Gray-400 text color

## Accessibility

- Use semantic HTML elements when possible (e.g., use `<h1>` through `<h6>` for headings)
- Ensure sufficient color contrast when using custom colors
- Avoid using color as the only means of conveying information

## Examples

### Basic Examples

```jsx
// Small caption (default)
<CaptionTypography>Small caption text</CaptionTypography>

// Large caption
<CaptionTypography size="large">Large caption text</CaptionTypography>

// Disabled caption
<CaptionTypography disabled>Disabled caption text</CaptionTypography>
```

### Styling Examples

```jsx
// Custom color
<CaptionTypography color="#8B5CF6">Purple caption text</CaptionTypography>

// Centered text
<CaptionTypography alignment="center">Centered caption text</CaptionTypography>

// Right-aligned text
<CaptionTypography alignment="right">Right-aligned caption</CaptionTypography>

// Bold text
<CaptionTypography weight="bold">Bold caption text</CaptionTypography>

// Medium weight text
<CaptionTypography weight="medium">Medium weight caption</CaptionTypography>
```

### Combined Properties

```jsx
<CaptionTypography
  size="large"
  weight="bold"
  alignment="center"
  color="#EF4444"
>
  Combined properties example
</CaptionTypography>
```

### Custom HTML Element

```jsx
<CaptionTypography as="span">Caption as span element</CaptionTypography>
```

### Long Text Example

```jsx
<CaptionTypography>
  This is a longer caption text that might wrap to multiple lines depending on
  the container width. It demonstrates how the component handles longer content.
</CaptionTypography>
```

## Implementation Details

The component is built using:

- React for component structure
- Tailwind CSS for styling
- Tailwind Variants for managing style variants

## Related Components

- `BodyTypography` - For body text
- `HeadingTypography` - For headings
- `LabelTypography` - For form labels
