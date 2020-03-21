# Eslint and Prettier Config

This repo contains my settings for ESLint and Prettier.
Checkout all my rules [here](https://github.com/eneax/eslint-config-eneax/blob/master/.eslintrc.js).

## Install

You can use eslint globally and/or locally per project.
I prefer to install it locally per single project, so I can have project specific settings:

- Create a `package.json` file with `npm init`.

- Install everything needed by the config:

```bash
npx install-peerdeps --dev eslint-config-eneax
```

- Create a `.eslintrc` file in the root of the project's directory and copy this:

```json
{
  "extends": ["eneax"]
}
```

- You can add two scripts to your package.json to lint and/or fix your code:

```json
"scripts": {
  "lint": "eslint <relative_path>",
  "lint:fix": "eslint <relative_path> --fix"
},
```

For instance, if all your code is in a `src/` folder:

```json
"scripts": {
  "lint": "eslint src/",
  "lint:fix": "eslint src/ --fix"
},
```

- Now you can manually lint your code by running `npm run lint` and fix all fixable issues with `npm run lint:fix`.

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

If you use VS Code and want it to lint all the errors for you, here are the instructions:

- Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- Setup VS Code settings via `Code` → `Preferences` → `Settings`:

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

## Not working?

- Remove all `eslint` modules that we installed previously:

```
npm remove eslint-config-eneax babel-eslint eslint eslint-config-prettier eslint-config-airbnb eslint-plugin-html eslint-plugin-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react prettier eslint-plugin-react-hooks
```

- Remove `package-lock.json` file and delete the `node_modules/` directory.

- Repeat above instructions again!
