# 评论组件

CommentList.vue 是评论组件的，使用时只需要使用这个组件。
CommentInput.vue 是评论组件中的输入组件。

应用方式：
App.vue
```
<template>
  <div id="app">
    <div class="doc_item">
      <p>标题</p>
      <p>段落2</p>
    </div>
    <v-comment-items></v-comment-items>
  </div>
</template>

<script>
  import CommentItems from './mycomponents/CommentList.vue'
  export default {
    components: {
      'v-comment-items':CommentItems
    }
  }
</script>


```

## 其他

其他功能待完善
```
1、图标字体没有使用
2、用户头像显示没有解决
3、当前数据存储使用的页面数据，数据存储还未解决

```

## changelog

1. 完成评论组件的基本操作   2019-5-11
