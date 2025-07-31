# 智能方向调整的悬停测试

基于Grok的专业建议，实现tooltip智能避开视口底部遮蔽。

<style>
/* 基于Grok建议的智能方向tooltip */
.smart-table {
    width: 100%;
    border-collapse: separate;
    border-spacing: 0;
    table-layout: fixed;
    margin: 20px 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.smart-table th {
    background-color: #2c3e50;
    color: white;
    padding: 15px 12px;
    text-align: center;
    border: 1px solid #34495e;
    font-size: 14px;
    font-weight: bold;
}

.smart-table td {
    border: 1px solid #ddd;
    padding: 15px 12px;
    vertical-align: top;
    background-color: #fff;
    position: relative;
    transition: background-color 0.2s ease;
    font-size: 14px;
    line-height: 1.5;
}

.smart-table td:hover {
    background-color: #f8f9fa;
    cursor: pointer;
}

/* 默认向下显示的tooltip */
.smart-tooltip {
    opacity: 0;
    visibility: hidden;
    position: absolute;
    top: 100%;
    left: 0;
    background: #2c3e50;
    color: white;
    padding: 12px 15px;
    border-radius: 6px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    z-index: 1000;
    font-size: 13px;
    line-height: 1.4;
    width: 280px;
    max-width: calc(100vw - 20px);
    margin-top: 8px;
    transition: opacity 0.2s ease, visibility 0.2s ease;
    pointer-events: none;
    word-wrap: break-word;
    white-space: nowrap;
}

.smart-table td:hover .smart-tooltip {
    opacity: 1;
    visibility: visible;
}

.smart-tooltip::before {
    content: '';
    position: absolute;
    top: -6px;
    left: 20px;
    border-left: 6px solid transparent;
    border-right: 6px solid transparent;
    border-bottom: 6px solid #2c3e50;
}

/* 媒体查询：当视口高度较小时，tooltip向上显示 */
@media (max-height: 600px) {
    .smart-tooltip {
        top: auto;
        bottom: 100%;
        margin-top: 0;
        margin-bottom: 8px;
    }
    
    .smart-tooltip::before {
        top: auto;
        bottom: -6px;
        border-bottom: none;
        border-top: 6px solid #2c3e50;
    }
}

/* 对于复杂内容的tooltip */
.complex-smart-tooltip {
    width: 320px;
    max-width: calc(100vw - 20px);
    white-space: normal;
}

.complex-smart-tooltip h4 {
    margin: 0 0 8px 0;
    color: #3498db;
    font-size: 13px;
    border-bottom: 1px solid #3498db;
    padding-bottom: 4px;
}

.complex-smart-tooltip ul {
    margin: 0;
    padding-left: 18px;
    list-style-type: disc;
}

.complex-smart-tooltip li {
    margin-bottom: 4px;
    font-size: 12px;
}

.complex-smart-tooltip li strong {
    color: #e74c3c;
}

/* 模拟底部场景的容器 */
.bottom-test {
    margin-top: 80vh;
}

.test-info {
    background-color: #e8f4f8;
    border: 1px solid #3498db;
    padding: 15px;
    border-radius: 5px;
    margin: 20px 0;
}

.collision-marker {
    color: #e74c3c;
    font-weight: bold;
}
</style>

## 正常位置测试

<table class="smart-table">
<thead>
<tr>
<th>测试项目</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td>
正常显示测试
<div class="smart-tooltip">这个tooltip应该向下显示，因为有足够的空间</div>
</td>
<td>
基础功能验证
<div class="smart-tooltip">验证基础的悬停和显示功能是否正常工作</div>
</td>
</tr>
</tbody>
</table>

## 接近底部位置测试

<div class="bottom-test">
<table class="smart-table">
<thead>
<tr>
<th style="width: 20%;">参与方</th>
<th style="width: 40%;">历史事件</th>
<th style="width: 40%;">五层分析</th>
</tr>
</thead>
<tbody>
<tr>
<td>
哲学界
<div class="smart-tooltip">在视口高度较小时，这个tooltip应该自动向上显示</div>
</td>
<td>
苏格拉底审判(399BC) <span class="collision-marker">⚡⚡</span>
<div class="smart-tooltip complex-smart-tooltip">
<h4>苏格拉底审判节点</h4>
<ul>
<li><strong>元价值层：</strong>理性质疑 → 政治权威反击</li>
<li><strong>核心价值层：</strong>个人良知 → 集体决定</li>
<li><strong>认知框架层：</strong>哲学思辨 → 法庭审判</li>
<li><strong>传播系统层：</strong>私人对话 → 公共审判</li>
<li><strong>结构现实层：</strong>死刑判决，理性与权力正面冲突</li>
</ul>
</div>
</td>
<td>
理性革命的代价
<div class="smart-tooltip complex-smart-tooltip">
苏格拉底之死标志着理性质疑与传统权威不可调和的根本冲突，同时也确立了理性殉道者的崇高地位，为后世的理性主义运动提供了精神象征。这个tooltip内容较长，测试在底部位置时是否能完整向上显示。
</div>
</td>
</tr>
<tr>
<td>
政治界
<div class="smart-tooltip">传统政治权威面临理性挑战的关键时期</div>
</td>
<td>
民主制度受冲击
<div class="smart-tooltip">雅典民主制度开始面临基于理性论证的系统性质疑</div>
</td>
<td>
权力与理性的对立
<div class="smart-tooltip">这是理性与政治权力首次公开、激烈的正面冲突</div>
</td>
</tr>
</tbody>
</table>
</div>

<div class="test-info">
<h3>测试指标</h3>
<p><strong>正常位置（页面上方）：</strong></p>
<p>• tooltip应该向下显示在单元格下方</p>
<p>• 箭头指向上方（单元格）</p>

<p><strong>底部位置（页面下方）：</strong></p>
<p>• 在视口高度≤600px时，tooltip应该自动向上显示</p>
<p>• 箭头指向下方（单元格）</p>
<p>• 完整内容可见，无需滚动</p>

<p><strong>通用要求：</strong></p>
<p>• 悬停响应流畅，无跳动</p>
<p>• 复杂内容（五层分析）完整显示</p>
<p>• 移动设备兼容</p>
</div>

## 如果测试成功

这意味着我们找到了完美的解决方案，可以开始制作康德项目的完整交互式历史表格：

1. **苏格拉底节点：理性质疑权威的首次现实冲突**
2. **中世纪综合节点：理性与信仰的平衡博弈**  
3. **文艺复兴/宗教改革节点：理性复兴与意外解放**
4. **科学革命/启蒙节点：理性成功示范与全面挑战**
5. **康德革命节点：理性立法权的最终确立**

---

**请测试这个版本，特别注意：**
- 滚动到页面底部测试底部表格的tooltip方向
- 在不同设备和浏览器窗口大小下测试
- 确认tooltip内容完整可见，无需手动滚动
