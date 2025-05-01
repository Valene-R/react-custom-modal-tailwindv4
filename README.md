# react-custom-modal-tailwindv4

A customizable React modal component styled with **Tailwind CSS v4**


## Features

- Modal types: `success`, `error`, `info`, `warning`
- Fully styled using **Tailwind CSS v4**
- Close on backdrop click (configurable)
- Supports custom buttons and children
- Accessible (with `aria` attributes)
- Functional component with `PropTypes` validation


## Installation

```bash
npm install react-custom-modal-tailwindv4
```
Don't forget to have React 19+ and Tailwind CSS 4.x installed in your project.
This component uses Tailwind utility classes.

If Tailwind CSS v4 is not already configured in your project, follow the [official setup guide](https://tailwindcss.com/docs/installation).


## Peer dependencies

```json
{
  "react": ">=19",
  "react-dom": ">=19",
  "prop-types": "^15.8.1"
}
```


## Usage

```jsx
import Modal from 'react-custom-modal-tailwindv4';

<Modal
  isOpen={isModalOpen}
  onClose={() => setIsModalOpen(false)}
  type="success"
  title="Success"
  message="Your changes have been saved!"
  showCloseIcon={true}
  showCloseButton={true}
/>
```


## Props

| Name                   | Type       | Required | Default | Description                                                            |
|------------------------|------------|----------|---------|------------------------------------------------------------------------|
| `isOpen`               | `boolean`  | ✅       | —       | Controls the visibility of the modal                                   |
| `onClose`              | `function` | ✅       | —       | Callback fired when the modal is closed                                |
| `type`                 | `string`   | ✅       | —       | Modal type: `'success'`, `'error'`, `'warning'`, `'info'`              |
| `title`                | `string`   | ❌       | —       | Optional modal title                                                   |
| `message`              | `node`     | ✅       | —       | Content of the modal (text or JSX)                                     |
| `customButton`         | `node`     | ❌       | —       | Replaces default buttons with custom JSX                               |
| `showCloseIcon`        | `boolean`  | ❌       | `false` | Show an "X" icon to close the modal                                    |
| `closeOnBackdropClick` | `boolean`  | ❌       | `true`  | Close the modal when clicking outside the modal                        |
| `children`             | `node`     | ❌       | —       | Custom content injected inside the modal                               |
| `showCloseButton`      | `boolean`  | ❌       | `false` | Shows a default “Close” button                                         |
| `showActionButtons`    | `boolean`  | ❌       | `false` | Enables display of “Save” and “Cancel” buttons                         |
| `showSaveButton`       | `boolean`  | ❌       | `true`  | Show Save button (only if `showActionButtons` is `true`)               |
| `showCancelButton`     | `boolean`  | ❌       | `true`  | Show Cancel button (only if `showActionButtons` is `true`)             |
| `onSave`               | `function` | ❌       | —       | Function triggered when the Save button is clicked                     |
| `onCancel`             | `function` | ❌       | —       | Function triggered when the Cancel button is clicked                   |


## Example (with useState)

Below is a practical example using `useState` to control the modal after a successful user creation:

```jsx
import { useState } from 'react';
import Modal from 'react-custom-modal-tailwindv4';

const UserFormPage = () => {
  const [isModalOpen, setIsModalOpen] = useState(false);
  const [createdUser, setCreatedUser] = useState(null);

  const handleCreateUser = (userData) => {
    // Simulate saving data and show modal
    setCreatedUser(userData);
    setIsModalOpen(true);
  };

  return (
    <div className="p-4">
      {/* Your form component */}
      <UserForm onSubmit={handleCreateUser} />

      {/* Success modal displayed after form creation submission */}
      <Modal
        title="Success"
        message={
          <>
            User{' '}
            <strong className="text-2xl text-black">
              {createdUser?.firstName} {createdUser?.lastName}
            </strong>{' '}
            has been created!
          </>
        }
        isOpen={isModalOpen}
        onClose={() => setIsModalOpen(false)}
        type="success"
        showCloseIcon={true}
        showCloseButton={true}
      />
    </div>
  );
};
```


## TailwindCSS Purge Notice (build)

This modal uses dynamic class names based on the `type` prop (`success`, `error`, `info`, `warning`) and conditional rendering.  
To ensure all Tailwind styles are preserved in production, you must safelist the following classes in your `tailwind.config.js`:

```js
// tailwind.config.js
export default {
  content: ['./index.html', './src/**/*.{js,jsx}'],
  safelist: [
    // Borders & Colors
    'border-green-500', 'border-red-500', 'border-yellow-500', 'border-blue-500', 'border-4',
    'text-green-700', 'text-red-700', 'text-yellow-700', 'text-blue-700',
    'bg-green-500', 'bg-red-500', 'bg-yellow-500', 'bg-blue-500', 'bg-gray-500', 'bg-white', 'bg-black/70',
    'hover:bg-green-700', 'hover:bg-red-700', 'hover:bg-yellow-700', 'hover:bg-blue-700', 'hover:bg-gray-700',

    // Text & Font
    'text-lg', 'text-xl', 'text-2xl', 'text-black', 'font-bold', 'font-normal',

    // Spacing
    'px-6', 'py-2', 'py-5', 'mx-2', 'mt-5', 'gap-4',

    // Layout & Flex
    'fixed', 'inset-0', 'flex', 'items-center', 'justify-center', 'relative', 'text-center',

    // Sizing
    'max-h-[90vh]', 'overflow-y-auto', 'rounded-xl', 'rounded-lg', 'size-5',

    // Positioning
    'absolute', 'top-1', 'right-1',

    // Effects & States
    'shadow-lg', 'cursor-pointer', 'focus:ring-1', 'focus:ring-black', 'focus:outline-none',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```


## License

This project is licensed under the MIT License.