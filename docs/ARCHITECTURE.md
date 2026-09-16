# 技术架构

## 推荐技术栈

- 前端：Next.js + TypeScript
- UI：Tailwind CSS + shadcn/ui
- 后端：FastAPI
- 数据库：PostgreSQL
- 向量检索：pgvector
- 缓存与队列：Redis
- 后台任务：Celery、RQ 或 Dramatiq
- 文件存储：阿里云 OSS 或腾讯云 COS
- OCR：PaddleOCR，必要时接入云 OCR
- 产品网页采集：Playwright
- 邮件：IMAP 读取、IMAP APPEND 写入草稿、SMTP 作为备用发送通道
- AI：统一模型网关，支持 OpenAI 与 DeepSeek
- 通知：应用内通知 + 企业钉钉
- 部署：Docker Compose 起步
- 监控：Sentry、结构化日志、健康检查和任务告警

## 核心模块

1. 身份认证与数据隔离
2. 邮箱连接与邮件同步
3. 文件解析、OCR 与知识库
4. 产品网页采集与结构化产品库
5. 客户识别、背调和价值分级
6. 技术需求提取与单位标准化
7. 硬条件产品筛选与候选排序
8. 参数对比表与标准价格匹配
9. 英文草稿生成和事实校验
10. 人工补充、审核和修改记录
11. 通知、日志、监控和备份

## 产品选型安全链路

1. 模型只负责将自然语言转换为结构化需求。
2. 所有数值必须保留原文、标准值、单位和来源位置。
3. 硬条件由确定性程序和数据库执行。
4. 只有通过硬条件的型号才能进入候选集。
5. AI 只允许对候选集排序和解释。
6. 草稿生成后重新抽取其中的参数，与来源及选型结果逐项比较。
7. 任何冲突、缺失或低置信度内容进入人工补充状态。

## 主要数据实体

- organizations
- users
- mailboxes
- email_threads
- emails
- attachments
- customers
- contacts
- customer_states
- customer_scores
- product_families
- products
- product_parameters
- knowledge_files
- knowledge_chunks
- technical_requirements
- product_recommendations
- comparison_tables
- price_rules
- drafts
- clarification_requests
- notifications
- ai_runs
- audit_logs

## 多租户原则

即使内部 MVP 暂时只有一家公司，也必须：

- 所有业务表保存 organization_id。
- 邮件及客户保存 user_id 和 mailbox_id。
- 所有查询默认带租户过滤。
- 对象存储路径按企业和用户分区。
- 缓存键和后台任务带租户标识。
- 日志不得输出邮件授权码或完整客户敏感信息。

## 失败处理

- 邮件同步、OCR、向量化、模型调用和草稿同步均需幂等。
- 后台任务必须支持重试、超时和死信状态。
- 失败任务显示可理解的原因和人工恢复入口。
- 禁止因模型失败而自动发送不完整邮件。
