# @krozamdev/vue-masked-password

A lightweight, customizable masked password input component for Vue3. This component allows you to securely mask password input fields and provides a customizable approach to controlling password visibility.
The InputMaskingPassword component is a password input field that includes masking functionality (hiding characters as the user types) and allows toggling to show or hide the password. It uses the `@krozamdev/masked-password` library to apply the masking and supports custom mask characters. The component also handles password input changes by passing the raw (unmasked) value via a callback function.

## Features

- **Masked Input**: Mask the entered password with a configurable mask character.
- **Password Toggle**: Option to show or hide the password input.
- **TypeScript Support**: Written in TypeScript for better type safety.
- **Easy Integration**: Can be easily integrated into any Vue3 form.
- **Lightweight**: Minimal JavaScript bundle size for better performance.
- **Cross-browser Compatibility**: Works across modern browsers.

## Installation

To install the package, use either npm or yarn, etc:

- npm
    ```bash
    npm install @krozamdev/vue-masked-password
    ```
- yarn
    ```bash
    yarn add @krozamdev/vue-masked-password
    ```
- pnpm
    ```bash
    pnpm add @krozamdev/vue-masked-password
    ```
- bun
    ```bash
    bun add @krozamdev/vue-masked-password
    ```

## Usage

Here’s an example of how to use the masked password input component in your Vue3 project:

```vue
<script setup lang="ts">
  import { ref } from 'vue'
  import InputMaskingPassword from "@krozamdev/vue-masked-password"

  const showPassword = ref(false);
  const handleChange = (originalValue: string) => {
    console.log("Password changed:", originalValue);
  };
  const togglePasswordVisibility = () => {
    showPassword.value = !showPassword.value;
  };
</script>

<template>
  <InputMaskingPassword
    :onChangeEvent="handleChange"
    :showPassword="showPassword"
    class="text-primary"
    :key="1"
  />

  <button @click="togglePasswordVisibility">
    {{ showPassword ? 'Hide Password' : 'Show Password' }}
  </button>
</template>
```

## Props

| Prop             | Type                                    | Description                                                                                      |
|------------------|-----------------------------------------|--------------------------------------------------------------------------------------------------|
| `onChangeEvent`  | `(originalValue: string)`               | Callback that fires when the password value changes.                                              |
| `maskCharacter`  | `string`                                | (Optional) The character used to mask the password. Defaults to `•`.                             |
| `showPassword`   | `boolean`                               | (Optional) Show or hide the password input. Defaults to `false`.                                  |
| `...props`        | `InputHTMLAttributes<HTMLInputElement>` | All other standard HTML input attributes are supported, such as `placeholder`, `class`, etc. |



## Development

To build the project locally:

1. Clone the repository:
    ```bash
    git clone https://github.com/krozamdev/vue-masked-password.git
    cd vue-masked-password
    ```
2. Install dependencies:
    ```bash
    yarn install
    ```
3. Run the build:
    ```bash
    yarn build
    ```
This will create the build output in the dist directory, including both CommonJS and ESM formats.

## Contributing

1. Fork the repository.
2. Create your feature branch (git checkout -b feature/my-feature).
3. Commit your changes (git commit -am 'Add new feature').
4. Push to the branch (git push origin feature/my-feature).
5. Create a new Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For support, please email [support@krozam.tech](mailto:support@krozam.tech).