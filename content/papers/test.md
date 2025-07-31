# 悬停效果测试文档

## 测试目标

验证交互式表格在您的GitHub网站环境中的实际表现，确保悬停效果完全稳定。

<style>
/* 基于Grok分析的稳定悬停解决方案 */
.test-table {
    width: 100%;
    border-collapse: separate;
    border-spacing: 0;
    table-layout: fixed;
    margin: 20px 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.test-table th {
    background-color: #2c3e50;
    color: white;
    padding: 15px 12px;
    text-align: center;
    border: 1px solid #34495e;
    font-size: 14px;
    font-weight: bold;
}

.test-table td {
    border: 1px solid #ddd;
    padding: 15px 12px;
    vertical-align: top;
    background-color: #fff;
    position: relative;
    transition: background-color 0.2s ease;
    font-size: 14px;
    line-height: 1.5;
}

.test-table td:hover {
    background-color: #f8f9fa;
    cursor: pointer;
}

.cell-tooltip {
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
    margin-top: 8px;
    transition: opacity 0.2s ease, visibility 0.2s ease;
    pointer-events: none;
    /* 防止溢出视口 */
    max-width: calc(100vw - 40px);
    word-wrap: break-word;
}

/* 右侧单元格的tooltip向左显示 */
.test-table td:last-child .cell-tooltip {
    left: auto;
    right: 0;
}

/* 如果是底部行，tooltip向上显示 */
.test-table tbody tr:last-child .cell-tooltip {
    top: auto;
    bottom: 100%;
    margin-top: 0;
    margin-bottom: 8px;
}

.test-table tbody tr:last-child .cell-tooltip::before {
    top: auto;
    bottom: -6px;
    border-bottom: none;
    border-top: 6px solid #2c3e50;
}

.test-table td:hover .cell-tooltip {
    opacity: 1;
    visibility: visible;
}

.cell-tooltip::before {
    content: '';
    position: absolute;
    top: -6px;
    left: 20px;
    border-left: 6px solid transparent;
    border-right: 6px solid transparent;
    border-bottom: 6px solid #2c3e50;
}

.complex-tooltip {
    width: 320px;
    max-width: calc(100vw - 40px);
}

/* 右侧单元格的复杂tooltip */
.test-table td:last-child .complex-tooltip {
    left: auto;
    right: 0;
}

/* 底部行的复杂tooltip */
.test-table tbody tr:last-child .complex-tooltip {
    top: auto;
    bottom: 100%;
    margin-top: 0;
    margin-bottom: 8px;
}

.test-table tbody tr:last-child .complex-tooltip::before {
    top: auto;
    bottom: -6px;
    border-bottom: none;
    border-top: 6px solid #2c3e50;
}

.complex-tooltip h4 {
    margin: 0 0 8px 0;
    color: #3498db;
    font-size: 13px;
    border-bottom: 1px solid #3498db;
    padding-bottom: 4px;
}

.complex-tooltip ul {
    margin: 0;
    padding-left: 18px;
    list-style-type: disc;
}

.complex-tooltip li {
    margin-bottom: 4px;
    font-size: 12px;
}

.complex-tooltip li strong {
    color: #e74c3c;
}

.test-status {
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

## 简单悬停测试

<table class="test-table">
<thead>
<tr>
<th style="width: 30%;">测试项目</th>
<th style="width: 70%;">悬停内容</th>
</tr>
</thead>
<tbody>
<tr>
<td>
基础功能测试
<div class="cell-tooltip">如果您能看到这个提示，说明基础悬停功能正常工作</div>
</td>
<td>
视觉稳定性测试
<div class="cell-tooltip">测试tooltip是否会出现位置跳动或闪烁现象</div>
</td>
</tr>
<tr>
<td>
响应速度测试
<div class="cell-tooltip">测试悬停响应速度和动画流畅性</div>
</td>
<td>
边界区域测试
<div class="cell-tooltip">请在单元格的边缘和角落区域测试悬停效果</div>
</td>
</tr>
</tbody>
</table>

## 历史节点模拟测试

<table class="test-table">
<thead>
<tr>
<th style="width: 20%;">参与方</th>
<th style="width: 40%;">公元前5世纪中期</th>
<th style="width: 40%;">公元前4世纪前期</th>
</tr>
</thead>
<tbody>
<tr>
<td>
哲学界
<div class="cell-tooltip">理性质疑权威的哲学基础建立阶段</div>
</td>
<td>
智者学派兴起，普罗泰戈拉"人是万物尺度"
<div class="cell-tooltip">首次系统性地挑战传统的绝对真理观念，为理性主义奠定基础</div>
</td>
<td>
苏格拉底发展诘问法 <span class="collision-marker">⚡</span>
<div class="cell-tooltip">通过"知道自己无知"的方法论，确立了理性质疑的合法地位</div>
</td>
</tr>
<tr>
<td>
政治界
<div class="cell-tooltip">传统政治权威面临理性挑战的历史阶段</div>
</td>
<td>
雅典民主制受到智者思想冲击
<div class="cell-tooltip">传统的政治合法性开始受到基于理性论证的质疑</div>
</td>
<td>
苏格拉底案审判(399BC) <span class="collision-marker">⚡⚡</span>
<div class="cell-tooltip">理性质疑与政治权威的首次正面冲突，标志性历史事件</div>
</td>
</tr>
</tbody>
</table>

## 五层传导分析测试

<table class="test-table">
<thead>
<tr>
<th style="width: 30%;">历史节点</th>
<th style="width: 70%;">传导分析</th>
</tr>
</thead>
<tbody>
<tr>
<td>
智者学派兴起
<div class="cell-tooltip complex-tooltip">
<h4>智者学派兴起节点</h4>
<ul>
<li><strong>元价值层：</strong>绝对真理 → 相对主义</li>
<li><strong>核心价值层：</strong>神圣智慧 → 人文知识</li>
<li><strong>认知框架层：</strong>权威接受 → 理性辩论</li>
<li><strong>传播系统层：</strong>神庙教导 → 收费教学</li>
<li><strong>结构现实层：</strong>教育市场化，知识商品化</li>
</ul>
</div>
</td>
<td>
普罗泰戈拉"人是万物尺度"的革命性意义
<div class="cell-tooltip complex-tooltip">
这一表述彻底颠覆了传统的认识论基础，将真理的判断标准从超越性的神或自然转向了人类主体，为后续两千年的理性主义发展奠定了哲学基础。
</div>
</td>
</tr>
<tr>
<td>
苏格拉底审判
<div class="cell-tooltip complex-tooltip">
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
理性质疑权威的历史代价
<div class="cell-tooltip complex-tooltip">
苏格拉底之死标志着理性质疑与传统权威不可调和的根本冲突，同时也确立了理性殉道者的崇高地位，为后世的理性主义运动提供了精神象征。
</div>
</td>
</tr>
</tbody>
</table>

## 测试结果评估

<div class="test-status">
<h3>请在您的网站环境中测试以下项目：</h3>

**基础功能：**
- [ ] 悬停时tooltip正常显示
- [ ] 离开时tooltip正常隐藏
- [ ] 没有位置跳动现象
- [ ] 动画过渡流畅

**交互体验：**
- [ ] 单元格任意位置都能触发悬停
- [ ] 复杂内容（五层分析）显示完整
- [ ] 在移动设备上的表现可接受
- [ ] 不与网站其他CSS发生冲突

**视觉效果：**
- [ ] tooltip背景和文字颜色正确
- [ ] 边框圆角和阴影正常
- [ ] 箭头指示器位置正确
- [ ] 字体大小和行距合适
</div>

## 如果测试成功

这意味着我们可以开始制作康德项目的完整交互式历史表格了！包括：

1. **苏格拉底节点：理性质疑权威的首次现实冲突**
2. **中世纪综合节点：理性与信仰的平衡博弈**
3. **文艺复兴/宗教改革节点：理性复兴与意外解放**
4. **科学革命/启蒙节点：理性成功示范与全面挑战**
5. **康德革命节点：理性立法权的最终确立**

每个节点都将采用这种稳定的悬停技术，为读者提供宏观历史脉络和微观五层传导分析的完美结合。

---

**测试完成后，请告知结果，我们将开始正式的内容制作！**
