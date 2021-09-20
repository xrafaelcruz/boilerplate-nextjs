# How it was built (2021)

## Create nextjs project

```bash
yarn create next-app
```
```bash
What is your project named? boilerplate
```

Delete `pages/api`.
Delete `pages/_app.js`.
Delete `styles/global.css`.

## Typescript

```bash
touch tsconfig.json
yarn add --dev typescript @types/react
yarn dev
```

When you run `yarn dev` the `next-env.d.ts` file will be created. It's a declaration file to work with the next types.

`tsconfig.json` will be modified, so change `strict: true`, it will not allow anys for example.

Move `pages` to `src/pages`.
Rename `src/pages/index.js` to `src/pages/index.tsx`.

In `tsconfig.json` add `"baseUrl": "src"` and update imports.

## EditorConfig

_It will start the files with some settings like the tab size.._

Create the file `.editorConfig` and add the settings.

## Eslint

_Find and fix problems in javascript code._

Install plugin ESLint in Visual Studio Code.

```bash
npx eslint --init
```

- To check syntax and find problems
- JavaScript modules (import/export)
- React
- TypeScript? Y
- Browser
- JSON
- Install with npm? N

Copy plugins and install with yarn.

```bash
yarn add --dev eslint-plugin-react@latest @typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest
```

The `.eslintrc.json` file will be created.

Add `next/core-web-vitals` in extends.

React Hooks Lint.

```bash
yarn add --dev eslint-plugin-react-hooks
```

In `.eslintrc.json`

```bash
"plugins": ["react", "react-hooks", "@typescript-eslint"]
"rules": {
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
}
```

Disable prop-types.

```bash
"rules": { ..., "react/prop-types": "off" }
```

Disable import react, because React as a global variable in Next.js.

```bash
"rules": { ..., "react/react-in-jsx-scope": "off" }
```

Disable explicit module boundary types, it warns that it is always necessary to inform the type of the functions return.

```bash
"rules": { ..., "@typescript-eslint/explicit-module-boundary-types": "off" }
```

Config to React Version -> plugin:react/recommended

```bash
"settings": { "react": { "version": "detect" } }
```

In `package.json`

```bash
"scripts": { ..., "lint": "next lint src" }
```

## Prettier(with ESLint)

_To format file like use single quote to everybody dev..._

```bash
yarn add --dev --exact prettier
```

Create file `.prettierrc.json` and add the settings.


```bash
yarn add --dev eslint-plugin-prettier eslint-config-prettier 
```

In `.eslintrc.json`

```bash
"extends": [..., "plugin:prettier/recommended"]
"rules": {..., "prettier/prettier": ["error", { "endOfLine": "auto" }]}
```

Create file `.vscode/settings.json` and add the settings.

*You may need to restart vscode*

## Jest

_Framework of test._

```bash
yarn add --dev jest @babel/preset-typescript @types/jest
```

`.eslintrc.json`

```bash
"env": { ..., "jest": true, "node": true }
```

Create `jest.config.js` file and add the settings.
Create `.babelrc` file and add the settings(To work well with jest).
Create `.jest/setup.ts`.

In `package.json`

```bash
"scripts": { ..., "test": "jest" },
```

## Testing Library and jest-dom

_Testing Library: Library of tests to work with react components._
_jest-dom: Matchers of Jest_
[Download Testing Library Cheat Sheet](https://github.com/testing-library/react-testing-library/raw/master/other/cheat-sheet.pdf)

```bash
yarn add --dev @testing-library/react @testing-library/jest-dom
```

In `.jest/setup.ts`

```bash
import '@testing-library/jest-dom'
```

```bash
"scripts": { ..., "test:watch": "yarn test --watch" },
```

## Styled-components

_css-in-js._

```bash
yarn add --dev @types/styled-components babel-plugin-styled-components
```

In `.babelrc`

```bash
"plugins": [["babel-plugin-styled-components", { "ssr": true }]],
```

```bash
yarn add styled-components
```

Create `src/pages/_document.tsx` and add the settings.

Jest integration.

```bash
yarn add --dev jest-styled-components
```

In `.jest/setup.ts`

```bash
import 'jest-styled-components'
```

## Storybook

_To preview components and your documentation._

```bash
npx sb init
```

Will be create `.storybook` and `src/stories` folders

Will be modified `package.json`
After insert in `scripts storybook and build-storybook` the params `-s ./public` to use static images.

```bash
"scripts": {
    ...,
    "storybook": "start-storybook -s ./public -p 6006",
    "build-storybook": "build-storybook -s ./public"
},
"devDependencies": {
    "@babel/core": "",
    ...,
    "@storybook/addon-actions": "",
    "@storybook/addon-essentials": "",
    "@storybook/addon-links": "",
    "@storybook/react": "",
    ...,
    "babel-loader": "",
    ...
}
```

In `.storybook/main.js`

```bash
stories: ['../src/**/**/stories.tsx', ...]
```

In `.storybook/preview.js` add decorator settings.

## PWA

_To work offline, push notifications and more._

```bash
yarn add next-pwa
```

Create `next.config.js` and add settings.
Create `public/manifest.json` and add settings.

In `src/pages/_app`

```bash
<link rel="manifest" href="/manifest.json" />
```

Run
```bash
NODE_ENV=production yarn build
yarn start
```

Will be create `public/sw.js` and `public/workbox-*.js`.
Add both in `.gitignore`
