# Transition Input Refactor

Take-home technical exercise for a Software Engineer role.

A refactor of a real production React component — a complex, multi-mode input supporting Google Places autocomplete, select dropdowns, MobX state, and inline editing. The goal was to improve code quality, patterns, and maintainability within a 3-hour constraint.

**Company:** [Collective](https://collective.com)

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

## Instructions

How would you improve this code?

This is a real example from our codebase that regularly sees edits… or at least it was at one point in time. It contains some known flaws and less than optimal patterns. Refactor the code to have better patterns and best practices. You can use any patterns you see fit but…

Be prepared to present and discuss your refactored code!

We’ll conduct a mock code review to discuss your refactor. Explain your reasoning, the strategies you employed, and the tradeoffs you considered. There are lots of opportunities for improvement, more than anyone could tackle in the time allotted (3 hours maximum), and there are pieces of context missing from the example. Such is life.

You should be prepared to answer questions like:

- How would you improve this code?
- What would you do differently?
- How would you test this sample?
- What else would you need to test?

Rather than grading you on your level of completion, this exercise is designed to:

- Provide a real-world example of what kind of work you can accomplish, not a contrived algorithmic  example or toy project from scratch.
- Judge how you deal with ambiguity, missing context, and balancing tradeoffs and your experience with making incremental progress.
- Provide you a glimpse of some of the real work inside the codebase.
- Help us understand the technical value you can bring to the team.

Disclaimer: None of your code will be used for anything other than this discussion.

## Responses

### How would you improve this code?

  - Use functional component and hooks
  - Using transaction info hook and passing it as prop for each field input instead of using React context in interest of time
  - Use TypeScript

### What would you do differently?

  - Organize the code into components

### How would you test this sample?

  - Tested it by doing manual testing and deploying it

### What else would you need to test?

  - Use unit tests like Jest or end to end testing like Cypress

## Notes

### Old Component

This code is a React component named `TransitionInput`, which appears to serve as a specialized input component that integrates with other components and services, such as Google Places API (via `react-places-autocomplete`). It's also wired up to MobX, a state management library, using `inject` and `observer` decorators. Let's break it down step by step:

#### Imports:

1. **React**:
    - `React`, `Component`, and `Fragment` are imported for creating React components.

2. **MobX React**:
    - `observer` and `inject`: Used to make the component reactive to MobX store changes and to inject the store into the component.

3. **react-onclickout**:
    - `ClickOutHandler`: A component that detects when a click is made outside of it.

4. **react-places-autocomplete**:
    - Used for fetching and displaying Google Places suggestions.

5. **semantic-ui-react**:
    - `Input`: A basic input component from Semantic UI.

#### Component Decorators:

- `@inject("OnboardHykeStore")`: Injects the `OnboardHykeStore` into the component's props.
- `@observer`: Makes the component observe and re-render on any relevant observable data change from MobX.

#### Component State:

- `edit`: A flag to indicate whether the input is in edit mode.
- `hover`: A flag to check if the mouse is hovering over the component.
- `oldValue`: Holds the previous value before any changes were made during editing.

#### Component Methods:

1. **enterEditMode**: Checks if a transaction is approved, and if not, enters the edit mode.
2. **cancelEdit**: Reverts the changes made during editing and exits the edit mode.
3. **saveEdit**: Saves the changes and, depending on the conditions, might update client info or transaction info.
4. **convertToBoolean**: Converts a value (Yes/No/Select an option) to its boolean or null representation.
5. **setHoverTrue**: Sets the hover state to true under certain conditions.
6. **handleInputChange**: Updates the value in the store based on user input.
7. **handleAddressChanged**: Handles address input changes.
8. **handleAddressSelected**: Handles when an address is selected from the Google Places dropdown.
9. **render**: Defines the UI of the component. Depending on the props passed, the component can render various types of inputs.

#### Render Method:

The render method checks various props to determine how to display the input:

1. **Notes**: Renders a textarea for note-taking.
2. **Link**: Renders a clickable link.
3. **Default**: Renders either a select dropdown, a PlacesAutocomplete input, or a standard input depending on the props.

#### Example Usage:

The comments at the start of the component show how `TransitionInput` can be used. It provides various custom input behaviors based on the props passed to it.

#### Export:

Finally, the component is exported as `TransitionInput`.

Overall, this component serves as a flexible, reactive input handler, able to manage a variety of input types while integrating with an external API (Google Places) and an application state (MobX).
