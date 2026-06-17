# bbang-react-editor

<p align="center">
  <strong>可配置的 React 块级文档编辑器</strong><br/>
  像写 Markdown 一样快，像用 Notion 一样自由。
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/bbang-react-editor">
    <img src="https://img.shields.io/npm/v/bbang-react-editor?style=flat-square" alt="npm version"/>
  </a>
  <a href="https://www.npmjs.com/package/bbang-react-editor">
    <img src="https://img.shields.io/npm/dm/bbang-react-editor?style=flat-square" alt="npm downloads"/>
  </a>
  <a href="https://github.com/JiuYoStar/editor-demo">
    <img src="https://img.shields.io/github/stars/JiuYoStar/editor-demo?style=flat-square" alt="GitHub stars"/>
  </a>
</p>

---

## 简介

**bbang-react-editor**（BbangEditor）是一款为 React 应用设计的可配置块级文档编辑器。它把 Markdown 的轻量输入体验与 Notion 式的块级编辑体验结合在一起，让你既能用 `#`、`-`、`[]` 等快捷语法快速写作，也能通过拖拽、命令菜单、工具栏直观组织内容。

> npm 定位：*configurable React block editor with Markdown import/export*

它适合用于：

- 技术文档、产品文档、项目说明书的结构化编辑
- Markdown 写作与可视化块编辑结合的场景
- 需要表格、代码块、日历、目录大纲等复杂内容块的文档工具
- 对长文档性能、撤销/重做一致性、跨平台渲染稳定性要求较高的编辑器项目

---

## 效果预览

### 基础块与 Markdown 快捷输入

支持标题 1-6 级、段落、无序/有序列表、待办事项、引用、分割线、图片、行内格式等，全部可用 Markdown 语法触发。

![基础块编辑预览](./demo1.png)

### 表格与日历块

内置专业表格块（行列操作、合并单元格、列宽调整、虚拟化）和日历块（事件创建、拖拽、分组、节假日），满足项目排期与数据展示需求。

![表格与日历块预览](./demo2.png)

---

## 核心特性

### 🧱 块级编辑体验

以“块”为基本编辑单元，支持段落、标题、列表、引用、分割线、待办事项、折叠块、提示块、代码块、表格块、日历块等。可以像写 Markdown 一样快速输入，也可以像使用 Notion 一样组织页面结构。

### ⚡ 高性能长文档

采用块树模型、事务化操作、增量渲染和虚拟滚动方案，减少不必要的 DOM 更新。面对较长文档时，编辑器只渲染当前可见区域，保持打开、输入和滚动的流畅性。

### 🛠 稳定的编辑内核

不依赖浏览器原生 `contenteditable`，完全自研数据模型、渲染引擎和输入接管机制。所有编辑行为都被转换为明确的 Operation 和 Transaction，保证撤销/重做、格式化、块移动、删除等行为清晰可控。

### 📥 Markdown 导入 / 导出

支持从 Markdown 快速导入内容，也支持将文档结构导出为 Markdown，方便与现有文档工作流集成。

### 🎯 丰富的块类型

- **基础块**：Paragraph、Heading 1-6、Bullet List、Number List、Todo List、Quote、Divider、Callout、Toggle
- **专业块**：Code（基于 CodeMirror 6）、Table（支持合并单元格与虚拟化）、Calendar（事件与分组）
- **行内格式**：加粗、斜体、下划线、删除线、行内代码、文本颜色、链接、`@mention`

### 🖱 直观的交互方式

- Markdown 快捷输入：`#`、`-`、`1.`、`[]`、`>`、`---` 等
- Slash Command 命令菜单：输入 `/` 快速插入块
- 块拖拽手柄：跨层级拖拽排序
- 浮动选区工具栏：选中文字即可加粗、斜体、改色
- 右侧目录大纲：点击跳转，当前段落高亮

---

## 安装

```bash
npm install bbang-react-editor
# 或
yarn add bbang-react-editor
# 或
pnpm add bbang-react-editor
```

### 依赖

bbang-react-editor 的 peerDependencies 要求：

```json
{
  "react": "^18.0.0 || ^19.0.0",
  "react-dom": "^18.0.0 || ^19.0.0"
}
```

