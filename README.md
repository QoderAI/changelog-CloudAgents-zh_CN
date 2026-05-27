# Qoder Cloud Agents

[![API](https://img.shields.io/badge/API-v1-blue)](https://api.qoder.com/api/v1/cloud)
[![文档](https://img.shields.io/badge/%E6%96%87%E6%A1%A3-Cloud_Agents-green)](https://docs.qoder.com/zh/cloud-agents)

Qoder Cloud Agents 让你部署 7×24 小时运行的 AI Agent，在安全的云端环境中执行任务——定义一次能力，模型升级时自动进化，无需修改代码。

## 快速开始

```bash
export QODER_PAT="your-personal-access-token"

# 创建 Agent
curl -s -X POST https://api.qoder.com/api/v1/cloud/agents \
  -H "Authorization: Bearer $QODER_PAT" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "my-agent",
    "model": "ultimate",
    "instructions": "You are a helpful programming assistant.",
    "tools": [{"type": "agent_toolset_20260401"}]
  }'

# 创建 Session（将 Agent 绑定到 Environment）
curl -s -X POST https://api.qoder.com/api/v1/cloud/sessions \
  -H "Authorization: Bearer $QODER_PAT" \
  -H "Content-Type: application/json" \
  -d '{
    "agent": "<AGENT_ID>",
    "environment_id": "<ENV_ID>"
  }'

# 发送消息
curl -s -X POST https://api.qoder.com/api/v1/cloud/sessions/<SESSION_ID>/events \
  -H "Authorization: Bearer $QODER_PAT" \
  -H "Content-Type: application/json" \
  -d '{
    "events": [{
      "type": "user.message",
      "content": "Hello, Cloud Agent!"
    }]
  }'

# 流式接收响应（SSE）
curl -s -N https://api.qoder.com/api/v1/cloud/sessions/<SESSION_ID>/events/stream \
  -H "Authorization: Bearer $QODER_PAT"
