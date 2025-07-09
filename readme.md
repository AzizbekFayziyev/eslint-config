# ⚙️ ESLint, Prettier & Husky: Full Integration (TypeScript + Next.js)

A complete step-by-step guide to integrating **ESLint**, **Prettier**, and **Husky** in a project using **TypeScript** and **Next.js**.

---

## 📦 Step 1: Install Dependencies

Install all required packages:

```bash
npm i -D eslint@8.57.1 prettier husky lint-staged
```

```bash
npm i -D @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

```bash
npm i -D eslint-config-airbnb-base eslint-plugin-import
```

```bash
npm i -D eslint-config-prettier eslint-plugin-prettier eslint-config-next
```

---

## 🛠️ Step 2: Configuration Files

### `.eslintrc.json`

```json
{
  "env": {
    "es2021": true,
    "node": true
  },
  "extends": [
    "airbnb-base",
    "plugin:@typescript-eslint/recommended",
    "next/core-web-vitals",
    "plugin:prettier/recommended",
    "prettier"
  ],
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint", "import"],
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module",
    "project": "./tsconfig.json"
  },
  "rules": {
    "no-console": "off",
    "no-void": "off",
    "import/extensions": "off",
    "no-unused-vars": [
      "warn",
      {
        "argsIgnorePattern": "^_"
      }
    ],
    "func-names": "off",
    "consistent-return": "off",
    "no-restricted-syntax": "off",
    "@typescript-eslint/indent": "off",
    "class-methods-use-this": "off",
    "@typescript-eslint/no-unused-vars": [
      "warn",
      {
        "argsIgnorePattern": "^_"
      }
    ],
    "@typescript-eslint/explicit-member-accessibility": "off",
    "@typescript-eslint/no-explicit-any": "error",
    "lines-between-class-members": "off",
    "camelcase": "off",
    "no-underscore-dangle": "off",
    "no-shadow": "off",
    "no-await-in-loop": "off",
    "radix": "off",
    "no-plusplus": "off",
    "no-promise-executor-return": "off",
    "import/no-duplicates": "off",
    "import/prefer-default-export": "off",
    "import/no-cycle": "off"
  },
  "settings": {
    "import/resolver": {
      "node": {
        "extensions": [".js", ".ts"]
      }
    }
  }
}
```

---

### `.eslintignore`

```
submodules/
node_modules/

dist/
build/
.next/

*.log
*.tmp
.temp/
migrations/

public/
static/

.vscode/
.idea/

.env*
```

---

### `prettier.config.cjs`

```js
/** @type {import("prettier").Config} */
module.exports = {
  semi: true,
  singleQuote: true,
  trailingComma: 'all',
  printWidth: 100,
  tabWidth: 4,
  useTabs: true,
  bracketSpacing: true,
  arrowParens: 'always',
  endOfLine: 'lf',
};
```

---

### `.prettierignore`

```
node_modules
build
dist
coverage
.next
.env
*.lock
submodules/
migrations/
```

---

## 🧾 Step 3: Set Up Husky and Pre-commit Hook

### Initialize Husky

```bash
npx husky
```

### Add `prepare` script to `package.json`

```json
"scripts": {
  "prepare": "husky"
}
```

### Create `.husky/pre-commit` and add:

```sh
#!/bin/sh

npx lint-staged
```

---

### Configure `lint-staged` in `package.json`

```json
"lint-staged": {
  "*.{ts,tsx,js,jsx}": [
    "eslint --fix",
    "prettier --write"
  ]
}
```

---

### Useful Scripts in `package.json`

```json
"scripts": {
  "format": "prettier --write .",
  "format:check": "prettier --check .",
  "eslint": "eslint . --ext .js,.ts,.tsx,.jsx --fix"
}
```

---

## ✅ Done!

Now, every commit will automatically run ESLint and Prettier. Your code will be linted and formatted before entering the repository.
