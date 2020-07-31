### mustache语法

{{}} 里面也可以写表达式

### v-once

下面更改时候 上面不动态显示

### v-html

可以放标签 显示成html格式

### v-text

相当于mustache语法 但是不解析url

### v-pre

原封不动的显示不解析

<h2 v-pre>{{message}}</> 不解析message 直接显示{{message}}

### v-bind 语法糖  ：

给单属性赋值

<img v-bind:src="imgurl" />

给对象赋值

：class=“{}” 跟一个大括号代表是对象

：class=“{类名1： bollean，类型二： Boolean}” 跟一个大括号代表是对象

：class=“{active：true，unactive：false}”

给数组赋值

：class=“['active':boolean]”

### 安装脚手架3

npm install -g @vue/cli  &&&   yarn global add @vue/cli



cnpm i @vue/cli -g

| 2.x  | `vue init <template-name> <project-name>` |
| ---- | ----------------------------------------- |
| 3.x  | `vue create <project-name>`               |