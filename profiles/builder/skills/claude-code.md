# Claude Code 技能

## 何时使用

当 builder 需要：
- 复杂重构或多步骤代码修改
- 需要自主决策的代码实现
- PR review 或代码审查

## 使用方法

```bash
claude -p "任务描述" --allowedTools "Read,Edit,Bash" --max-turns 10
```

## 注意事项

- 复杂任务用 `--max-turns 10-15`
- 简单任务用 `--max-turns 5`
- 始终指定 `--allowedTools` 限制权限
- 注意 `--dangerously-skip-permissions` 的默认选择是 No，需用 Down+Enter
