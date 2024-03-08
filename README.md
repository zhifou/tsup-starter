# tsup-starter
## 发布的package.json配置
### 导出多种格式，cjs、esm、iife的配置
- cjs是commonjs的缩写，支持使用require导入模块
- esm是es6模块的缩写，支持使用import导入模块
- iife是立即执行函数，支持使用script标签导入模块
- 打包后的文件名格式为：index.cjs、index.mjs、index.global.js，另外types必须加上，否则无法使用，会出现这个问题 “Module not found: Error: Default condition should be last one”
``` package.json
{
    "type": "module",
    "main": "./dist/index.js",
    "module": "./dist/index.js",
    "exports": {
      "require": "./dist/index.cjs",
      "import": "./dist/index.js",
      "default": "./dist/index.cjs",
      "node": "./dist/index.cjs"
      "types": "./dist/index.d.ts",
    }
}
```

``` tsup.config.ts
import type { Options } from "tsup";

const config: Options = {
    entry: ["src/index.ts"],
    dts: true,
    sourcemap: true,
    format: ["iife", "cjs", "esm"],
};

export default config;
```

### 仅导出esm模块的配置
``` package.json
{
    "type": "module",
    "main": "./dist/index.js",
    "module": "./dist/index.js",
    "exports": {
      "types": "./dist/index.d.ts",
      "import": "./dist/index.js"
    }
}
```

``` tsup.config.ts
import type { Options } from "tsup";

const config: Options = {
    entry: ["src/index.ts"],
    dts: true,
    sourcemap: true,
    format: ["esm"],
};

export default config;
```