# Accordion

The Accordion component is designed for organizing content into collapsible sections, allowing users to show or hide content as needed. It displays a list of items with summaries that can be expanded to reveal more detailed content, making it ideal for FAQs, product details, or any content that benefits from progressive disclosure.

## Features

- Collapsible content sections
- Support for custom content in expanded sections
- Optional dividers between items
- Customizable titles and summaries
- Controlled and uncontrolled usage modes
- Imperative handle for programmatic control
- Async content loading support
- Smooth animations for expanding/collapsing

## Component Structure

The Accordion system consists of two main components:

1. **Accordion**: The parent container component that manages state and renders a collection of accordion items
2. **AccordionItem**: The individual collapsible section component that renders the summary, content, and handles interactions

### Visual Structure

```
┌─────────────────────────────────────────────────┐
│ Accordion Title (optional)                      │
├─────────────────────────────────────────────────┤
│ Summary Text 1                           ▼      │ ← Collapsed AccordionItem
├─────────────────────────────────────────────────┤
│ Summary Text 2                           ▲      │ ← Expanded AccordionItem (button)
├─────────────────────────────────────────────────┤
│                                                 │
│ Detailed content is displayed here when the     │ ← Expanded AccordionItem (content)
│ accordion item is expanded.                     │
│                                                 │
├─────────────────────────────────────────────────┤ ← Optional divider
│ Summary Text 3                           ▼      │ ← Collapsed AccordionItem
└─────────────────────────────────────────────────┘
```

## Usage Examples

### Basic Usage

```tsx
import { Accordion, useTheme } from "ui-components-web";

const { theme } = useTheme();

<Accordion
  title="Frequently Asked Questions"
  data={[
    {
      summary: "What is an accordion?",
      details: (
        <div style={{ width: "100%", paddingRight: theme.shape.inset.xxs }}>
          <BodyTypography size="large" color={theme.content.paragraphy.soft}>
            An accordion is a component that allows you to show or hide content
            sections. It's useful for organizing information in a compact way.
          </BodyTypography>
        </div>
      ),
      expanded: false,
      visibleDivider: true,
    },
    {
      summary: "How do I use it?",
      details: (
        <div style={{ width: "100%", paddingRight: theme.shape.inset.xxs }}>
          <BodyTypography size="large" color={theme.content.paragraphy.soft}>
            Simply provide an array of data items with summary and details
            properties. The component will handle the rest!
          </BodyTypography>
        </div>
      ),
      expanded: false,
      visibleDivider: true,
    },
  ]}
/>;
```

### Async Content Loading

```tsx
import { useRef, useState } from "react";
import {
  Accordion,
  AccordionImperativeRef,
  DataProps,
} from "ui-components-web";

const AsyncAccordion = () => {
  const accordionRef = useRef<AccordionImperativeRef>(null);
  const [data, setData] = useState<DataProps[]>([
    {
      summary: "Section 1",
      details: <LoadingIndicator />,
      expanded: false,
      visibleDivider: true,
    },
    {
      summary: "Section 2",
      details: <LoadingIndicator />,
      expanded: false,
      visibleDivider: true,
    },
  ]);

  async function handleClickedIndex(clickedIndex: number) {
    // Show loading state
    setData((prevData) => {
      const newData = [...prevData];
      newData[clickedIndex].details = <LoadingIndicator />;
      return newData;
    });

    // Expand the clicked section
    accordionRef.current!.toggleIndex(clickedIndex);

    // Fetch data (simulated)
    const result = await fetchData();

    // Update with actual content
    setData((prevData) => {
      const newData = [...prevData];
      newData[clickedIndex].details = (
        <div>
          <p>Content for section {clickedIndex}</p>
          <p>{result}</p>
        </div>
      );
      return newData;
    });
  }

  return (
    <Accordion
      data={data}
      isOutsideControlled
      ref={accordionRef}
      onClickedIndex={handleClickedIndex}
    />
  );
};
```

## Props

### Accordion Props

