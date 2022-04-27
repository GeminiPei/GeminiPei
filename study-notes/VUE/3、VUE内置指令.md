# VUE内置指令

### 1、v-text

作用：替换标签中的所有内容，不支持结构解析。

```vue
<template>
	<div v-text="msg">
	</div>
</template>
<script>
	new Vue({
    data() {
      msg: '<h3>你好</h3>'
    }
  })
</script>
```

### 2、v-html

作用：支持结构解析，但有安全性问题。

```vue
<template>
	<div v-html="msg">
  </div>
</template>
<script>
	new Vue({
    data() {
      msg: '<h3>你好</h3>'
    }
  })
</script>
```

### 3、v-cloak

作用：特殊属性，VUE实例创建完毕后会删掉此属性，配合CSS可以解决网速慢时页面展示网页结构的问题。

```vue
<template>
	<div v-cloak>
  </div>
</template>
<script>
	new Vue({
    data() {
      msg: '<h3>你好</h3>'
    }
  })
</script>
<style>
  [v-cloak] {
    display: none;
  }
</style>
```

### 4、v-once

作用：在初次动态渲染完成后就视为静态内容。之后的数据改变不会引起v-once所在结构的更新，可以用于优化性能。

```vue
<template>
	<div>
  	<h2 v-once>初始化的n值是：{{n}}</h2>
		<h2>当前的n值是：{{n}}</h2>
		<button @click="n++">点我n+1</button>
  </div>
</template>
<script>
	new Vue({
    data() {
      n: 1
    }
  })
</script>
```

### 5、v-pre

作用：跳过所在节点的编译过程，可以加快编译。

```vue
<template>
	<div>
		<h2>这是一个文字</h2>
		<h2>当前的n值是：{{n}}</h2>
		<button @click="n++">点我n+1</button>
  </div>
</template>
<script>
	new Vue({
    data() {
      n: 1
    }
  })
</script>
```
