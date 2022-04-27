# VUE自定义指令

### 1、自定义v-big

作用：点击n值放大10倍

```vue
<template>
	<h2>当前的n值是：<span v-text="n"></span></h2>
	<h2>放大10倍的n值是：<span v-big="n"></span></h2>
	<botton @click="n++">点我n+1</botton>
</template>
<script>
	new Vue({
		data() {
			n: 1
		},
		directives: {
			big(element,binding) {
        element.innerText = binding.value * 10
			}
    }
  })
</script>
```

自定义指令在与元素成功绑定时或所在模版被重新解析时调用。

### 2、自定义v-fbind

作用：

```vue
<template>
	<input type="text" v-fbind:value="n">
</template>
<script>
	new Vue({
		data() {
			n: 1
		},
		directives: {
			fbind: {
        //指令与元素成功绑定
        bind(element, value) {
          element.value = binding.value
        },
        //指令所在元素被插入页面时
        inserted(element, value) {
          element.focus()
        },
    		//指令所在的模版被重新解析时
    		update(element, value) {
          element.value = binding.value
        },
			}
		}
	})
</script>
```

原生js实现获取input焦点

```html
<html>
  <head>
    <style>
      .demo {
        
      }
    </style>
  </head>
  <body>
  	<button id="btn">点我创建一个输入框</button>
		<script>
			const btn = document.getElementById('btn')
			btn.onclick() = ()=>{
			const input = document.createElement('input')
				input.className = 'demo'  //增加样式
        input.value = '99'  //设置初始值
        input.onclik = ()=>{alert(1)}  //弹窗
				document.body.appendChild(input) //appendChild指定元素节点的最后一个子节点之后添加节点
        input.parentElement.style.backgroundColor = ''  //设置父级元素的背景色
				input.focus()
			}
		</script>
	</body>
</html>
```

### 3、注意

在使用自定义事件的同时使用原生事件，需要在原生事件后加".native"。
