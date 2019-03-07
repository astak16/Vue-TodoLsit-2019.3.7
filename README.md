什么是 Vue ？

Vue 是尤雨溪的项目，是一套构建用户界面的渐进式框架，与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。Vue 的核心库只关注视图层，它不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与单文件组件和 Vue 生态系统支持的库结合使用时，Vue 也完全能够为复杂的单页面程序提供驱动

```
<template>
  <div>
    <input type="text" v-model.trim="msg" @keyup.enter="push">
    <ul>
      <li v-for="(item, index) in list" @click="deleteItem(index)">
        {{index}}{{item.name}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      msg: "",
      list: []
    }
  },
  methods: {
    push () {
      this.list.push({name: this.msg})
      this.msg = ""
    },
    deleteItem (index) {
      this.list.splice(index, 1)
    }
  }
}
</script>
```
一个 `todo-list`应用集成两个事件，两条`data`数据就完成了！
通过`Template`里的`Html`模版能清楚的观察到绑定信息，数据联动和时时改动：
* `v-model`里面的`msg`和实例`data`里存放的数据进行了绑定
* `@keyup.enter="push"`对键盘事件`keyup`进行监听，同时用`enter`修饰符进行`enter`键进行监听，dang'chu'发`methods`里的`push`函数，向整个`list`列表里添加一条`object`数据
* 通过`v-for`指令循环除整个`list`里的数据，循环除相对应的节点数
* 点击每个节点的时候执行`deleteItem`事件，删除对应的节点

**对于往时操作`dom`写法和当前的数据驱动有很区别？**

* 数据渲染
	* 我们会通过第三方的模版引擎，比如`artTemplate`、`Jade`等，渲染完毕之后在`append`到根元素中。
	* Vue 只是通过一个`v-for`指令循环所有对应节点，先前只要在`html`中写好循环模版。
* 执行事件
	* 需要获取`dom`元素，对`dom`元素`addEventListener`事件，在执行函数
	* Vue 直接通过你的`Template`集成的模版在需要发生事件的元素上直接绑定事件，只要执行一个`v-on`结合你需要需要绑定的事件，所有原生的事件都支持
* 需要存储数据时
	* 我们需要定义一堆变量，有局部变量和全局变量，导致后续的变量难以维护，甚至可能会导致变量名冲突，作用域调用错误，无法准确定位到正确的数据源
	* Vue 通过`data`选项，用每个属性去保存渲染的数据和临时过渡的数据，用统一的`data`选项去保存，让使用者一目了然
* 所有执行的函数
	* 无论是事件所需执行的，还是封装所需要调用的函数，通过函数式声明在`script`标签内写入，代码量大了，也会存在变量名冲突和无法准确的定位方法。
	* Vue 通过`Methods`选项专门为事件所执行的函数和所封装需要调用的函数，就像垃圾桶一样，有一个准确的、可投放的位置，需要找到执行和所需调用的函数，直接可以准确定位到`Methods`选项。
* 平时我们要对有些数据进行一些处理
	* 比如：去除两边的空格，按键的定位，都要通过`js`去过滤或者判断
	* Vue 提供大量的修饰符封装了这些过滤和判断，让开发者少写代码，把时间都投入业务、逻辑上，只需要通过一个`.`修饰符去调用。
