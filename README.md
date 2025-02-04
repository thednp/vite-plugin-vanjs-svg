# vite-plugin-vanjs-svg

[![Coverage Status](https://coveralls.io/repos/github/thednp/vite-plugin-vanjs-svg/badge.svg)](https://coveralls.io/github/thednp/vite-plugin-vanjs-svg)
[![ci](https://github.com/thednp/vite-plugin-vanjs-svg/actions/workflows/ci.yml/badge.svg)](https://github.com/thednp/vite-plugin-vanjs-svg/actions/workflows/ci.yml)
[![NPM Version](https://img.shields.io/npm/v/vite-plugin-vanjs-svg.svg)](https://www.npmjs.com/package/vite-plugin-vanjs-svg)
[![typescript version](https://img.shields.io/badge/typescript-5.6.2-brightgreen)](https://www.typescriptlang.org/)
[![vanjs-core version](https://img.shields.io/badge/vanjs--core-1.5.3-brightgreen)](https://github.com/vanjs-org/van)
[![vitest version](https://img.shields.io/badge/vitest-3.0.4-brightgreen)](https://www.vitest.dev/)
[![vite version](https://img.shields.io/badge/vite-6.0.11-brightgreen)](https://vite.dev)


A Vite plugin that transforms SVG files into VanJS components using the [DOMParser](https://github.com/thednp/domparser) and [vite-plugin-vanjs](https://github.com/thednp/vite-plugin-vanjs).

**Note:** The plugin will also resolve SVG files from the `/public` folder or any valid `viteConfig.publicDir` option.


## Features
* 🚀 Fast transformation using [DOMParser](https://github.com/thednp/domparser)
* 🎯 TypeScript support
* 🔧 Configurable transformation options
* 💪 Full props support (className, style, events, etc.)
* 🔥 Hot Module Replacement (HMR) support
* ⚡ Vitest powered tests


## Installation

```bash
npm install -D vite-plugin-vanjs-svg
```

```bash
pnpm add -D vite-plugin-vanjs-svg
```

```bash
yarn add -D vite-plugin-vanjs-svg
```

```bash
deno add npm:vite-plugin-vanjs-svg
```

```bash
bun install vite-plugin-vanjs-svg
```


## Usage
### Configuration
```ts
// vite.config.ts
import { defineConfig } from 'vite'
import vanSVG from 'vite-plugin-vanjs-svg'

export default defineConfig({
  plugins: [
    // other plugins
    vanSVG({
        // optional
    })
  ]
})
```

### Options
While the default options work just fine, for your convenience the plugin allows you to set them all:

```ts
interface VitePluginVanSvgOptions {
  // vanjs-converter options
  converterOptions?: ParserOptions;
  // esbuild transform options
  esbuildOptions?: EsbuildTransformOPtions;
  // filter options
  include?: string | RegExp | (string | RegExp)[]
  exclude?: string | RegExp | (string | RegExp)[]
}
```

* `converterOptions`: [ParserOptions](https://github.com/thednp/domparser?tab=readme-ov-file#options) allows you to configure sanitization options;
* `esbuildOptions`: [EsbuildTransformOptions](https://esbuild.github.io/api/#transform) esbuild will make sure the plugin will work seamless within the Vite ecosystem and provides some additional options;
  // filter options
* `include`: filter option to **include** one or more RegExp for file IDs; the default value is `["**/*.svg?van"]`;
* `exclude`: filter option to **exclude** one or more RegExp for file IDs.

**Note** - If you modify or add more include filters and you're using Typescript, you should also define new global modules.


### Typescript
To add typescript support, edit your `src/vite-env.d.ts` (or any global types you have set in your app) as follows:

```ts
/// <reference types="vite/client" />
/// <reference types="vite-plugin-vanjs-svg" />
```


### In Your Code
```ts
import Icon from './icon.svg?van'

const app = () => {
  return div(
    Icon({ 
      width: 24,
      height: 24,
      class: 'my-icon',
      style: 'fill: "currentColor"'
    })
  )
}
```
**Notes**:
 - style attribute only supports string value;
 - `fill`, `fillOpacity`, `stroke`, `strokeWidth`, `strokeOpacity`, `transform`, `width`, `height`, `class` and `style` attributes are fully reactive.


## Contributing
* Fork it!
* Create your feature branch: `git checkout -b my-new-feature`
* Commit your changes: `git commit -am 'Add some feature'`
* Push to the branch: `git push origin 'my-new-feature'`
* Submit a pull request


## Acknowledgments
* [vanjs-converter](https://github.com/vanjs-org/converter) - For the excellent SVG to VanJS conversion, it's faster than SVGO;
* [JSON5](https://json5.org/) - For conversion of the SVG attributes to the object we use to set component attributes;
* [vite-plugin-svgr](https://github.com/pd4d10/vite-plugin-svgr) - For inspiration on the plugin architecture.


## License
**vite-plugin-vanjs-svg** is released under [MIT License](LICENSE).
