# eslint-config-prettify

[![version](https://img.shields.io/npm/v/eslint-config-prettify-base.svg?style=flat-square)](http://npm.im/eslint-config-prettify-base)
[![MIT License](https://img.shields.io/npm/l/eslint-config-prettify-base.svg?style=flat-square)](http://opensource.org/licenses/MIT)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)
[![lerna](https://img.shields.io/badge/maintained%20with-lerna-cc00ff.svg?style=flat-square)](https://lerna.js.org/)

A set of prettify eslint configs with prettier and Airbnb rules include. Support for React/TypeScript/ES2019/Node.

This repo container 4 npm packages.

- `eslint-config-prettify-base` for ES2019 or Node project
- `eslint-config-prettify-react` for React JavaScript project
- `eslint-config-prettify-ts-base` for vanilla TypeScript project
- `eslint-config-prettify-ts-react` for React TypeScript project

## Quick start

Chose proper config 👆, and install dependencies. For example, `eslint-config-prettify-base`:

```bash
# Just those two dependencies, no need for extra parser, plugins or configs
yarn add --dev eslint eslint-config-prettify-base prettier
# Or using npm if you prefer
npm install --save-dev eslint eslint-config-prettify-base prettier
```

Upgrade your ESLint config

```json
// .eslintrc
{
  "root": true,
  "extends": ["eslint-config-prettify-base"]
}
```

## Configuration

### tsconfig path

`eslint-config-prettify-ts-react` and `eslint-config-prettify-ts-base` using command executing directory to detect `tsconfig.json`(for TypeScript path alias), try below configuration if you meet `Unable to resolve path to module ‘xxx’` error.

```js
{
  "extends": ["eslint-config-prettify-base"],
  "settings": {
    "import/parsers": {
      "@typescript-eslint/parser": [".ts", ".tsx"]
    },
    "import/resolver": {
      // use <root>/tsconfig.json
      "typescript": {
        // always try to resolve types under `<root/>@types` directory even it doesn't contain any source code, like `@types/unist`
        "alwaysTryTypes": true,
        // use <root>/path/to/folder/tsconfig.json
        "directory": "./path/to/folder"
      },

      // Multiple tsconfigs (Useful for monorepos)

      // use a glob pattern
      "typescript": {
        "directory": "./packages/*/tsconfig.json"
      },

      // use an array
      "typescript": {
        "directory": [
          "./packages/module-a/tsconfig.json",
          "./packages/module-b/tsconfig.json"
        ]
      },
  }
}
```

## Development

This monorepo managed by [lerna](https://lerna.js.org/) with yarn workspace.

### Install dependencies

```bash
# Trigger 'lerna bootstrap'
yarn
```

### Test

Unit tests write with jest

```bash
yarn test
```

### Commit

Commit message lint by [commitlint](https://github.com/conventional-changelog/commitlint) with config `@commitlint/config-conventional`, scope must be package's names.For example, `fix(base): import module unsolved`.

### Publish

```bash
# Create package CHANGELOG.md, increase package.json version and git commit and tag
yarn run release
# Publish release version
yarn run publish
```
