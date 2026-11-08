# BbangEditor

面向 React 18 / 19 的 Markdown 编辑器。已内置签名授权，安装后即可使用块文档编辑器，也可开启适合 AI Chat 的多段落消息输入框。

```sh
npm install bbang-react-editor
```

## AI Chat 输入框

设置 `config.isTextAreaMode: true` 即可启用。普通 Enter 交给宿主发送消息，Shift + Enter 在光标处新建段落或下一列表项。在空列表项中再按一次即可退出列表。

```tsx
import { useRef } from 'react';
import { BbangEditor, type BbangEditorHandle } from 'bbang-react-editor';
import 'bbang-react-editor/style.css';

const config = {
  isTextAreaMode: true,
  editor: { padding: '12px' },
  placeholder: { blockPlaceholders: { paragraph: '输入消息…' } },
};

export function ChatInput({ onSend }: { onSend: (markdown: string) => void }) {
  const editor = useRef<BbangEditorHandle>(null);

  return (
    <div onKeyDown={(event) => {
      if (event.key !== 'Enter' || event.shiftKey || event.defaultPrevented ||
          event.nativeEvent.isComposing || event.nativeEvent.keyCode === 229) return;
      event.preventDefault();
      const message = editor.current?.exportMarkdown() ?? '';
      if (!message.trim()) return;
      onSend(message);
      editor.current?.importMarkdown('');
    }}>
      <BbangEditor ref={editor} config={config} />
    </div>
  );
}
```

- **段落与列表**　支持多段落、无序列表和数字列表。段首输入 `-` 或 `1.` 再按空格即可创建列表。任务列表及围栏代码块在此模式下禁用。
- **行内格式**　支持粗体、斜体、下划线、删除线和行内代码。闭合反引号后可继续输入普通文字。
- **提及**　支持原子化的 @mention 标签。宿主通过 `onMentionInput`、`onMentionKeyDown` 和 `ref.confirmMention()` 提供候选数据及弹层。候选菜单处理 Enter 时可优先确认标签。
- **输入与编辑**　支持中文输入法、多块粘贴、撤销和重做。占位提示仅在整个输入框是一个空段落时出现。

接入方可通过 `confirmMention({ sessionId, label, iconUrl, payload })` 显示图标和名称。`iconUrl` 可传入 SVG 或 PNG 地址。

## 普通文档编辑器

组件默认使用文档模式。已有自定义授权的项目仍可通过 `config.license` 传入签名文本。

```tsx
import { BbangEditor } from 'bbang-react-editor';
import 'bbang-react-editor/style.css';

export default function Note() {
  return <BbangEditor defaultValue={'# 我的笔记\n\n从这里开始写。'} />;
}
```

`onChange` 接收 Markdown，`readOnly` 开启只读展示。需要立即读取当前草稿时，可使用示例中的 `exportMarkdown()`。

[在线演示](https://jiuyostar.github.io/editor-demo/) · [反馈问题](https://github.com/JiuYoStar/editor-demo/issues)
