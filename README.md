## vite-preprocess

### Introduction

`vite-preprocess-loader`支持vue项目中使用条件编译功能.

条件编译支持：
```
@ifdef 变量名
  code...
@endif
```
```
@ifndef 变量名
  code...
@endif
```

### Example
```
<script setup lang="ts">
// @ifdef web
console.log('hello world!')
// @endif
</script>
<template>
    <div class="wrapper">
      <!-- @ifdef web -->
      <h1>web</h1>
      <!-- @endif -->
      <!-- @ifndef web -->
      <h1>not web</h1>
      <!-- @endif -->
    </div>
</template>

<style scoped>
.wrapper {
  line-height: 1.5;
  max-height: 100vh;
  /* @ifdef web */
  color: red;
  /* @endif */
  /* @ifdef h5 */
  font-size: 100px;
  font-weight: bold;
  /* @endif */
}
</style>
```

### Install

```
npm install vite-preprocess
```

### Usage

需要在项目运行的时候添加临时node的环境变量`platform`

```
vite.config.ts
import vitePreprocess from 'vite-preprocess'

export default defineConfig({
  plugins: [vitePreprocess(), vue()],
  // esbuild: false, // esbuild默认过滤注释内容
  esbuild: {
    legalComments: 'none', // * 一定要设置'legalComments: none'或者 'esbuild: false' ,不用esbuild处理注释内容.
  }
})
```

```
package.json
"scripts": {
    "serve": "cross-env platform=h5 vite"
}
```
### All directives
```
@ifdef 变量 /@endif 包括定义其中的代码块
@ifndef 变量 /@endif 不包括其中定义的代码块
```

