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

## License

This project is licensed under the MIT License.