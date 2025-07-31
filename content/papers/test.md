# Grok的智能tooltip方案（确切代码）

完全按照Grok提供的代码实现，不做任何修改。

<style>
/* 表格布局稳定 */
table {
  border-collapse: separate;
  table-layout: fixed;
  width: 100%;
  border-spacing: 0;
}

/* 单元格样式 */
td {
  padding: 10px;
  border: 1px solid #ddd;
  position: relative;
  min-height: 40px;
}

th {
  padding: 10px;
  border: 1px solid #ddd;
  background-color: #f5f5f5;
  font-weight: bold;
}

/* tooltip样式 */
.cell-tooltip {
  position: absolute;
  left: 0;
  background: #333;
  color: #fff;
  padding: 5px 10px;
  border-radius: 4px;
  white-space: nowrap;
  z-index: 1000;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.2s ease, visibility 0.2s ease;
  pointer-events: none; /* 防止tooltip干扰鼠标事件 */
}

/* 默认向下显示 */
td:hover .cell-tooltip {
  top: 100%;
  margin-top: 2px; /* 增加间距，避免紧贴 */
  opacity: 1;
  visibility: visible;
}

/* 接近视口底部时向上显示 */
td:hover .cell-tooltip[data-position="top"] {
  top: auto;
  bottom: 100%;
  margin-top: 0;
  margin-bottom: 2px; /* 向上显示时的间距 */
  opacity: 1;
  visibility: visible;
}

/* 单元格内容样式 */
.cell-content {
  display: inline-block;
  width: 100%; /* 确保触发区域覆盖整个单元格 */
}

/* CSS变量检测视口空间（纯CSS近似方案） */
td {
  --space-below: calc(100vh - 100%);
  --tooltip-height: 30px;
}

/* 修复悬停稳定性 */
td:hover .cell-tooltip {
  bottom: auto;
}

/* 接近底部时切换方向 - 增加延迟避免闪烁 */
@media (max-height: 600px) {
  td:hover .cell-tooltip {
    top: auto;
    bottom: 100%;
    margin-bottom: 2px;
    transition-delay: 0.1s; /* 增加延迟 */
  }
}

/* 为测试添加的空间 */
.spacer {
  height: 80vh;
  background: #f0f0f0;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 20px 0;
}
</style>

## Grok方案测试：康德项目五层传导分析表

### 正常区域（向下显示）

<table>
<tr>
<th>层次</th>
<th>描述</th>
<th>康德革命特征</th>
</tr>
<tr>
<td>
<span class="cell-content">元价值层</span>
<span class="cell-tooltip">定义：决定价值来源的哲学基础</span>
</td>
<td>
<span class="cell-content">理性至上</span>
<span class="cell-tooltip">理性成为一切价值判断的最终标准</span>
</td>
<td>
<span class="cell-content">立法权转移</span>
<span class="cell-tooltip">从神的启示转向人类理性的自我立法</span>
</td>
</tr>
<tr>
<td>
<span class="cell-content">核心价值层</span>
<span class="cell-tooltip">定义：基于理性的道德自律原则</span>
</td>
<td>
<span class="cell-content">道德自律</span>
<span class="cell-tooltip">个体通过理性实现道德的自我立法</span>
</td>
<td>
<span class="cell-content">绝对命令</span>
<span class="cell-tooltip">道德法则的普遍有效性要求</span>
</td>
</tr>
</table>

<div class="spacer">
<strong>↓ 滚动到下方，测试底部tooltip的智能方向切换 ↓</strong>
</div>

### 底部区域（智能向上显示）

<table>
<tr>
<th>参与方</th>
<th>历史变化</th>
<th>五层传导分析</th>
</tr>
<tr>
<td>
<span class="cell-content">哲学界</span>
<span class="cell-tooltip" data-position="top">理性质疑权威的哲学基础建立</span>
</td>
<td>
<span class="cell-content">苏格拉底审判(399BC)</span>
<span class="cell-tooltip" data-position="top">理性质疑与政治权威的首次正面冲突</span>
</td>
<td>
<span class="cell-content">传导分析</span>
<span class="cell-tooltip" data-position="top">元价值层：理性质疑→政治反击 | 核心价值层：个人良知→集体决定</span>
</td>
</tr>
<tr>
<td>
<span class="cell-content">政治界</span>
<span class="cell-tooltip" data-position="top">传统政治权威面临理性挑战</span>
</td>
<td>
<span class="cell-content">康德《纯粹理性批判》</span>
<span class="cell-tooltip" data-position="top">理性获得认识论的立法权威</span>
</td>
<td>
<span class="cell-content">革命影响</span>
<span class="cell-tooltip" data-position="top">为启蒙运动和法国大革命提供理论基础</span>
</td>
</tr>
</table>

---

**测试指标：**
- 上方表格：tooltip向下显示
- 下方表格：带有`data-position="top"`的tooltip向上显示
- 媒体查询：视口高度≤600px时自动向上切换
- 悬停任意单元格位置都能触发tooltip
- 无跳动，响应流畅

如果这个版本还是有问题，那可能是我对Grok代码的复制还有遗漏。
