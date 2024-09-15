# Vue-starter-2024

# 1. Indulás a Quasar CLI-vel

> npm init quasar@latest

![Beállítások](images/npm_init_quasar.jpg 'Beállítások')

# 2. VS Code beállítása - ".vscode" mappa

## 2.1 Ajánlott bővítmények: .vscode/extensions.json

```
{
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode",
    "eamodio.gitlens",
    "formulahendry.auto-rename-tag",
    "formulahendry.auto-close-tag",
    "christian-kohler.npm-intellisense",
    "codecoaching.quasar-docs",
    "wemade.quasar-class-autocompletion",
    "antfu.iconify"
  ],
  "unwantedRecommendations": [
    "octref.vetur",
    "hookyqr.beautify",
    "dbaeumer.jshint",
    "ms-vscode.vscode-typescript-tslint-plugin"
  ]
}
```

> Az .editorconfig állomány a projekt root-ban felesleges, törölhető!

> A javasolt bővítmények megjelenítése: "@recommended" keresés, majd telepíteni őket.

## 2.2 tasks.json állomány létrehozása: .vscode/tasks.json

```
{
  // .vscode/tasks.json
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "type": "npm",
      "script": "dev",
      "group": {
        "kind": "build",
        "isDefault": true
      }
    },
    {
      "type": "npm",
      "script": "test",
      "group": {
        "kind": "test",
        "isDefault": true
      }
    }
  ]
}
```

> A projekt a **Ctrl-Shift-B** billentyű-kombinációval is futtatható, vagy:<br>
> npm run dev

## 2.3 Project VS Code beállítások: .vscode/settings.json

```
{
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": true,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": ["source.fixAll.eslint"],
  "editor.mouseWheelZoom": true,
  "editor.wordWrap": "on",
  "editor.minimap.enabled": false,
  "eslint.validate": ["javascript", "javascriptreact", "typescript", "vue"],
  "files.autoSave": "afterDelay",
  "git.enableSmartCommit": true,
  "git.confirmSync": false,
  "git.autofetch": true,
  "git.autofetchPeriod": 60,
  "prettier.printWidth": 120,
  "typescript.tsdk": "node_modules/typescript/lib",
  "files.exclude": {
    "**/.git": true,
    "**/.gitignore": true,
    "**/.vscode": false,
    "**/tsconfig.json": false,
    "**/package-lock.json": true,
    "**/dist": true,
    "**/node_modules": true,
    "**/*.js.map": true,
    "**/*.npmrc": true
  }
}
```

## 2.4 Beállítások a nyomkövetéshez: .vscode/launch.json

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "msedge",
      "request": "launch",
      "name": "vuejs: edge",
      "url": "http://localhost:8080",
      "webRoot": "${workspaceFolder}",
      "pauseForSourceMap": false,
      "sourceMapPathOverrides": {
        "webpack:///./*": "${webRoot}/*"
      },
      "skipFiles": ["${workspaceFolder}/node_modules/**/*"]
    },
    {
      "type": "chrome",
      "request": "launch",
      "name": "vuejs: chrome",
      "url": "http://localhost:8080",
      "webRoot": "${workspaceFolder}",
      "pauseForSourceMap": false,
      "sourceMapPathOverrides": {
        "webpack:///./*": "${webRoot}/*"
      },
      "skipFiles": ["${workspaceFolder}/node_modules/**/*"]
    }
  ]
}
```

>Nyomkövetés menete:
>1.  Indítsad el a fordítást a **Ctrl-Shift-B**-vel, vagy az "npm run dev" paranccsal
>2.  Zárjad be a megjelenő böngészőablakot (ha megjelenik)
>3.  Indítsad el az alkalmazást debug-módban az **F5**-el
>4.  Az új böngészőablak megnyitása után helyezz el a vizsgálni kívánt kódsorok elé töréspontokat (piros pontok)
>5.  Navigálj úgy az alkalmazásban, hogy a kódsorok végrehajtásra kerüljenek
>6.  Vizsgáld a változók tartalmát, figyeld/folytasd a programsorok végrehajtását (**F10**, **F11**, **F5**)

## 2.5 Quasar beállítása: quasar.config.ts

```
extras: [
      // 'ionicons-v4',
      "mdi-v7",
      // 'fontawesome-v6',
      // 'eva-icons',
      // 'themify',
      // 'line-awesome',
      "roboto-font-latin-ext", // this or either 'roboto-font', NEVER both!

      // "roboto-font", // optional, you are not bound to it
      "material-icons", // optional, you are not bound to it
    ],
```

```
vueRouterMode: "history", // available values: 'hash', 'history'
```

```
devServer: {
  // https: true
  open: true, // opens browser window automatically
  port: 8080,
  vueDevTools: true
},
```
```
// Quasar plugins
plugins: ['Notify', 'Dialog', 'Loading', 'LocalStorage'],
```

## 2.6 Vue.js devtools bővítmény telepítése (Edge és Chrome böngészőkbe) és bekapcsolása

![Devtools](images/vuejs_devtools.jpg 'Vue.js Devtools bővítmény')
>Az automatikusan induló és az F5-el induló böngészőhöz is telepíteni kell
# 3. Forrásállományok formázása az új beállításokkal
>npm run format

# 4. Forrásállományok ellenőrzése ESLint-el
>npm run lint

# 5. Projekt futtatása
>Ctrl-Shift-B, vagy<br>
>npm run dev

# 6. A dotenv használata (pl.: jelszó tárolására)
## 6.1 Telepítés
```
npm i -D dotenv
```
## 6.2 Beállítás a quasar.config.js állományban
```
build {
   env: require('dotenv').config().parsed,
}
```
## 6.3 ".env" állomány létrehozása a project root-ban, változók megadása
```
BASE_URL=http://localhost:3000
```
## 6.4 Változó(k) elérése forráskódból:
```
  process.env.BASE_URL
```
## 6.5 ".gitignore" állomány bővítése, ha érzékeny adatok vannak a .env állományban
```
.env
```
