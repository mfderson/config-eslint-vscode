# Style Guide - VSCODE :boom:
Configuração default de style guide.

### 0 - Install Extensions in VS Code
* EditorConfig for VS Code
* ESLint

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
Y/N

> Where does your code run? (Onde irá rodar seu projeto?)

Browser ou Node (use a barra de espaço para desmarcar uma opção)
- No caso do react native, desmarque todas.)
- No caso de desenvolvimento do back com node, marque apenas Node.

> Use a popular style guide (Utilize uma guia de estilo popular)

Use a popular style guide

> Which style guide do you want to follow? (Qual guia de estilo deseja seguir?)

Airbnb 

> What format do you want your config file to be in? (Em que formato você deseja que o seu arquivo de configuração esteja?)

JSON

> The style guide "airbnb" requires eslint@^5.16.0 || ^6.8.0. You are currently using eslint@7.0.0. Do you want to downgrade?

No

> Would you like to install them now with npm?

No

Pega a linha gerada em cima do comando anterior e remova o eslint, pois já temos instalado.

Era assim:
```console
yarn add -D @typescript-eslint/eslint-plugin@latest eslint-config-airbnb-base@latest eslint@^5.16.0 || ^6.8.0 eslint-plugin-import@^2.20.1 @typescript-eslint/parser@latest
```

Ficou assim:
```console
yarn add -D @typescript-eslint/eslint-plugin@latest eslint-config-airbnb-base@latest eslint-plugin-import@^2.20.1 @typescript-eslint/parser@latest 
```

### 3 - Delete package-lock
Apagar aquivo ***package-lock.json*** para associar as dependências ao arquivo ***yarn.lock*** e reinstalar utilizando o comando abaixo:
```console
yarn 
```

### 4 - Install Plugin Importer
```console
yarn add -D eslint-import-resolver-typescript
```

### 5 - Add to eslintrc
No arquivo ***.eslintrc.json*** copiar as configurações:

Para versão **Node - Backend**:
```javascript
{
  "env": {
    "es6": true,
    "node": true
  },
  "extends": [
    "airbnb-base",
    "plugin:@typescript-eslint/recommended",
    "prettier/@typescript-eslint",
    "plugin:prettier/recommended"
  ],
  "globals": {
    "Atomics": "readonly",
    "SharedArrayBuffer": "readonly"
  },
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": 11,
    "sourceType": "module"
  },
  "plugins": [
    "@typescript-eslint",
    "prettier"
  ],
  "rules": {
    "prettier/prettier": "error",
    "import/extensions": [
      "error",
      "ignorePackages",
      {
        "ts": "never"
      }
    ]
  },
  "settings": {
    "import/resolver": {
      "typescript": {}
    }
  }
}
```
Para a versão **web/mobile**:
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
    'import-helpers/order-imports': [
      'warn',
      {
        newlinesBetween: 'always',
        groups: ['/^react/', 'module', '/^~/', ['parent', 'sibling', 'index']],
        alphabetize: { order: 'asc', ignoreCase: true },
      },
    ],
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

Crie o arquivo .eslintingnore na raiz. Ele terá o seguinte conteúdo:
```
/*.js
node_modules
dist
```

### 6 - Install Prettier
Instalar dependências do prettier:
```console
yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```

Crie o arquivo prettier.config.js na raiz. Ele terá o seguinte conteúdo:
```javascript
module.exports = {
  singleQuote: true,
  trailingComma: "all",
  arrowParens: "avoid",
};
```

### 7 - Add to settings.json
Para que as configurações sejam aplicadas ao salvar o arquivo, no arquivo principal de configurações do VSCODE ***settings.json*** (ctrl + shift + P) adicione a seguinte linha:
```json
"[javascript]": {
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
},

"[javascriptreact]": {
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true 
  }
},

"[typescript]": {
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true 
  }
},

"[typescriptreact]": {
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
``` 

### 8 - Configurando Debug no VSCode

- Clique no play com a barata na barra lateral

- Clique em *create a launch.json file*

- O conteúdo do arquivo deve ficar assim:
```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "protocol": "inspector",
      "restart": true,
      "name": "Debug",
      "skipFiles": [
        "<node_internals>/**"
      ],
      "outFiles": [
        "${workspaceFolder}/**/*.js"
      ]
    }
  ]
}
```

- Adicione no **package.json** a propriedade **--inspect** em sua script de dev. Deve ficar como abaixo (por exemplo):
```json
"scripts": {
  "build": "tsc",
  "dev:server": "ts-node-dev --inspect --transpileOnly --ignore-watch node_modules src/server.ts"
},
```

- Agora com o projeto rodando ou não, vá no ícone de play com a barata e dê um **run**.

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
