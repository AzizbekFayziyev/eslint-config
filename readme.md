
# ⚙️ ESLint, Prettier и Husky: Полная интеграция (TypeScript + Next.js)

Полное пошаговое руководство по подключению ESLint, Prettier и Husky к проекту с использованием TypeScript и Next.js.

---

## 📦 Шаг 1: Установка зависимостей

Установи все нужные пакеты:

```
npm i -D eslint prettier husky lint-staged
```

```
npm i -D @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

```
npm i -D eslint-config-airbnb-base eslint-plugin-import
```

```
npm i -D eslint-config-prettier eslint-plugin-prettier eslint-config-next
```

---

## 🛠️ Шаг 2: Конфигурационные файлы

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

public/
static/

.vscode/
.idea/

.env*
```

---

### `prettier.config.js`

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
```

---

## 🧾 Шаг 3: Настройка Husky и pre-commit hook

### Инициализируй Husky

```bash
npx husky install
```

### Добавь `prepare` скрипт в `package.json`

```json
"scripts": {
  "prepare": "husky install"
}
```

### Создай `.husky/pre-commit` и вставь:

```sh
#!/bin/sh

npx lint-staged
```

---

### Конфигурация `lint-staged` в `package.json`

```json
"lint-staged": {
  "*.{ts,tsx,js,jsx}": [
    "eslint --fix",
    "prettier --write"
  ]
}
```

---

### Полезные скрипты в `package.json`

```json
"scripts": {
  "lint": "eslint . --ext .ts,.tsx,.js",
  "lint:fix": "eslint . --ext .ts,.tsx,.js --fix",
  "format": "prettier --write ."
}
```

---

## ✅ Готово!

Теперь каждый коммит будет автоматически запускать ESLint и Prettier. Код будет проверяться и форматироваться перед тем, как попасть в репозиторий.
