## repro for echarts + vue-echarts with vitesse

these are the changes I made, you can see it here https://github.com/userquin/vitesse-apache-echarts using vitesse template (the changes on the dependencies should be done manually, not included on the repo):
- `package.json`: add `"type": "module"`
- `vite.config.ts`: changed the import for `VueI18n` and included some entries on `optimizedDeps/include` option
- `tsconfig.json`: changed `module` to `ESNext` instead `es2016`
- `src/components/ChartComponent.vue`  using `vue-echarts/dist/index.esm.js` instead `vue-echarts` (maybe we need to also change the `package.json` of `vue-echarts`)
- `pnpm install`: once dependencies installed you must modify the following dependencies (we can also apply something similar to `echarts`...)

**node_modules/echarts**
- `package.json`: add `"type": "module"`, add also `exports` entry before `main` entry, the file should be like this:
```json
{
  "name": "echarts",
  "version": "5.3.0",
  "description": "Apache ECharts is a powerful, interactive charting and data visualization library for browser",
  "license": "Apache-2.0",
  "type": "module",
  "keywords": [
    "echarts",
    "data-visualization",
    "charts",
    "charting-library",
    "visualization",
    "apache",
    "data-viz",
    "canvas",
    "svg"
  ],
  "exports": {
    ".": {
      "require": "./dist/echarts.js",
      "import": "./dist/echarts.esm.js",
      "types": "./index.d.ts"
    },
    "./core": {
      "require": "./core.js",
      "import": "./core.js",
      "types": "./core.d.ts"
    },
    "./renderers": {
      "require": "./renderers.js",
      "import": "./renderers.js",
      "types": "./renderers.d.ts"
    },
    "./charts": {
      "require": "./charts.js",
      "import": "./charts.js",
      "types": "./charts.d.ts"
    },
    "./components": {
      "require": "./components.js",
      "import": "./components.js",
      "types": "./components.d.ts"
    }
  },
  "main": "dist/echarts.js",
 ```

**node_modules/vue-echarts**
- `package.json` add  `"type": "module"`
- `dist/index.esm.js`: replace `import { addListener, removeListener } from 'resize-detector';` with `import { addListener, removeListener } from 'resize-detector/esm/index.js';`

**node_modules/resize-detector**
- `package.json` add  `"type": "module"`

**node_modules/zrender**
- `package.json` add  `"type": "module"`
