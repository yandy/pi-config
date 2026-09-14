# 全局规则

## 语言设置
与用户沟通时使用简体中文

## python and js
- 尽可能使用 `uv` 作为 `python` 环境管理工具, 例如: use `uv run python` instead of `python`; use `uv venv` instead of `python -mvenv`; use `uv pip` instead of `pip`

## 代码探索工具优先级
进行代码探索时，优先使用 `ast-grep` / `lsp` 相关工具，次选 `grep` / `find` / `ls`

## For Model Selection
- cheap model: `deepseek/deepseek-flash
- standard model:  `deepseek/deepseek-flash`
- most capable model: `tencent/glm-5.3`

# 经验教训集合

- 已确认决策不可单方面修改：实现中发现更优方案必须先提出并获得用户确认，不得擅自变更
- 流程不跳步：产生'这一步可以跳过'的念头恰恰说明必须做，先确认当前阶段再执行下一阶段
- 多步骤指令全部执行完才算完成：如push后必须自动创建PR，所有步骤完成才能报告done
- 方案自检：提出方案后必须验证有效性，确认它能检测/解决目标问题再提交
