# eslint-config-md

[![npm version](https://badge.fury.io/js/eslint-config-md.svg)](https://badge.fury.io/js/eslint-config-md)

These are the settings for ESLint and Prettier I use for  my personal projects

## Installation

You can use this config **globally** and/or **locally** per project.

It's best to install this locally once per project, that way you can have project specific settings as well as sync those settings with others working on your project via git.

### Local / Per Project Install

1. If you don't already have a `package.json` file, create one with `npm init -y`.

2. Then we need to install everything needed by the config:

    ```
    npx install-peerdeps eslint-config-md@latest --dev
    ```

3. You can see in your `package.json` there are now a big list of devDependencies.

4. Create a `.eslintrc.json` file in the root of your project's directory (it should live where `package.json` does). Your `.eslintrc.json` file should look like this:

    ```json
    {
      "extends": ["md"]
    }
    ```

      Tip: You can alternatively put this object in your `package.json` under the property `"eslintConfig":`. This makes one less file in your project.

5. You can add two scripts to your package.json to lint and/or fix:

    ```json
    "scripts": {
      "lint": "eslint . --ext .js,.ts",
      "lint:fix": "eslint . --ext .js,.ts --fix"
    },
    ```

6. Now you can manually lint your code by running `npm run lint` and fix all fixable issues with `npm run lint:fix`.
   You probably want your editor to do this though.

## Overriding

If you'd like to override `eslint` or `prettier` settings, you can add the rules in your `.eslintrc.json` file.

The ESLint rules go directly under `"rules"` while prettier options go under `"prettier/prettier"`.

Note that prettier rules overwrite anything in this config (trailing comma, and single quote), so you'll need to include those as well.

```json
{
  "extends": ["md"],
  "rules": {
    "prettier/prettier": [
      "error",
      {
        "printWidth": 120,
        "semi": true,
        "singleQuote": true,
        "tabWidth": 4,
        "trailingComma": "es5"
      }
    ]
  }
}
```

Overrides can also be added to React package.json.

## Usage

### With VS Code

You should read this entire thing. Serious!

Once you have done one, or both, of the above installs. You probably want your editor to lint and fix for you. Here are the instructions for VS Code:

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Now we need to setup some VS Code settings via `Code/File` → `Preferences` → `Settings`. It's easier to enter these settings while editing the `settings.json` file, so click the `{}` icon in the top right corner:

```js
"editor.formatOnSave": true,
"[javascript]": {
  "editor.formatOnSave": false
},
"[javascriptreact]": {
  "editor.formatOnSave": false
},
"[typescript]": {
  "editor.formatOnSave": false
},
"[typescriptreact]": {
  "editor.formatOnSave": false
},
"eslint.workingDirectories": [
  {
    "mode": "auto"
  }
],
"editor.codeActionsOnSave": {
  "source.fixAll": true
}
```

### With Create React App

1. Run `npx install-peerdeps --dev eslint-config-md`
1. Open your `package.json` and replace `"extends": "react-app"` with `"extends": "md"`

## Not working

Start fresh. Sometimes npm modules can goof you up.

This will remove them all from the project.

```
npm remove eslint eslint-config-airbnb eslint-config-prettier eslint-plugin-html eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks prettier
```

Then, remove your `package-lock.json` file and delete the `node_modules/` directory.

After uninstalled, follow the above instructions again from start.
