# Axios组件封装

### 1、创建一个（Utils）文件夹

文件夹中创建一个（request）.js文件

```js
import axios from "axios";

const request = axios.create({
  baseURL: 'http://127.0.0.1:8000',
  timeout: 5000,  //超时时间
})

export default request
```

### 2、创建接口文件（文件夹<api>可自定义）

创建产品接口文件<products.js>可自定义

```js
import request from '../utils/request'

export function getProducts(params) {
  return request({
    method: 'GET',
    url: '/products',
    params,
  })
}

export function getProduct(id) {
  return request({
    method: 'GET',
    url: `/products/${id}`,
  })
}

export function updateProduct(id, data) {
  return request({
    methed: 'PUT',
  	url: `/products/${id}`,
    data,
  })
}
```

文件夹中创建index.js

```js
import products from './products'
//导入下方前缀接口文件
import prefixes from './prefixes'

export default {
  products,
  prefixes,
}
```

文件夹中创建前缀接口<prefixes.js>

```js
import request from '../utils/request'

export function getPrefixes(params = {}) {
  return request({
    method: 'GET',
    url: '/prefixes',
    params,
  })
}
//在index.js中导入
```

### 3、VUE中引用

main.js中导入

```js
import api from './api'

Vue.prototype.$api = api
```

组件中引用

```vue
<script>
  getProducts() {
    this.$api.products.get(this.query/* 查询参数 */).then((response) => {
      
    })
  }
</script>
```

