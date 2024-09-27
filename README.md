# rollup-rename-package 🚀

A blazing-fast, highly customizable Rollup plugin to rename package imports **after** bundling. It modifies JavaScript/TypeScript import paths and `package.json` dependencies, giving you complete control over your naming conventions.

Have you ever wanted to rename or alias packages without disrupting the ecosystem? You're in the right place! `rollup-rename-package` helps you seamlessly swap out package names in bundled files and `package.json` with zero effort.

From

```js
// ESM
import { FeatureFlags } from  '@my-org/old-package';
// CJS
var  oldPackageName  =  require('@my-org/old-package');
```

To

```js
// ESM
import { FeatureFlags } from  '@my-new-org/new-package';
// CJS
var  oldPackageName  =  require('@my-new-org/new-package');
```

> For the sake of consistency, `rollup-rename-package` doesn't replace the rollup generated `oldPackageName` variable name; if you see any importance in it, feel free to open a PR to toggle this functionality

## Features 🌟

- **Blazing Fast ⚡**: Parallel file processing for maximum performance.
- **Super Customizable**: Define your charset, file extensions, and dependency keys!
- **Plug and Play**: Works out of the box with zero configuration.
- **Async Everything**: Fully asynchronous for non-blocking performance.

## Install 🛠️

```bash
npm install --save-dev rollup-rename-package
```

## Usage 💡

Add `rollup-rename-package` to your Rollup config:

```js
import renamePackages from "rollup-rename-package";

export default {
  input: "src/index.js",
  output: {
    dir: "dist",
    format: "cjs",
  },
  plugins: [
	// ...
    renamePackages({
      alias: [
        { originalPackageName: "@my-org/old-package-A", newPackageName: "@my-new-org/new-package-A" },
        { originalPackageName: "@my-org/old-package-B", newPackageName: "@my-new-org/new-package-B" },
      ],
      // Optional - override which file extensions should be edited
      fileExtensions: /\.(js|ts|d\.ts|jsx|tsx)$/,
      // Optional - override which charset should be used for file read/write
      charset: "utf-8",
      // Optional - override which package.json dependency types should be edited
      dependencyKeys: [
        "dependencies",
        "devDependencies",
        "peerDependencies",
        "optionalDependencies",
      ],
    }),
    // ..
  ],
};
```

## Options 🎛️

- **`alias`**: **(Required)** An array of objects with originalPackageName and
  newPackageName to specify your renaming preferences.
- `fileExtensions`: (Optional) A regex for which file extensions to apply
  the renaming. Defaults to /\.(js|ts|d\.ts|jsx|tsx)$/

- `charset`: (Optional) The
  charset used for reading/writing files. Defaults to utf-8.
- `dependencyKeys`: (Optional) An array of package.json keys to update.
  Defaults to ['dependencies', 'devDependencies', 'peerDependencies',
  'optionalDependencies'].

## Contributing 🤝

PRs are welcome! Let’s improve package renaming. For features, bugs, and discussions, check out the issue tracker.

Let’s Rename Together! 🌍✨

Happy coding from the `rollup-rename-package` team! 🎉
