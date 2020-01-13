# Style Guide - VSCODE :boom:
Configuração default de style guide.

### 0 - Install Extensions in VS Code
* EditorConfig for VS Code
* ESLint
* Prettier - Code formatter

### 1 - Gerar .editorconfig
Clicar com botão direito no diretório raíz do VSCODE e ***Generate .editorconfig***
Dentro do arquivo copiar o código:
```
root = true

[*]
end_of_line = lf
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

### 2 - Delete eslint
Apagar arquivo do eslint, se houver, e instalar o eslint como dependência de desenvolvimento:
```
yarn add eslint -D && yarn eslint --init
```
### Obs: Após rodar o comando eslint --init, algumas opções deverão ser selecionadas:
> How would you like to use ESLint? (Como você gostaria de utilizar o ESLint?)

 To check syntax, find problems, and enforce code style

> What type of modules does your project user? (Quais tipos de módulos o seu projeto usa?)

Javascript modules (import/export)

> Which framework does your project use? (Qual framework o seu projeto usa?)
 
React, Vue ou None of theses

> Does your project use TypeScript? (y/N) (O seu projeto usa TypeScript?)
 
N

> Where does your code run? (Onde irá rodar seu projeto?)

Browser ou Node (use a barra de espaço para desmarcar uma opção. No caso do react native, desmarque todas.)

> Use a popular style guide (Utilize uma guia de estilo popular)

Use a popular style guide

> Which style guide do you want to follow? (Qual guia de estilo deseja seguir?)

Airbnb 

> What format do you want your config file to be in? (Em que formato você deseja que o seu arquivo de configuração esteja?)

JavaScript

> Would you like to install them now with npm? (Y/n) (Gostaria de instalar as dependências com npm?)

Y



### 3 - Delete package-lock
Apagar aquivo ***package-lock.json*** para associar as dependências ao arquivo ***yarn.lock*** e reinstalar utilizando o comando abaixo:
```
yarn 
```

### 4 - Install Prettier
Instalar dependências do prettier e babel-eslint conforme abaixo:
```
yarn add prettier eslint-config-prettier eslint-plugin-prettier babel-eslint -D 
```

### 5 - Add to eslintrc
No arquivo ***.eslintrc.js*** copiar as configurações:
```
module.exports = {
  env: {
    es6: true,
  },
  extends: ['plugin:react/recommended', 'airbnb', 'prettier/react'],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  parser: 'babel-eslint',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  plugins: ['react', 'prettier'],
  rules: {
    'linebreak-style': ['error', 'windows'],
    'linebreak-style': 0,
    'prettier/prettier': 'error',
    'react/jsx-filename-extension': [
      'warn',
      {
        extensions: ['.jsx', '.js'],
      },
    ],
    'import/prefer-default-export': 'off',
  },
};
```

### 6 - Add to prettierrc
Criar arquivo ***.prettierrc*** com configurações de single quote:
```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

### 7 - Add to settings
Para que as configurações sejam aplicadas ao salvar o arquivo, no arquivo principal de configurações do VSCODE ***settings.json*** (ctrl + shift + P) adicione a seguinte linha:
```
"editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
``` 


Ambiente configurado! Só começar a codar. :coffee: :raised_hands: 
