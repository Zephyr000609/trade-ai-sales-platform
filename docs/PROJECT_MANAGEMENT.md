# 项目管理规则

## 任务类型

- Epic：大型功能范围
- Feature：用户可感知的完整功能
- Task：具体开发任务
- Bug：缺陷
- Change Request：需求变更
- Research：技术验证
- Data：数据整理或迁移
- Security：安全任务
- Test：测试和验收
- Documentation：文档任务

## 看板状态

- Inbox
- Ready
- In Progress
- AI Review
- Human Review
- Testing
- Blocked
- Done
- Rejected

## 优先级

- P0：数据泄露、错误自动发送、跨用户数据访问、关键参数严重错误
- P1：主要业务流程不可用
- P2：有替代方案但显著影响效率
- P3：一般体验问题
- P4：长期优化

## Issue 必填信息

- 用户场景
- 当前问题
- 预期结果
- 输入与输出
- 业务规则
- 页面或交互
- 异常情况
- 数据与权限影响
- 验收标准
- 测试案例
- 关联文档

## 完成定义

- 验收标准全部通过
- 单元测试和关键集成测试通过
- 权限测试通过
- 错误处理完整
- 没有硬编码密钥
- 日志已脱敏
- 文档已更新
- 具备部署及回滚路径

## WenzFlow 使用规则

- WenzFlow 只执行处于 Ready 状态且验收标准明确的 Issue。
- 每次只处理一个边界清晰的任务。
- 代码修改必须通过 Pull Request 回到 GitHub。
- AI 生成代码必须经过测试和人工审核。
- 需求、Prompt 和架构决策不能只保存在 WenzFlow 对话中。

## 变更请求

所有新增字段、页面调整和规则变化必须说明：

- 当前行为与期望行为
- 字段名称、类型、默认值和是否必填
- 适用行业
- 对历史数据的影响
- 对 AI Prompt 和选型规则的影响
- 对 API、页面和测试的影响
