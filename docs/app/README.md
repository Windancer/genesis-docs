---
sidebar: auto
---
# genesis-app
它提供了快速创建APP的方法，以及包装了 `vue-router`，它帮你解决了在历史模式下，多个 `Router` 实例冲突的问题

## 安装
```bash
npm install vue-router @fmfe/genesis-app
```

## 使用
### 路由配置
```ts
// import VueRouter from 'vue-router';
import { Router } from '@fmfe/genesis-app';
const router = new Router({
    mode: 'history'
});
```
只需要将 [VueRouter](https://github.com/vuejs/vue-router) 修改成 `@fmfe/genesis-app` 的 Router 即可，其它的还是和 [VueRouter](https://github.com/vuejs/vue-router) 的使用方式一样
### 客户端使用
```ts
// entry-client.ts
import { ClientOptions } from '@fmfe/genesis-core';
import { createClientApp } from '@fmfe/genesis-app';
import Vue from 'vue';
import App from './app.vue';

export default async (clientOptions: ClientOptions): Promise<Vue> => {
    return createClientApp({
        App,
        clientOptions,
        vueOptions: {
            // 传递给 new Vue({}) 的选项
            // 默认将 renderContext 传递给 new Vue({ clientOptions })
        }
    });
};

```
### 服务端
```ts
// entry-server.ts
import { RenderContext } from '@fmfe/genesis-core';
import { createServerApp } from '@fmfe/genesis-app';
import Vue from 'vue';
import App from './app.vue';

export default async (renderContext: RenderContext): Promise<Vue> => {
    return createServerApp({
        App,
        renderContext,
        vueOptions: {
            // 传递给 new Vue({}) 的选项
            // 默认将 renderContext 传递给 new Vue({ renderContext })
        }
    });
};

```