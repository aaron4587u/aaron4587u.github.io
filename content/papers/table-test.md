---
title: "表格功能测试"
date: 2025-01-30
description: "测试网站的表格显示功能"
---

# 表格功能测试

这是一个简单的测试文件，用来验证网站的表格显示功能。

## 测试一：Markdown表格

| 层次 | 变化前 | 变化后 |
|------|--------|--------|
| 价值层 | 传统权威 | 理性立法 |
| 认知层 | 外在约束 | 主体建构 |

## 测试二：简单HTML表格

<table>
<tr>
<th>时期</th>
<th>特征</th>
<th>影响</th>
</tr>
<tr>
<td>启蒙前期</td>
<td>理性挑战</td>
<td>权威松动</td>
</tr>
<tr>
<td>康德时期</td>
<td>理性立法</td>
<td>价值重构</td>
</tr>
</table>

## 测试三：稍复杂的HTML表格

<table>
<thead>
<tr>
<th>历史阶段</th>
<th>核心变化</th>
<th>传导机制</th>
<th>长期影响</th>
</tr>
</thead>
<tbody>
<tr>
<td>古希腊</td>
<td>理性质疑神性</td>
<td>哲学辩论</td>
<td>理性获得话语权</td>
</tr>
<tr>
<td>康德革命</td>
<td>理性自我立法</td>
<td>三大批判体系</td>
<td>价值源泉转移</td>
</tr>
</tbody>
</table>

## 结论

如果您能看到上面三个表格都正常显示，说明网站支持：
- ✅ Markdown表格
- ✅ 基础HTML表格  
- ✅ 带thead/tbody的HTML表格

如果某个表格显示异常，我们就知道问题出在哪里了。
