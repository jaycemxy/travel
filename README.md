# travel

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

## 兄弟组件通信（City.vue作为eventBus，在Alphabet和List组件间传值）
1. 在Alphabet中给循环项绑定一个click事件"handleLetterClick"
2. 在methods中定义这个事件，得到e.target.innerText为点击元素（A、B、C、D... ...）
3. 将Alphabet中得到的数据传递给City，再通过City传递给List
4. 在Alphabet的handleLetterClick方法中，调用this.$emit('change',e.target.innerText)向外触发事件，第一个参数为事件名，第二个参数为事件携带的内容（即点击的当前元素A、B、C、D... ...）
5. 在City组件中监听这个事件，@change="handleLetterChange"，在methods中定义这个方法，这一步可理解为父组件接收到子组件Alphabet传来的数据
6. City向下再以属性的形式传递给另一个兄弟组件List。在data中定义一个letter值为空，在handleLetterChange中令this.letter = letter，即接受传来的数据，然后再传递给city-list，在这个组件中绑定:letter="letter"
7. 父组件City传递过来数据，子组件List就要接收这个数据，在props中定义一个letter: String 即接受传来的数据的类型为字符串，调用watch监听器的属性监听letter的变化，如果不为空，那么有this.scroll.scrollToElement
8. 给每一个class="area"的区域加一个 :ref="key" ，再在letter中定义常量 const element = this.$refs[this.letter]，这样就可以通过this.$refs获取这个字母对应的 class=area 区域，但这里有一个小bug，因为ref是通过循环得到的，它是一个数组，当我们必须让 element 是一个dom元素或选择器，使用 const element = this.$refs[this.letter][0] 来取得对应元素而非一个数组，再将 this.scrollToElement(element)传入element

## 解绑全局事件
在制作查看详情页的下滑header逐渐显示，上滑逐渐消失时，采用了 window.addEventListener('scroll', this.handleScroll) 它绑定了一个全局的window对象，使得它不仅仅作用在header组件中，还对其他组件有影响。

解决方法：在我们使用了 keep-alive 这个标签时，它不仅向我们提供了 activated 这个函数，他在页面展示的时候会执行，与之相对应的还提供了 deactivated 这个生命周期函数，它在页面被转换成新的页面时会被执行
```
deactivated () {
  window.removeEventListener('scroll', this.handleScroll)
}
```