---

## 快速开始

```tsx
import React, { useRef } from 'react';
import { Editor } from 'bbang-react-editor';
import 'bbang-react-editor/style.css';

function App() {
  const editorRef = useRef(null);

  const handleSave = () => {
    const document = editorRef.current?.getDocument();
    console.log('保存文档', document);
  };

  return (
    <Editor
      ref={editorRef}
      defaultValue="# 欢迎使用 bbang-react-editor\n\n开始你的块级写作吧。"
      placeholder="输入 / 查看命令，输入 Markdown 快捷语法开始写作..."
      onSave={handleSave}
    />
  );
}

export default App;
```

### 获取文档数据

通过 `forwardRef` 暴露的 `getDocument` 方法读取当前文档：

```tsx
const document = editorRef.current?.getDocument();
```

### 导入 Markdown

```tsx
<Editor
  ref={editorRef}
  defaultValue={markdownString}
/>
```

---

## 已支持能力

### 基础编辑

- [x] 文字输入与 IME 中文输入法
- [x] 删除、光标移动、选区移动
- [x] 复制、剪切、粘贴
- [x] Markdown 粘贴解析
- [x] 富文本粘贴（保留 Notion、Word、网页格式）
- [x] 撤销 / 重做（含快捷键）
- [x] Cmd/Ctrl + S 保存、Cmd/Ctrl + A 逐级全选
- [x] 查找替换
- [x] 浮动 Selection Toolbar
- [x] 加粗、斜体、下划线、删除线、行内代码、文本颜色

### 块类型

- [x] Paragraph、Heading 1-6
- [x] Bullet List、Number List、Todo List
- [x] Quote、Divider、Callout、Toggle
- [x] Code（CodeMirror 6 语法高亮）
- [x] Table（行列操作、合并拆分单元格、列宽调整、Tab 导航、虚拟化）
- [x] Calendar（月视图、事件增删改、拖拽创建、分组筛选、节假日）
- [x] `@mention` 渲染

### Markdown 快捷输入

- [x] `#` ~ `######` 转标题
- [x] `-` / `*` 转无序列表
- [x] `1.` 转有序列表
- [x] `[]` / `[x]` 转 Todo 列表
- [x] `>` 转引用，`---` 转分割线，`>>>` 转折叠标题
- [x] 代码块、行内粗体/斜体/删除线/代码/链接解析

### 块级交互

- [x] Enter 智能分裂块、Backspace/Delete 智能合并块
- [x] 列表缩进/反缩进、嵌套列表深度合并
- [x] Slash Command 命令菜单与键盘导航
- [x] 块拖拽手柄与跨层级拖拽排序
- [x] 右侧目录大纲、点击跳转与当前段落高亮

### 性能与体验

- [x] Piece Table 文本存储
- [x] BlockTree 块树模型
- [x] Transaction 历史栈
- [x] 增量渲染与虚拟滚动
- [x] 自定义光标与选区渲染
- [x] 大文档性能测试与 IME 滚动优化

---

## 技术架构

采用清晰的分层架构：

```
kernel ← engine ← editor ← app
```

- **Kernel**：数据模型、Piece Table、BlockTree、Transaction
- **Engine**：渲染、输入处理、光标管理、选区系统
- **Editor**：React 组件封装、命令分发、UI 层
- **App**：具体应用场景（桌面端、Web 应用等）

---

## 桌面端应用

BbangEditor 同时提供基于 Electron 的桌面客户端，支持本地文件保存、拖拽文件导入和工具栏图标化。

- GitHub 仓库：[JiuYoStar/editor-demo](https://github.com/JiuYoStar/editor-demo)
- 问题反馈：[Issues](https://github.com/JiuYoStar/editor-demo/issues)

> macOS 首次打开未签名应用时，可能需要在“系统设置 → 隐私与安全性”中手动允许打开。

---

## 许可证

[SEE LICENSE IN LICENSE](./LICENSE)

---

<p align="center">
  由 <a href="https://github.com/JiuYoStar">JiuYoStar</a> 构建 · 欢迎 Star 与 PR
</p>
