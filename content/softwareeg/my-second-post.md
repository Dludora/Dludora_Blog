---
title: "Vue 与 Markdown 交互"
date: 2022-06-02T23:11:47+08:00
lastmod: 2022-06-02T23:11:47+08:00
description: ""
tags: []
categories: []
author: "codecat"
keywords: []
comment: true
toc: true
autoCollapseToc: true
postMetaInFooter: false
hiddenFromHomePage: false
contentCopyright: true
reward: true
mathjax: true
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false
---

## Vue 与 Markdown 交互

### vue3 适配的 markdown编辑器

​	命令行输入`npm i md-editor-v3`安装 `md-editor-v3`组件

​	在想要引入的界面中加入如下代码，即可通过`MdEditor`模块进行使用`markdown`编辑器

```javascript
import MdEditor from 'md-editor-v3';
import 'md-editor-v3/lib/style.css';
export default {
  components: {
  	MdEditor,
  },
}
```

### 渲染markdown文件

#### 需要提前安装的包

`npm install vue-loader vue-template-compiler -D`

`npm install --save vue-markdown`

`npm install github-markdown-css`

`npm install highlight.js`

#### 组件引入

在需要的地方引入刚才安装的组件

```javascript
import VueMarkdown from 'vue-markdown'
export default {
  components: {
    VueMarkdown // 注入组件
  },
  data () {
    return { 
      value: MarkdownData // value的值是要解析的markdown数据
    },
  }
}
```

在`main.js`文件中引入css文件

```javascript
import 'github-markdown-css/github-markdown.css'
import hljs from 'highlight.js'
// 如果开启了typescript 需要额外安装 npm install @types/highlight.js
// 通过 import * as hljs from 'highlight.js' 引入
app.directive('highlight', function (el) {
  const blocks = el.querySelectorAll('pre code')
  blocks.forEach(block => {
    hljs.highlightBlock(block)
  })
})
```

#### 组件使用

```vue
<div class="markdown-body">
    <VueMarkdown :source="value"></VueMarkdown>
</div>
```

