# Django实现跨域

## 1-

```python
pip3 install django-cors-headers
```

## 2-

后端 django 根目录  settings.py

```python
INSTALLED_APPS = [
  ...
  'rest_framework',
  'corsheaders',
]

MIDDLEWARE = [
  'django.middleware.security.SecurityMiddleware',
  'django.contrib.sessions.middleware.SessionMiddleware',
  # 跨域设置--开始（注意顺序）
  'corsheaders.middleware.CorsMiddleware',
  # 跨域设置--结束
  'django.middleware.common.CommonMiddleware',
  'django.middleware.csrf.CsrfViewMiddleware',
  'django.contrib.auth.middleware.AuthenticationMiddleware',
  'django.contrib.messages.middleware.MessageMiddleware',
  'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

添加：（放到最下面）
# 跨域设置
CORS_ORIGIN_ALLOW_ALL = True
// 添加白名单
CORS_ORIGIN_WHITELIST = (
	'127.0.0.1:8080',
  'localhost:8080',
  'www.xxxx.com:8080',
  'api.xxxx.com:8080'
)
CORS_ALLOW_CREDENTIALS = True  # 允许携带cookieALLOWED_HOSTS = ['www.xxxx.com:8080', 'api.xxxx.com:8080', '127.0.0.1']
# 前端需要携带cookies访问后端时,需要设置withCredentials: True
// 设置允许访问的方法
CORS_ALLOW_METHODS = (
	'GET'
  'POST'
  'PUT'
  'PATCH'
  'DELETE'
  'OPTIONS'
)
// 设置允许的 HEADER
CORS_ALLOW_HEADERS = (
	'x-requested-with',
  'content-type',
  'accept',
  'origin',
  'authorization',
  'x-csrftoken'
)

# 上传设置
import os  # 默认的Django没有的话需要引入
MEDIA_URL = "/upimg/"  # upimg是第一级目录，名字可自定义，是一个静态地址
MEDIA_ROOT = os.path.join(BASE_DIR, 'upimg')  # 访问方法
```

## 3-

### 前端项目中

```node
npm install axios
npm install vue-axios
```

前端 VUE 根目录  /main.js

#### 引入axios

```vue
import Axios from 'axios'
import VueAxios from 'vue-axios'
```

前端需要数据的页面，引入Axios  设定方法：

```vue
Methods: {
	getData() {
		Axios.get(`数据页面`).then((response) => {
			console.log(response)  # 打印日志
			this.数据名称 = response.data
		})
	}
}
```

#### 获取的数据形式是 JSON

```vue
data() {
	return {
		数据表形式:[]
	}
}
```

#### 序列化数据  v-for

```vue
<div v-for="item in 数据表形式" :key="item.id">
  <div class="box">
    {{item.数据名称}}
  </div>
</div>
```

