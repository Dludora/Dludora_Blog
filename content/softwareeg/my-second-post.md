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

### 1. vue3 适配的 markdown编辑器

​	命令行输入`npm i @kangc/v-md-editor@next -S`安装 `v-md-editor`组件

​	在`main.js`中加入如下代码，即可通过`v-md-editor`模块进行使用`markdown`编辑器

```javascript
// 引入所有语言包
import hljs from 'highlight.js'

import VMdPreview from '@kangc/v-md-editor/lib/preview';
import '@kangc/v-md-editor/lib/style/preview.css';
import VMdEditor from '@kangc/v-md-editor/lib/codemirror-editor';
import '@kangc/v-md-editor/lib/style/codemirror-editor.css';
import githubTheme from '@kangc/v-md-editor/lib/theme/github.js';
import '@kangc/v-md-editor/lib/theme/style/github.css';
// emoji
import createEmojiPlugin from '@kangc/v-md-editor/lib/plugins/emoji/index';
import '@kangc/v-md-editor/lib/plugins/emoji/emoji.css';
// 显示代码行数
import createLineNumbertPlugin from '@kangc/v-md-editor/lib/plugins/line-number/index';
// 快速复制
import createCopyCodePlugin from '@kangc/v-md-editor/lib/plugins/copy-code/index';
import '@kangc/v-md-editor/lib/plugins/copy-code/copy-code.css';

// codemirror 编辑器的相关资源
import Codemirror from 'codemirror';
// mode
import 'codemirror/mode/markdown/markdown';
import 'codemirror/mode/javascript/javascript';
import 'codemirror/mode/css/css';
import 'codemirror/mode/htmlmixed/htmlmixed';
import 'codemirror/mode/vue/vue';
// edit
import 'codemirror/addon/edit/closebrackets';
import 'codemirror/addon/edit/closetag';
import 'codemirror/addon/edit/matchbrackets';
// placeholder
import 'codemirror/addon/display/placeholder';
// active-line
import 'codemirror/addon/selection/active-line';
// scrollbar
import 'codemirror/addon/scroll/simplescrollbars';
import 'codemirror/addon/scroll/simplescrollbars.css';
// style
import 'codemirror/lib/codemirror.css';

VMdEditor.Codemirror = Codemirror;
VMdEditor.use(githubTheme, {
  Hljs: hljs,
});
VMdPreview.use(githubTheme, {
  Hljs: hljs,
});
VMdPreview.use(createEmojiPlugin());
VMdPreview.use(createLineNumbertPlugin());
VMdPreview.use(createCopyCodePlugin());
app.use(VMdEditor);
app.use(VMdPreview);
```

**如果想要添加流程图功能**

在`main.js`中添加

```javascript
// 流程图
import createMermaidPlugin from '@kangc/v-md-editor/lib/plugins/mermaid/cdn';
import '@kangc/v-md-editor/lib/plugins/mermaid/mermaid.css';

VMdPreview.use(createMermaidPlugin());
```

在`index.html`中添加

```javascript
<script src="https://unpkg.com/mermaid/dist/mermaid.min.js"></script>
```

在想要引入的页面中加入

```vue
<v-md-editor
    v-model="xxx"
    height="600px"></v-md-editor>
```

### 2. 渲染markdown文件

#### 需要提前安装的包

`npm install vue-loader vue-template-compiler -D`

`npm install --save vue-markdown`

`npm install github-markdown-css`

`npm install highlight.js`

`npm install markdown-loader`

#### 预览器使用

```javascript
<v-md-preview :text="blogForm.text"></v-md-preview>
```

