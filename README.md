# Eslint and Prettier Config

This repo contains my settings for ESLint and Prettier.
Checkout all my rules [here](https://github.com/eneax/eslint-config-eneax/blob/master/.eslintrc.js).

## Install

You can use eslint globally and/or locally per project.
I prefer to install it locally per project, so I can have project specific settings.

1. Create a `package.json` file with `npm init`.

2. Install everything needed by the config:

```bash
npx install-peerdeps --dev eslint-config-eneax
```

3. Create a `.eslintrc` file in the root of the project's directory and copy this:

```json
{
  "extends": ["eneax"]
}
```

4. You can add two scripts to your package.json to lint and/or fix:

```json
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint . --fix"
},
```

5. Now you can manually lint your code by running `npm run lint` and fix all fixable issues with `npm run lint:fix`.

## Settings

If you want to overwrite eslint or prettier settings, go to your `.eslintrc` file and you can add `rules`.
[ESLint rules](https://eslint.org/docs/rules/) go directly under `"rules"` while [prettier options](https://prettier.io/docs/en/options.html) go under `"prettier/prettier"`.

For instance:

```json
{
  "extends": ["eneax"],
  "rules": {
    "no-console": 2,
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true
      }
    ]
  }
}
```

## VS Code

If you use VS Code and want it to lint for you, here are the instructions:

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Setup VS Code settings via `Code` → `Preferences` → `Settings` or `Cmd + ,`:

```json
// These are all my auto-save configs
"editor.formatOnSave": true,
// turn it off for JS and JSX, we will do this via eslint
"[javascript]": {
  "editor.formatOnSave": false
},
"[javascriptreact]": {
  "editor.formatOnSave": false
},
// tell the ESLint plugin to run on save
"editor.codeActionsOnSave": {
  "source.fixAll": true
},
// Optional BUT IMPORTANT: If you have the prettier extension enabled for other languages like CSS and HTML, turn it off for JS since we are doing it through Eslint already
  "prettier.disableLanguages": ["javascript", "javascriptreact"],
```

## Create React App

1. First `npm run eject` or `yarn eject`
2. Run `npx install-peerdeps --dev eslint-config-eneax`
3. Open `package.json` and replace `"extends": "react-app"` with `"extends": "eneax"`

## Not working?

1. Remove all eslint modules that we installed previously:

```
npm remove eslint-config-eneax babel-eslint eslint eslint-config-prettier eslint-config-airbnb eslint-plugin-html eslint-plugin-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react prettier eslint-plugin-react-hooks
```

2. Remove `package-lock.json` file and delete the `node_modules/` directory.

3. Repeat above instructions again!
