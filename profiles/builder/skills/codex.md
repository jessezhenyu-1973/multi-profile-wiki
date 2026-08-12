# Codex 技能

## 何时使用

当 builder 需要：
- 快速实现功能
- 并行处理多个小任务
- 需要 OpenAI 模型的编码任务

## 使用方法

```bash
cd /git/repo && codex exec "任务描述" --sandbox workspace-write
```

## 注意事项

- 必须在 git 仓库内运行
- 使用 `--sandbox workspace-write` 自动批准文件变更
- 需要 `pty=true`（交互式终端应用）
- 长期任务用 `background=true` + `process` 监控
