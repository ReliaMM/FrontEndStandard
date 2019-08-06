优先级 A：必要的
### 目录
- 组件名应该始终是多个单词的，根组件 App 除外。
- Prop 定义应该尽量详细
- 总是用 key 配合 v-for
- 避免 v-if 和 v-for 用在一起
- 私有属性名

### 组件名应该始终是多个单词的，根组件 App 除外。

```js
//反例
Vue.component('todo', {
  // ...
})
export default {
  name: 'Todo',
  // ...
}
```

```js
//好例子
Vue.component('todo-item', {
  // ...
})
export default {
  name: 'TodoItem',
  // ...
}
```

### Prop 定义应该尽量详细
```js
// 发例
// 这样做只有开发原型系统时可以接受
props: ['status']
```
```js
// 好例子
props: {
  status: String
}
// 更好的做法！
props: {
  status: {
    type: String,
    required: true,
    validator: function (value) {
      return [
        'syncing',
        'synced',
        'version-conflict',
        'error'
      ].indexOf(value) !== -1
    }
  }
}
```

### 总是用 key 配合 v-for
>在组件上总是必须用 key 配合 v-for，以便维护内部组件及其子树的状态。甚至在元素上维护可预测的行为，比如动画中的对象固化 (object constancy)，也是一种好的做法。

### 避免 v-if 和 v-for 用在一起
>永远不要把 v-if 和 v-for 同时用在同一个元素上。

### 私有属性名
>在插件、混入等扩展中始终为自定义的私有属性使用 $_ 前缀。并附带一个命名空间以回避和其它作者的冲突 (比如 $_yourPluginName_)。
```js
// 好例子
var myGreatMixin = {
  // ...
  methods: {
    $_myGreatMixin_update: function () {
      // ...
    }
  }
}
```