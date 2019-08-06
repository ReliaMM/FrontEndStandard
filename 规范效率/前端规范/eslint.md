### ESlint

### VUE ESlint
1. 核心规则  

|规则名|说明|选项|
|:-:|:-:|:-:|
|vue/no-async-in-computed-properties|在计算属性中不允许异步操作|错误|
|vue/no-dupe-keys|不允许重复字段名|错误|
|vue/no-duplicate-attributes|html中不允许重复属性 `<MyComponent :foo="abc" foo="def" /> `|错误|
|vue/no-parsing-error|在“\<template\>”中解析指令的错误|错误|
|vue/no-reserved-keys|不允许覆盖保留的方法，如`$nextTick` `$on` `$emit` `$el`等等，不允许使用`_`或者`$`开头的属性或者方法|错误|
|vue/no-shared-component-data|将组件的data属性强制为函数|错误|
|vue/no-side-effects-in-computed-properties|在计算属性中禁用"副作用"，比如做其他的赋值操作|错误|
|vue/no-template-key|在' \<template\> '上禁用' key '属性|错误|
|vue/no-textarea-mustache|禁止在textarea标签内使用模板插值|错误|
|vue/no-unused-components|不允许注册模板中不使用的组件|错误|
|vue/no-unused-vars|禁止在v-for或者scope中定义未使用的变量|错误|
|vue/no-use-v-if-with-v-for|禁止在使用了v-for指令的元素上使用v-if;如有需要可以用computed先过滤一下遍历元素|错误|
|vue/require-component-is|\<component>标签必须通过v-bind指令绑定is属性|错误|
|vue/require-prop-type-constructor|prop的type必须是类型构造函数|错误|
|vue/require-render-return|render函数始终有返回值|错误|
|vue/require-v-for-key|使用v-for指令的元素需要有key值|错误|
|vue/require-valid-default-prop|prop属性必须有default值|错误|
|vue/return-in-computed-property|computed属性必须有返回值|错误|
|vue/use-v-on-exact|如果一个元素上的两个v-on绑定同类型事件，且其中一个有修饰时，另外一个必须也有修饰|错误|
|vue/valid-template-root|根\<template\>标签内部有且仅有一个非template或slot的非文本的元素|错误|
|vue/valid-v-bind|v-bind指令需要有value值，同时校验修饰符|错误|
|vue/valid-v-cloak|检验v-cloak|错误|
|vue/valid-v-else-if||错误|
|vue/valid-v-else||错误|
|vue/valid-v-for||错误|
|vue/valid-v-html||错误|
|vue/valid-v-if||错误|
|vue/valid-v-model||错误|
|vue/valid-v-on||错误|
|vue/valid-v-once||错误|
|vue/valid-v-pre||错误|
|vue/valid-v-show||错误|
|vue/valid-v-text||错误|

2. 强烈推荐

|规则名|说明|选项|
|:-:|:-:|:-:|
|vue/attribute-hyphenation|在模板中的自定义组件上强制属性命名样式，使用连接符||
|vue/html-closing-bracket-newline|要求或不允许在html标签的右括号前换行||
|vue/html-closing-bracket-spacing|要求或不允许在html标签的右括号前添加一个空格||
|vue/html-end-tags|强制关闭标签||
|vue/html-indent|html标签缩进对齐||
|vue/html-quotes|html标签属性值使用双花括号||