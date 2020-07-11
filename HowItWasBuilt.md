## How it was built (2020)
#### Create nextjs project
```bash
npx create-react-app
```
Delete `pages/api`.

#### Typescript
```bash
touch tsconfig.json
yarn add --dev typescript @types/react @types/node
yarn dev
```
When you run `yarn dev` the `next-env.d.ts` file will be created. It's a declaration file to work with the next types.

`tsconfig.json` will be modified, so change `strict: true`, it will not allow anys for example.

Move `pages` to `src/pages`.

#### EditorConfig
*It will start the files with some settings like the tab size..*

Create the file `.editorConfig` and add the settings.

#### Eslint
*Find and fix problems in javascript code.*

Install plugin ESLint in Visual Studio Code.
```bash
npx eslit --init
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
yarn add --dev eslint-plugin-react@latest @typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest eslint@latest
```
The `.eslintrc.json` file will be created.

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

Config to React Version.
```bash
"settings": { "react": { "version": "detect" } }
```

`Package.json`
```bash
"scripts": { ..., "lint": "eslint src" }
```

#### Prettier(with ESLint)
*To format file like use single quote to everybody dev...*
```bash
yarn add --dev eslint-config-prettier eslint-plugin-prettier
```
In `.eslintrc.json`
```bash
"extends": [..., "plugin:prettier/recommended"]
```
Create file `.prettierrc` and add the settings.
Create file `.vscode/settings.json` and add the settings.

#### git hook with Husky and Lint-Staged
*Prevent errors in commits.*
```bash
yarn add --dev linst-staged husky
```
`Package.json`
```bash
"scripts": { ..., "lint": "eslint src --max-warnings=0" },
"husky": { "hooks": {  "pre-commit": "lint-staged" } },
"lint-staged": { "src/**/*": ["yarn lint --fix"] }
```

#### Jest
*Framework of test.*
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

`Package.json`
```bash
"scripts": { ..., "test": "jest" },
```

#### Testing Library and jest-dom
*Testing Library: Library of tests to work with react components.*
*jest-dom: Matchers of Jest*
[Download Testing Library Cheat Sheet](https://github.com/testing-library/react-testing-library/raw/master/other/cheat-sheet.pdf)

```bash
yarn add --dev @testing-library/react @testing-library/jest-dom
```
In `.jest/setup.ts`
```bash
import '@testing-library/jest-dom'
```
`Package.json`
`--bail` *to stop in first error*
`--findRelatedTests` *Run tests just in testable changed files*
```bash
"scripts": { ..., "test:watch": "yarn test --watch" },
"lint-staged": { "src/**/*": [..., "yarn test --findRelatedTests --bail"] }
```

#### Styled-components
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
```bash
yarn add styled-components
```
Jest integration.
```bash
yarn add --dev jest-styled-components
```
In `.jest/setup.ts`
```bash
import 'jest-styled-components'
```
