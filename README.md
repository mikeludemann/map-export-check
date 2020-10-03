# Map export check

A simple cli tool that checks if the export map defined in a `package.json` file is correct and that the referenced files/folders exist.

Rules:

- Entries must start with a `.`
- Must have the following entries:
  - `.` = main export when you do `import * as foo from "my-package"`
  - `./` = allow deep import paths
  - `./package.json` = allow user to import the package's `package.json` file
- Entry type `import` must end with `.mjs`
- Entry file paths must be relative and start with a `.`
- All referenced files/folders must exist on disk

Example of a valid export map in `package.json`:

```json
{
  "name": "preact",
  "exports": {
    ".": {
      "browser": "./dist/preact.module.js",
      "umd": "./dist/preact.umd.js",
      "import": "./dist/preact.mjs",
      "require": "./dist/preact.js"
    },
    "./compat": {
      "browser": "./compat/dist/compat.module.js",
      "umd": "./compat/dist/compat.umd.js",
      "require": "./compat/dist/compat.js",
      "import": "./compat/dist/compat.mjs"
    },
    "./compat/server": {
      "require": "./compat/server.js"
    },
    "./package.json": "./package.json",
    "./": "./"
  }
}
```