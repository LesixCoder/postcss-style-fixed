# postcss-style-fixes

[![NPM version](https://img.shields.io/npm/v/postcss-style-fixes?color=a1b858&label=)](https://www.npmjs.com/package/postcss-style-fixes) [![Download monthly](https://img.shields.io/npm/dm/postcss-style-fixes.svg)](https://www.npmjs.com/package/postcss-style-fixes)

PostCSS plugin tries to fix all issues about [antd](https://www.npmjs.com/package/antd) with any others global CSS reset

## Features

- support antd + [TailwindCSS preflight.css](https://github.com/tailwindlabs/tailwindcss/blob/master/src/css/preflight.css)
  - fix button style conflict, ref: [ant-design/ant-design#38794](https://github.com/ant-design/ant-design/issues/38794)
  - support anchor tags with `colorPrimary` under any antd components

## Usage

```bash
npm install postcss-style-fixes --save-dev
```

```js
// postcss.config.js
module.exports = {
  plugins: {
    'tailwindcss': {},
    'autoprefixer': {},
    'postcss-style-fixes': {
      // Support multiple prefixes, if you do not custom antd class name prefix, it's not necessary option.
      prefixes: ['ant'],
    },
  },
}
```

## Transforms

### Transform `button` styles

```css
button,
[type='button'],
[type='reset'],
[type='submit'] {
  -webkit-appearance: button; /* 1 */
  background-color: transparent; /* 2 */
  background-image: none; /* 2 */
}

/* => */

button:where(:not([class*='ant'])),
[type='button']:where(:not([class*='ant'])),
[type='reset']:where(:not([class*='ant'])),
[type='submit']:where(:not([class*='ant'])) {
  -webkit-appearance: button; /* 1 */
  background-color: transparent; /* 2 */
  background-image: none; /* 2 */
}
```

### Add `anchor` styles

```css
:where([class*='ant']) a {
  /* colorPrimary */
  color: #1677ff;
  text-decoration: none;
}
```

## Build & Publish

- `npm run build`
- `npx changeset`
- `npx changeset version`
- `git commit`
- `npx changeset publish`
- `git push --follow-tags`

> [`changeset` prerelease doc](https://github.com/changesets/changesets/blob/main/docs/prereleases.md)

## License

[MIT](./LICENSE) License © 2023 [Yuns](https://github.com/LesixCoder)
