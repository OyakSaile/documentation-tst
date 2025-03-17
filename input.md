# Input

The Input component is a versatile form control that supports various features including labels, status messages, tooltips, password visibility toggling, search functionality, and tag management. It's designed to be flexible and accessible while maintaining a consistent look and feel across the application.

## Features

- Label support with optional htmlFor attribute
- Status messages for validation feedback
- Tooltip integration with customizable position and content
- Password input with show/hide text functionality
- Search input variant with icon
- Tag management system
- Custom icon support
- Clear value functionality
- Space variants for different layout needs
- Full HTML input attribute support

## Component Structure

The Input component consists of several optional elements that can be combined based on needs:

```
┌─────────────────────────────────────────────────┐
│ Label                                          │
├─────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────┐ │
│ │ Tag1 Tag2 Tag3 +2                           │ │
│ │                                             │ │
│ │ Input field with optional icon              │ │
│ │                                             │ │
│ └─────────────────────────────────────────────┘ │
│ Status message (optional)                      │
└─────────────────────────────────────────────────┘
```

## Usage Examples

### Basic Input with Label

```tsx
import { Input } from "@ccr/ui-components-react";

<Input
  label="Username"
  placeholder="Enter your username"
  htmlFor="username-input"
/>;
```

### Input with Tags

```tsx
import { Input, Tag, Icons } from "@ccr/ui-components-react";
import { useState, useRef } from "react";

const InputWithTags = () => {
  const [selectedTags, setSelectedTags] = useState<string[]>([]);
  const inputRef = useRef<HTMLInputElement>(null);

  const handleSelectItem = (tag: string) => {
    setSelectedTags((prev) => prev.filter((t) => t !== tag));
  };

  return (
    <Input
      ref={inputRef}
      placeholder="Select items"
      label="Tags"
      toolTipPosition="top"
      tooltipTitle="Select multiple items"
      customIcon={<Icons.ChevronBottom />}
      readOnly
      onClick={() => setIsDropdownOpen((prev) => !prev)}
      tags={
        <InputTags
          selectedTags={selectedTags}
          inputWidth={inputRef.current?.offsetWidth}
          onClickTag={handleSelectItem}
        />
      }
    />
  );
};
```

### Search Input

```tsx
import { Input } from "@ccr/ui-components-react";

<Input isSearch placeholder="Search..." label="Search" />;
```

### Password Input

```tsx
import { Input, Icons } from "@ccr/ui-components-react";

const PasswordInput = () => {
  const [showText, setShowText] = useState(false);

  return (
    <Input
      type="password"
      label="Password"
      showText={showText}
      toggleShowText={() => setShowText(!showText)}
      customIcon={showText ? <Icons.EyeOff /> : <Icons.Eye />}
    />
  );
};
```

### Input with Status Message

```tsx
import { Input } from "@ccr/ui-components-react";

<Input
  label="Email"
  status="Please enter a valid email address"
  variant="negative"
/>;
```

## Props

| Property           | Type                                  | Required | Default   | Description                            |
| ------------------ | ------------------------------------- | -------- | --------- | -------------------------------------- |
| label              | string                                | No       | -         | Label text for the input               |
| status             | string \| ReactNode                   | No       | -         | Status message or component to display |
| variant            | "default" \| "positive" \| "negative" | No       | "default" | Visual variant of the input            |
| toolTipPosition    | TooltipPosition                       | No       | -         | Position of the tooltip                |
| tooltipTitle       | string                                | No       | -         | Title text for the tooltip             |
| tooltipDescription | string                                | No       | -         | Description text for the tooltip       |
| showText           | boolean                               | No       | -         | Controls password text visibility      |
| toggleShowText     | () => void                            | No       | -         | Function to toggle password visibility |
| customIcon         | ReactNode                             | No       | -         | Custom icon component                  |
| isSearch           | boolean                               | No       | false     | Enables search input styling           |
| onClearValue       | () => void                            | No       | -         | Function to clear input value          |
| space              | "default" \| "short"                  | No       | "default" | Controls input spacing                 |
| tags               | ReactNode                             | No       | -         | Tags component to display              |
| htmlFor            | string                                | No       | -         | ID for label association               |

## Variations

1. **Default Input**

   - Basic text input with label
   - Standard styling and behavior

2. **Search Input**

   - Search icon integration
     | Specialized styling for search functionality

3. **Password Input**

   - Show/hide text toggle
   - Secure text entry

4. **Input with Tags**

   - Tag management system
   - Dynamic tag display with overflow handling
   - Tag removal functionality

5. **Input with Status**

   - Validation feedback
   - Positive/negative states
   - Custom status messages

6. **Input with Tooltip**
   - Helpful context information
   - Customizable position
   - Title and description support

## Implementation Details

### Tag Management

The Input component supports a sophisticated tag management system through the `InputTags` component:

1. **Tag Display**

   - Tags are displayed within the input field
   - Handles overflow with a counter
   - Supports dynamic width calculation

2. **Tag Interaction**

   - Click to remove tags
   - Visual feedback on hover
   - Maintains input focus

3. **Responsive Behavior**
   - Automatically adjusts to container width
   - Shows overflow count when needed
   - Maintains accessibility

## Accessibility

- Proper label associations using htmlFor
- ARIA attributes for status messages
- Keyboard navigation support
- Screen reader friendly
- Clear visual feedback for states

## Dependencies

- React
- Icons from @ccr/ui-components-react
- Tooltip component
- Tag component

## Notes

- The component extends standard HTML input attributes
- Tag management requires the InputTags component
- Status messages can include both text and React components
- Tooltips are optional and configurable
- The component supports both controlled and uncontrolled modes
