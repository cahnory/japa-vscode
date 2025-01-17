<div align="center">
  <img width="650px" src="https://user-images.githubusercontent.com/8337858/187943614-8faa9500-d7e8-463c-b5f7-3ece742827fd.png" />
  <h1>🧪 Japa extension for VSCode</h1> <br/>
</div>

## Features
* [Vscode Testing API](https://code.visualstudio.com/api/extension-guides/testing) integration 
* Run tests without typing anything. Either with a shortcut, Code Lenses, or using Vscode Test Explorer
* "See snapshot" codelens to quickly see the snapshot of a test ( for [@japa/snapshot](https://github.com/japa/snapshot) )
* Support multiple workspaces
* Support Javascript, Typescript, ESM, CJS
* Works with Adonis.js projects using Japa
* Snippets

## Demo

### Using Vscode Test Explorer
![](https://github.com/Julien-R44/japa-vscode/assets/8337858/0eba59be-3897-4a70-95a2-06b1195b85b0)

### Using Code Lenses
![](https://user-images.githubusercontent.com/8337858/187944316-c1b5f0c4-2ea2-46f1-9437-a7433db8a2eb.gif)

## Instructions

### Test Explorer
If you wish to use the vscode test explorer integration, you will need to have Japa version `3.0.0` or higher to be able to use the `--reporter` flag.

Also note that you need to have the `ndjson` reporter activated in your Japa config file, since we are using it to communicate with the extension. `ndjson` is enabled by default if you don't have a `reporters` key in your config file. So if you have a `reporters` config, make sure to inclure `ndjson` in it.

```js
import { configure, processCLIArgs, run } from '@japa/runner'
import { assert } from '@japa/assert'
import { ndjson, spec } from '@japa/reporters'

processCLIArgs(process.argv.splice(2))
configure({
  files: ['tests/**/*.spec.js'],
  plugins: [assert()],
  reporters: {
    activated: ['spec'],
    list: [ndJson(), spec()], // 👈 Make sure to include ndjson
  }
})
```

## Configuration
- `tests.npmScript`: The npm script to run when executing tests. Defaults to `test`

  i.e if you set it to `test:unit`, the extension will run `npm run test:unit --flags` when executing tests
- `tests.enableCodeLens`: Show CodeLenses above each test. Defaults to `true`
- `tests.watchMode`: Run tests in watch mode when executed via shortcut/codelens. Defaults to `false`
- `tests.filePattern`: The glob pattern to use when searching for tests. Defaults to `**/*.{test,spec}.{ts,js}`
- `misc.useUnixCd`: Use Unix-style cd for windows terminals ( Useful when using Cygwin or Git Bash )
- `misc.disableNodeWarnings` : Disable node warnings by setting `NODE_NO_WARNINGS=1` when running tests. Defaults to `true`. 

## Keybindings
- `ctrl+shift+t`: Run the test at the cursor position
- `ctrl+shift+f`: Run the test file in the active editor

These keybindings can be easily changed in your VSCode configuration : 

- F1 -> Preferences: Open Keyboard Shortcuts
- Type `japa-vscode` in the search bar
- Change the `japa-vscode.runTest` or `japa-vscode.runTestFile` keybindings

## Snippets

All snippets are prefixed with `ja:`. Give it a try in your editor to see what's available.

## Contributing
* See [contributing guide](./.github/CONTRIBUTING.md)
* Clone the project and open it in VS Code
* Run `npm install`
* Press `F5` to open a new VSCode window with your extension loaded.
* You can relaunch the extension from the debug toolbar after changing code in `src/index.ts`.
* You can also reload (`Ctrl+R` or `Cmd+R` on Mac) the VS Code window with your extension to load your changes.
