# Storybook6 building with Errors with Yarn 2 monorepo + React + Typescript

### FIX: [workarround] Enable pnp loose mode

```sh
# .yarnrc.yml

pnpMode: loose
```

Enabling `pnpMode: loose` to [yarn config file](https://yarnpkg.com/features/pnp#pnp-loose-mode) resolves the issue but this solution comes with its share of [caveats](https://yarnpkg.com/features/pnp#caveat).

### Note

This doesn't resolve the issue with core-js:

```
Module not found: Error: Your application tried to access core-js, but it isn't declared in your dependencies; this makes the require call ambiguous and unsound.
```

## Dependencies

- "@babel/core": "^7.12.3"
- "@mdx-js/react": "^1.6.18"
- "@storybook/addon-actions": "^6.0.26"
- "@storybook/addon-docs": "^6.0.26"
- "@storybook/addon-essentials": "^6.0.26"
- "@storybook/addon-links": "^6.0.26"
- "@storybook/react": "^6.0.26"

- "babel-loader": "^8.1.0"
- "react-is": "^16.13.1"

- "react": "^16.13.1"
- "react-dom": "^16.13.1"

### Aditionnal Dependencies [#11255](https://github.com/storybookjs/storybook/issues/11255)

- "core-js": "^3.6.5"
