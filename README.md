# React Router v7 Demo

This repo was bootstrapped using React + TypeScript + Vite template, then modified to use react-router v7.

Basically, `reactRouter` plugin from `@react-router/dev/vite` is used to replace react plugin from Vite's `@vitejs/plugin-react`.

## TLDR;

```bash
mkdir /data/Labs/react_router_v7
cd /data/Labs/react_router_v7
pnpm create vite@latest .
pnpm update --latest
pnpm add react-router@pre @react-router/node@pre @react-router/serve@pre
pnpm add --save-dev @react-router/dev@pre
mkdir app
touch app/root.tsx
touch app/home.tsx
touch app/routes.ts
```

Then modify the following files respectively.

- [Root](./app/root.tsx)
- [Home](./app/home.tsx)
- [Routes](./app/routes.ts)
- [Vite Config](./vite.config.ts)
- [Vite App TS Config](./tsconfig.app.json)

Use the following command to invoke react-router (in place of vite):

```bash
pnpm exec react-router dev # start HMR dev
pnpm exec react-router build # generate production build
pnpm exec react-router-serve ./build/server/index.js # serve build result
```

The origin Vite's template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

- Configure the top-level `parserOptions` property like this:

```js
export default tseslint.config({
  languageOptions: {
    // other options...
    parserOptions: {
      project: ["./tsconfig.node.json", "./tsconfig.app.json"],
      tsconfigRootDir: import.meta.dirname,
    },
  },
});
```

- Replace `tseslint.configs.recommended` to `tseslint.configs.recommendedTypeChecked` or `tseslint.configs.strictTypeChecked`
- Optionally add `...tseslint.configs.stylisticTypeChecked`
- Install [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react) and update the config:

```js
// eslint.config.js
import react from "eslint-plugin-react";

export default tseslint.config({
  // Set the react version
  settings: { react: { version: "18.3" } },
  plugins: {
    // Add the react plugin
    react,
  },
  rules: {
    // other rules...
    // Enable its recommended rules
    ...react.configs.recommended.rules,
    ...react.configs["jsx-runtime"].rules,
  },
});
```
