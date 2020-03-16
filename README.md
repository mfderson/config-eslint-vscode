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
```console
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
```console
yarn 
```

### 4 - Install Prettier
Instalar dependências do prettier e babel-eslint conforme abaixo:
```console
yarn add prettier eslint-config-prettier eslint-plugin-prettier babel-eslint eslint-plugin-import eslint-import-resolver-babel-plugin-root-import -D 
```

### 6 - Add to eslintrc
No arquivo ***.eslintrc.js*** copiar as configurações:
```javascript
module.exports = {
  env: {
    es6: true
  },
  extends: ["plugin:react/recommended", "airbnb", "prettier/react"],
  globals: {
    Atomics: "readonly",
    SharedArrayBuffer: "readonly"
  },
  parser: "babel-eslint",
  parserOptions: {
    ecmaFeatures: {
      jsx: true
    },
    ecmaVersion: 2018,
    sourceType: "module"
  },
  plugins: ["react", "prettier"],
  rules: {
    "linebreak-style": ["error", "windows"],
    "linebreak-style": 0,
    "prettier/prettier": "error",
    "react/jsx-filename-extension": [
      "warn",
      {
        extensions: [".jsx", ".js"]
      }
    ],
    "import/prefer-default-export": "off",
    "no-param-reassign": "off",
    "no-console": ["error", { allow: ["tron"] }]
  }
};
```
Para a versão web/mobile:
```javascript
module.exports = {
  env: {
    es6: true,
    jest: true,
    browser: true,
  },
  extends: ['airbnb', 'prettier', 'prettier/react'],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
    __DEV__: true,
  },
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  plugins: [
    'react',
    'jsx-a11y',
    'import',
    'react-hooks',
    'prettier',
    'eslint-plugin-import-helpers',
  ],
  rules: {
    'prettier/prettier': 'error',
    'react/jsx-filename-extension': ['error', { extensions: ['.js', '.jsx'] }],
    'import/prefer-default-export': 'off',
    'no-unused-vars': ['error', { argsIgnorePattern: '^_' }],
    'react/jsx-one-expression-per-line': 'off',
    'global-require': 'off',
    'react-native/no-raw-text': 'off',
    'no-param-reassign': 'off',
    'no-underscore-dangle': 'off',
    camelcase: 'off',
    'no-console': ['error', { allow: ['tron'] }],
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn',
    'react/jsx-props-no-spreading': 'off',
    'import/no-named-as-default': 'off',
  },
  settings: {
    'import/resolver': {
      'babel-plugin-root-import': {
        rootPathSuffix: 'src',
      },
    },
  },
};
```

### 7 - Add to prettierrc
Criar arquivo ***.prettierrc*** com configurações de single quote:
```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

### 8 - Add to settings
Para que as configurações sejam aplicadas ao salvar o arquivo, no arquivo principal de configurações do VSCODE ***settings.json*** (ctrl + shift + P) adicione a seguinte linha:
```javascript
"editor.formatOnSave": true,
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true
}
``` 

### 9 - LEMBRETE: NÃO SE ESQUEÇA - MOBILE

Para rodar a versão mobile, é necessário alterar para o **JDK8**.
```console
sudo update-alternatives --config java
```

### 10 - Config root import

Com isso podemos utilizar o *"~"* para referenciar a pasta *src* do nosso projeto
```console
yarn add babel-plugin-root-import eslint-import-resolver-babel-plugin-root-import -D
```
- **Para mobile** o seu arquivo ***babel.config.js*** deve ficar assim:
```
module.exports = {
  presets: ['module:metro-react-native-babel-preset'],
  plugins: [
    [
      'babel-plugin-root-import',
      {
        rootPathSuffix: 'src',
      },
    ],
  ],
};
```

- Crie o arquivo ***jsconfig.json*** na raiz do projeto com o seguinte conteúdo:

Se o arquivo exibir algum erro, feche a abra o vscode novamente.
```
{
  "compilerOptions": {
    "baseUrl": "src",
    "paths": {
      "~/*": ["*"]
    }
  }
}
```

### 11 - Config [commitlint](https://github.com/conventional-changelog/commitlint) e [commitizen](https://github.com/commitizen/cz-cli)

Padronização de mensagens de commit.

- Instalar commitlint:
```console
yarn add @commitlint/{config-conventional,cli} -D
```

- Criar o arquivo *commitlint.config.js* na raiz do projeto com o seguinte conteúdo:
```javascript
module.exports = { extends: ['@commitlint/config-conventional'] };
```
ou pode criá-lo com o comando:
```console
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

- Instale o husky:
```console
yarn add husky -D
```

- Cole o conteúdo abaixo no arquivo *package.json* antes de devDependencies:
```javascript
"husky": {
  "hooks": {
    "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
  }
}
```

- Instale o commitizen:
```console
yarn add commitizen -D
yarn commitizen init cz-conventional-changelog --yarn --dev --exact
```

- Adicionar o seguinte conteúdo dentro do *package.json* na propriedade *husky:hooks*:
```
"prepare-commit-msg": "exec < /dev/tty && git cz --hook || true"
```

- Pronto!!! Agora você pode realizar um commit com o seguinte comando:
```console
git commit
```

Ambiente configurado! Só começar a codar. :coffee: :raised_hands: 
