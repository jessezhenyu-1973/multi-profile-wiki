# Computer Use 技能

## 何时使用

当 builder 需要：
- 操作桌面应用（非 Web 端）
- 截图分析或 UI 自动化
- 需要 GUI 交互的任务

## 使用方法

```bash
# 先截图
computer_use(action="capture", mode="som", app="App名称")
# 按元素索引点击
computer_use(action="click", element=N)
```

## 注意事项

- 默认后台操作，不抢占焦点
- 元素索引在每次截图后有效，点击后需重新截图
- 不用于文件编辑（用 write_file/patch）
- 不用于 shell 命令（用 terminal）