| Property            | Type                    | Required | Default  | Description                                                               |
| ------------------- | ----------------------- | -------- | -------- | ------------------------------------------------------------------------- |
| title               | string                  | No       | -        | Defines the title of the accordion section                                |
| data                | DataProps[]             | No       | -        | Array that defines the accordion items to be displayed                    |
| isOutsideControlled | boolean                 | No       | false    | Determines if the accordion state is controlled externally                |
| onClickedIndex      | (index: number) => void | No       | () => {} | Event handler for when an item is clicked (used with isOutsideControlled) |
| ...divProps         | HTMLDivElement          | No       | -        | Standard HTML div attributes                                              |

### AccordionItem Props

| Property      | Type                    | Required | Description                                                       |
| ------------- | ----------------------- | -------- | ----------------------------------------------------------------- |
| item          | DataProps               | Yes      | The data object containing summary, details, and other properties |
| index         | number                  | Yes      | The index of this item in the accordion items array               |
| expandedIndex | number \| null          | Yes      | The currently expanded item index, or null if none                |
| handleToggle  | (index: number) => void | Yes      | Function to call when toggling expansion state                    |

### DataProps

| Property       | Type             | Required | Default | Description                                     |
| -------------- | ---------------- | -------- | ------- | ----------------------------------------------- |
| id             | string \| number | No       | -       | Unique identifier for the accordion item        |
| summary        | string           | No       | -       | The text displayed in the collapsed state       |
| details        | React.ReactNode  | No       | -       | The content displayed when the item is expanded |
| expanded       | boolean          | No       | false   | Defines whether the item is initially expanded  |
| visibleDivider | boolean          | No       | false   | Determines if a divider is shown below the item |

### AccordionImperativeRef

| Property     | Type                    | Description                                           |
| ------------ | ----------------------- | ----------------------------------------------------- |
| accordionRef | HTMLDivElement \| null  | Reference to the accordion DOM element                |
| toggleIndex  | (index: number) => void | Function to programmatically toggle an accordion item |

## Variations

1. **Default Accordion**

   - Basic collapsible sections
   - Single item expansion at a time
   - Optional section title

2. **Async Content Accordion**

   - Dynamic content loading
   - Loading state handling
   - External state management

3. **Custom Content Accordion**

   - Support for rich content in expanded sections
   - Can include any React components
   - Flexible layout options

4. **Divider Variations**
   - Optional dividers between items
   - Visual separation of content sections

## Implementation Details

### Accordion Component

The main Accordion component:

1. Manages the expansion state of all accordion items
2. Renders the optional title using HeadingTypography
3. Maps through the data array to render AccordionItem components
4. Provides an imperative handle for external control when needed
5. Handles controlled and uncontrolled modes through the isOutsideControlled prop

### AccordionItem Component

The AccordionItem component:

1. Renders a button containing the summary text and a chevron icon
2. Toggles the expansion state when clicked by calling the handleToggle function
3. Conditionally renders the detailed content when expanded
4. Optionally renders a divider below the content

## Styling

The components use Tailwind CSS for styling:

- The AccordionItem container has a top margin (`mt-sm`)
- The button is styled as a flex container with items aligned and justified between the ends
- The chevron icon rotates based on the expansion state with a smooth transition animation
- The components are fully responsive and adjust to the width of their container

## Accessibility

- Proper ARIA attributes for accordion navigation
- Keyboard navigation support through button elements
- Clear visual indicators for expanded/collapsed states
- Smooth animations for better user experience

## Dependencies

- React
- Tailwind CSS (with tailwind-merge)
- HeadingTypography component
- LabelTypography component
- Divider component
- ChevronUp icon

## Notes

- Only one accordion item can be expanded at a time
- The component handles state internally but can be controlled externally through the isOutsideControlled prop
- When using isOutsideControlled, you must provide an onClickedIndex handler and manage the state yourself
- The imperative handle provides a way to programmatically control the accordion
- The component is responsive and adjusts to container width
