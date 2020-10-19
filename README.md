# Storybook6 building with Errors with Yarn 2 monorepo + React + Typescript

### Solution Upgrade to Storybook v6.1.0-alpha.8 or greater

[related issue](https://github.com/storybookjs/storybook/issues/12805#issuecomment-711153013)

As of 2020.10.19, storybook 6.1 is in prerelease mode.

Installing this versio can be done using the command `sb upgrade --prerelease`.

After upgrading to `6.1.0-alpha.26`, and running storybook, I get the following error:

```
ERR! Error: @storybook/addon-docs tried to access webpack (a peer dependency) but it isn't provided by your application; this makes the require call ambiguous and unsound.
ERR!
ERR! Required package: webpack (via "webpack")

.... more skipped lines ...

ERR!  Error: @storybook/addon-docs tried to access webpack (a peer dependency) but it isn't provided by your application; this makes the require call ambiguous and unsound.
ERR!
ERR! Required package: webpack (via "webpack")
.... more skipped lines ...

info => Loading config/preview file in "./.storybook".
info => Loading config/preview file in "./.storybook".
info => Adding stories defined in ".storybook/main.js".
info => Using default Webpack setup.
webpack built db2ea4bcf84a1d328d11 in 9169ms
⚠ ｢wdm｣: Hash: db2ea4bcf84a1d328d11
Version: webpack 4.44.2
Time: 9169ms
Built at: 10/19/2020 10:33:37 AM

.... more skipped lines ...

WARNING in ./stories/Introduction.stories.mdx 11:0
Module parse failed: Unexpected token (11:0)
You may need an appropriate loader to handle this file type, currently no loaders are configured to process this file. See https://webpack.js.org/concepts#loaders
| import StackAlt from './assets/stackalt.svg';
|
> <Meta title="Example/Introduction" />
|
| <style>{`
 @ \.)(?=.)[^/]*?\.stories\.mdx)$ (./stories sync ^\.(?:(?:^|\/|(?:(?:(?!(?:^|\/)\.).)*?)\/)(?!\.)(?=.)[^/]*?\.stories\.mdx)$) ./Introduction.stories.mdx
 @ ./.storybook/generated-stories-entry.js

 .... more skipped lines ...

╭─────────────────────────────────────────────────────╮
│                                                     │
│   Storybook 6.1.0-alpha.26 started                  │
│   11 s for manager and 10 s for preview             │
│                                                     │
│    Local:            http://localhost:6006/         │
│    On your network:  http://...:6006/               │
│                                                     │
╰─────────────────────────────────────────────────────╯

```

All other addons seems to work execpt addon-docs.

### Notes

**sb upgrade failure**

Running `yarn workspace frontend exec yarn dlx sb upgrade --prerelease` generates the following logs

```
➤ YN0000: ┌ Resolution step
➤ YN0061: │ resolve-url@npm:0.2.1 is deprecated: https://github.com/lydell/resolve-url#deprecated
➤ YN0061: │ urix@npm:0.1.0 is deprecated: Please see https://github.com/lydell/urix#deprecated
➤ YN0002: │ sb@npm:6.0.26 doesn't provide jest@* requested by @storybook/cli@npm:6.0.26
➤ YN0000: └ Completed in 9s 553ms
➤ YN0000: ┌ Fetch step
➤ YN0000: └ Completed in 0s 238ms
➤ YN0000: ┌ Link step
➤ YN0007: │ core-js@npm:3.6.5 must be built because it never did before or the last one failed
➤ YN0000: └ Completed in 1s 370ms
➤ YN0000: Done with warnings in 11s 251ms

 • Checking for latest versions of '@storybook/*' packagesinfo ,Upgrading ~/github-issues/monorepo-yarn2-react-typescript-storybook6-issue/packages/frontend/package.json
info
info  @storybook/addon-actions     ^6.0.26  →  ^6.1.0-alpha.26
info  @storybook/addon-docs        ^6.0.26  →  ^6.1.0-alpha.26
info  @storybook/addon-essentials  ^6.0.26  →  ^6.1.0-alpha.26
info  @storybook/addon-links       ^6.0.26  →  ^6.1.0-alpha.26
info  @storybook/react             ^6.0.26  →  ^6.1.0-alpha.26
info
info Run npm install to install new versions.
info
info ,npx: installed 285 in 11.731s
info
info
 • Installing upgrades • Preparing to install dependencies. ✓

.... more skipped lines ...

. ✓
WARN No storybook core packages found.
WARN 'npm ls | grep storybook' can show if multiple versions are installed.
(node:983833) UnhandledPromiseRejectionWarning: TypeError: Cannot read property 'version' of undefined
    at checkVersionConsistency (/tmp/xfs-b7cb47a7/dlx-983646/.yarn/

.... more skipped lines ...

(node:983833) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). To terminate the node process on unhandled promise rejection, use the CLI flag `--unhandled-rejections=strict` (see https://nodejs.org/api/cli.html#cli_unhandled_rejections_mode). (rejection id: 1)
(node:983833) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.
```

I'm not sure why the command runs with npm internally.

The script fails with a TypeError.

**core-js missing dependency**

This solution doesn't resolve the issue with core-js:

```
Module not found: Error: Your application tried to access core-js, but it isn't declared in your dependencies; this makes the require call ambiguous and unsound.
```

## Dependencies

- "@babel/core": "^7.12.3"
- "@mdx-js/react": "^1.6.18"
- "@storybook/addon-actions": "^6.1.0-alpha.26"
- "@storybook/addon-docs": "^6.1.0-alpha.26"
- "@storybook/addon-essentials": "^6.1.0-alpha.26"
- "@storybook/addon-links": "^6.1.0-alpha.26"
- "@storybook/react": "^6.1.0-alpha.26"

- "babel-loader": "^8.1.0"
- "react-is": "^16.13.1"

- "react": "^16.13.1"
- "react-dom": "^16.13.1"

### Aditionnal Dependencies [#11255](https://github.com/storybookjs/storybook/issues/11255)

- "core-js": "^3.6.5"
