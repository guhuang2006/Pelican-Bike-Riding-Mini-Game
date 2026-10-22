# 鹈鹕专送・Pelican‑Express

> 
> 海鸟驰骋滨海公路，迎着海风开启快递派送之旅。
> 朝晖、落日雨夜、全力冲刺，**全部依靠纯 HTML + CSS 实现**。
> 零 JavaScript 代码，零外部图片与 SVG 资源。

---

## 目录

- [项目简介](#%E9%A1%B9%E7%9B%AE%E7%AE%80%E4%BB%8B)
- [功能总览](#%E5%8A%9F%E8%83%BD%E6%80%BB%E8%A7%88)
- [核心技术拆解](#%E6%A0%B8%E5%BF%83%E6%8A%80%E6%9C%AF%E6%8B%86%E8%A7%A3)
  - [1. 表单控件构建 CSS 状态机](#1-%E8%A1%A8%E5%8D%95%E6%8E%A7%E4%BB%B6%E6%9E%84%E5%BB%BA-css-%E7%8A%B6%E6%80%81%E6%9C%BA)
  - [2. 响应式舞台：容器查询与统一单位变量](#2-%E5%93%8D%E5%BA%94%E5%BC%8F%E8%88%9E%E5%8F%B0%E5%AE%B9%E5%99%A8%E6%9F%A5%E8%AF%A2%E4%B8%8E%E7%BB%9F%E4%B8%80%E5%8D%95%E4%BD%8D%E5%8F%98%E9%87%8F)
  - [3. 环境光照系统：CSS 变量实现场景平滑过渡](#3-%E7%8E%AF%E5%A2%83%E5%85%89%E7%85%A7%E7%B3%BB%E7%BB%9Fcss%E5%8F%98%E9%87%8F%E5%AE%9E%E7%8E%B0%E5%9C%BA%E6%99%AF%E5%B9%B3%E6%BB%91%E8%BF%87%E6%B8%A1)
  - [4. 全局调速：单变量驱动整套动画节拍](#4-%E5%85%A8%E5%B1%80%E8%B0%83%E9%80%9F%E5%8D%95%E5%8F%98%E9%87%8F%E9%A9%B1%E5%8A%A8%E6%95%B4%E5%A5%97%E5%8A%A8%E7%94%BB%E8%8A%82%E6%8B%8D)
  - [5. 载具构建：边框与渐变拼接完整交通工具](#5-%E8%BD%BD%E5%85%B7%E6%9E%84%E5%BB%BA%E8%BE%B9%E6%A1%86%E4%B8%8E%E6%B8%90%E5%8F%98%E6%8B%BC%E6%8E%A5%E5%AE%8C%E6%95%B4%E4%BA%A4%E9%80%9A%E5%B7%A5%E5%85%B7)
  - [6. 鸟类腿部：余弦定理推导 12 帧骨骼动画](#6-%E9%B8%9F%E7%B1%BB%E8%85%BF%E9%83%A8%E4%BD%99%E5%BC%A6%E5%AE%9A%E7%90%86%E6%8E%A8%E5%AF%BC12%E5%B8%A7%E9%AA%A8%E9%AA%BC%E5%8A%A8%E7%94%BB)
  - [7. 多层视差滚动：传送带式无限循环场景](#7-%E5%A4%9A%E5%B1%82%E8%A7%86%E5%B7%AE%E6%BB%9A%E5%8A%A8%E4%BC%A0%E9%80%81%E5%B8%A6%E5%BC%8F%E6%97%A0%E9%99%90%E5%BE%AA%E7%8E%AF%E5%9C%BA%E6%99%AF)
  - [8. 天气系统：降雨、积水水洼、雷电闪光效果](#8-%E5%A4%A9%E6%B0%94%E7%B3%BB%E7%BB%9F%E9%99%8D%E9%9B%A8%E7%A7%AF%E6%B0%B4%E6%B0%B4%E6%B4%BC%E9%9B%B7%E7%94%B5%E9%97%AA%E5%85%89%E6%95%88%E6%9E%9C)
  - [9. 多角色复用：共用 DOM 结构，CSS 样式差异化覆写](#9-%E5%A4%9A%E8%A7%92%E8%89%B2%E5%A4%8D%E7%94%A8%E5%85%B1%E7%94%A8dom%E7%BB%93%E6%9E%84css%E6%A0%B7%E5%BC%8F%E5%B7%AE%E5%BC%82%E5%8C%96%E8%A6%86%E5%86%99)
  - [10. 隐藏彩蛋：纯 CSS 实现 14 次点击解锁平行世界](#10-%E9%9A%90%E8%97%8F%E5%BD%A9%E8%9B%8B%E7%BA%AFcss%E5%AE%9E%E7%8E%B014%E6%AC%A1%E7%82%B9%E5%87%BB%E8%A7%A3%E9%94%81%E5%B9%B3%E8%A1%8C%E4%B8%96%E7%95%8C)
  - [11. 无障碍适配与性能优化方案](#11-%E6%97%A0%E9%9A%9C%E7%A2%8D%E9%80%82%E9%85%8D%E4%B8%8E%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96%E6%96%B9%E6%A1%88)
- [仓库文件结构](#%E4%BB%93%E5%BA%93%E6%96%87%E4%BB%B6%E7%BB%93%E6%9E%84)
- [核心参数速查表](#%E6%A0%B8%E5%BF%83%E5%8F%82%E6%95%B0%E9%80%9F%E6%9F%A5%E8%A1%A8)
- [项目局限与取舍说明](#%E9%A1%B9%E7%9B%AE%E5%B1%80%E9%99%90%E4%B8%8E%E5%8F%96%E8%88%8D%E8%AF%B4%E6%98%8E)
- [项目技术栈](#%E9%A1%B9%E7%9B%AE%E6%8A%80%E6%9C%AF%E6%A0%88)

---

## 项目简介

**鹈鹕专送**是一份单文件、零外部依赖的 CSS 创意动画演示页面。
天空大海、沙滩海岸、滨海公路、交通工具、鸟类角色全部由普通`div`标签、`border`边框、各类渐变以及`@keyframes`关键帧组合绘制，不引入任何位图素材，全程不使用 JS 脚本。

本项目也是一次 CSS 能力边界的实践演示：

- 3 套环境天色 × 3 档骑行速度 × 3 位鸟类角色 × 3 种交通工具 × 4 种天气模式
- 点击 14 次解锁隐藏平行世界彩蛋剧情
- 页面内置可折叠技术维修手册，通过小型动画卡片直观讲解每一块核心实现原理

## 功能总览

表格

| 分类 | 选项 | 功能说明 |
| --- | --- | --- |
| 天色环境 | ☀️黎明 / 🌇黄昏 / 🌙深夜 | 联动修改全场景配色、日月位置、星空、路灯发光效果 |
| 骑行速度 | 🚶漫步 / 🚲巡航 / 🔥疾冲 | 统一调整全部动画播放倍率，动作节奏同步变化 |
| 骑行角色 | 🪽鹈鹕 / 🦜鹦鹉 / 🦉猫头鹰 | 复用同一套骨骼 DOM，依靠 CSS 修改外观色彩造型 |
| 交通工具 | 🚲自行车 / 🛹滑板 / 🛵电动滑板车 | 复用腿部骨骼，非骑行载具切换为静态站立姿态 |
| 天气效果 | ☀️晴天 / ☁️阴天 / 🌧️小雨 / ⛈️雷雨 | 包含雨丝、路面水洼涟漪、闪电闪光、环境压暗 |
| 播放控制 | ⏸暂停预览 | 通过`animation‑play‑state`冻结页面所有动画 |
| 隐藏彩蛋 | 鹈鹕 + 自行车，连续点击角色 14 次 | 白光转场动画，解锁反转世界线剧情 |

---

### 1. 表单控件构建 CSS 状态机

整个页面不存在任何脚本逻辑，所有交互状态全部由隐藏的`radio`单选框、`checkbox`复选框保存。

```
<input class="vh" type="radio" name="skyMode" id="sky‑dawn">
<input class="vh" type="radio" name="skyMode" id="sky‑dusk" checked>
<input class="vh" type="radio" name="skyMode" id="sky‑night">

<div class="stage‑wrap">
  <div class="stage"> <!-- 完整动画场景 --> </div>
</div>
```

输入框全部放置在场景容器`.stage‑wrap`**前面**，借助 CSS 通用兄弟选择器`~`穿透，控制场景内部任意元素样式。

```
#sky‑night:checked ~ .stage‑wrap .stage { --nightOpacity:1; --starOpacity:1; }
#veh‑skate:checked ~ .stage‑wrap .vehicle‑skate { display:block; }
#anim‑pause:checked ~ .stage‑wrap .stage,
#anim‑pause:checked ~ .stage‑wrap .stage * { animation‑play‑state: paused !important; }
```

表格

| 交互需求 | 实现手段 |
| --- | --- |
| 互斥选项切换 | `radio`单选框，设置相同`name`属性 |
| 布尔开关 | `checkbox`复选框 |
| 自定义外观按钮 | `<label for="id">`，完全重写视觉样式 |

`.vh`类将原生输入控件压缩为极小透明元素，**保留键盘聚焦能力**，配合`:focus‑visible`为控制面板绘制焦点提示边框。

### 2. 响应式舞台：容器查询与统一单位变量

场景舞台固定维持 5:3 宽高比例。

```
.stage {
  --unit: 1px;
  aspect‑ratio: 5 / 3;
  width: 100%;
  overflow: hidden;
}
@supports (width:1cqw) {
  .stage { --unit: 0.1cqw; }
}
```

整套设计稿基准尺寸为`1000 × 600`，页面内全部尺寸统一写成 `calc(N * var(--unit))`。

```
.wheel { width: calc(96 * var(--unit)); height: calc(96 * var(--unit)); }
.rider { left: calc(460 * var(--unit)); top: calc(482 * var(--unit)); }
```

浏览器支持容器查询单位`cqw`时，`1cqw`等于舞台容器宽度的百分之一；`--unit`代表舞台宽度千分之一，**整个画面跟随容器等比例缩放，无需大量媒体查询**。
老旧浏览器自动降级为固定像素原始设计尺寸。
技术手册内的演示卡片同样启用`container‑type: inline‑size`，使用不同`--unit`系数，直接复用整套场景组件嵌入小卡片。

### 3. 环境光照系统：CSS 变量实现场景平滑过渡

天空、海面采用多层元素叠加，依靠透明度自定义变量控制每一层显示权重。

```
.sky‑dawn  { opacity: var(--op‑dawn); }
.sky‑dusk  { opacity: var(--op‑dusk); }
.sky‑night { opacity: var(--op‑night); }
```

切换环境模式本质是批量修改`.stage`上一组 CSS 自定义属性：日月大小位置、云层色调、沙滩马路颜色、景物剪影、路灯亮度、星月透明度全部同步更新。

```
#sky‑night:checked ~ .stage‑wrap .stage {
  --op‑night: 1; --starOpacity:1; --moonOpacity:1;
  --sunOpacity:0; --sandColor:#5b5470; --roadColor:#2b2836; --lampBright:1;
}
```

数十个 DOM 元素共用同一套变量，一次选择完成全场景换装；所有颜色透明度配置添加`transition`过渡，天色环境是平滑渐变，而非生硬切换。

### 4. 全局调速：单变量驱动整套动画节拍

只修改`--speed`一个变量，同步控制页面全部动画周期。

```
#speed‑walk:checked ~ .stage‑wrap .stage { --speed: 0.55; }
#speed‑sprint:checked ~ .stage‑wrap .stage { --speed: 1.75; }

.stage {
  --wheelCycle: calc(1.12s / var(--speed));     /* 车轮旋转周期 */
  --pedalCycle: calc(2.10s / var(--speed));    /* 脚踏踩踏周期 */
  --bgMidCycle: calc(8.60s / var(--speed));    /* 中景景物传送带 */
  --fgCycle: calc(1.45s / var(--speed));      /* 前景草丛 */
  --roadDash: calc(0.35s / var(--speed));     /* 道路虚线移动 */
}
```

云朵、海浪、飞鸟的动画时长全部除以`--speed`，保证场景加速减速时各物体相对运动比例不变。
高速模式出现的速度拖影，利用 CSS 算术表达式动态计算透明度，无需额外条件判断：

```
.speed‑zip { opacity: calc((var(--speed) - 1.3) * 1.3); }
```

速度不足阈值时计算结果为负数，opacity 自动归 0，拖影直接隐藏。

### 5. 载具构建：边框与渐变拼接完整交通工具

表格

| 零件 | 实现方案 |
| --- | --- |
| 轮胎 | `border`厚边框 + `border‑radius:50%`圆形 |
| 轮辐 | `repeating‑conic‑gradient`重复锥形渐变绘制 |
| 花鼓 | 伪元素`::after`小圆块 |
| 牙盘 | 虚线圆环边框 + 伪元素重复虚线环 |

```
@keyframes wheel‑spin { to { transform: rotate(360deg); } }
.wheel { animation: wheel‑spin var(--wheelCycle) linear infinite; }
```

自行车车架全部由同一种管件类`.bar`实现，通过设置宽度、旋转角度、变换原点，拼接三角车架结构。

```
.bar {
  height: calc(5 * var(--unit));
  transform‑origin: 0 50%;
  background:#1f9d8c;
}
.down‑tube { width: calc(77 * var(--unit)); transform: rotate(-35.4deg); }
.seat‑stay { width: calc(94 * var(--unit)); transform: rotate(-43.3deg); }
```

车筐、车铃、挡泥板等细节依靠`clip‑path`裁切、渐变、伪元素组合生成。

### 6. 鸟类腿部：余弦定理推导 12 帧骨骼动画

大腿、小腿、脚掌三层嵌套容器，每一层设置独立旋转原点。

```
<div class="leg near">
  <div class="thigh"><div class="shin"><div class="foot"></div></div></div>
</div>
```

先确定曲柄旋转角度对应的踏板坐标，**使用余弦定理离线计算每帧关节旋转角度**，一共采样 12 帧写入关键帧。

```
@keyframes thigh‑anim {
  0%    { transform: rotate(-5.1deg); }
  8.33% { transform: rotate(-8.4deg); }
  16.67%{ transform: rotate(1.5deg); }
  25%   { transform: rotate(17.8deg); }
  /* …其余关键帧… */
  100%  { transform: rotate(-5.1deg); }
}
```

脚掌额外配置一套反向旋转关键帧，保证骑行过程脚底尽量保持水平。
远离镜头一侧的腿直接设置负的动画延迟，实现双腿交替踩踏：

```
.leg.far :is(.thigh,.shin,.foot) { animation‑delay: calc(var(--pedalCycle) / -2); }
```

踏板保持水平原理：外层跟随曲柄旋转，内层踏板反向旋转抵消角度。

切换滑板、电动滑板车时，**不修改 DOM 结构，直接关闭腿部动画，赋值静态旋转角度**，同时整体偏移骑手位置适配载具高度。

```
.vehicle‑skate .leg :is(.thigh,.shin,.foot) { animation: none; }
.vehicle‑skate .leg.near .thigh { transform: rotate(73.6deg); }
```

### 7. 多层视差滚动：传送带式无限循环场景

前进视觉效果依靠三层景物以不同速度横向滚动实现：

表格

| 层级 | 包含景物 | 移动距离 | 运动速度 |
| --- | --- | --- | --- |
| 远景 | 云朵、海面船只、海鸟 | 1080u → -260u | 最慢 |
| 中景 | 路灯、长椅、路牌、礁石浮标 | -1000u | 中等 |
| 前景 | 路边草丛 | -500u | 最快 |

无限无缝循环方案：**每组景物复制两份并排摆放**，当第一组完全移出屏幕，第二组刚好衔接上。

```
<div class="belt">
  <div class="bgroup"> <!-- 第一组景物 --> </div>
  <div class="bgroup" aria‑hidden="true"> <!-- 重复副本 --> </div>
</div>
```

```
@keyframes belt‑move { to { transform: translateX(calc(-1000 * var(--unit))); } }
.bgroup + .bgroup { left: calc(1000 * var(--unit)); }
```

道路虚线不复制 DOM，直接动态修改`background‑position`实现流动。
海浪使用多层半透明横条反向滚动；水面波光利用重复渐变加径向遮罩，跟随太阳位置左右移动。

### 8. 天气系统：降雨、积水水洼、雷电闪光效果

开启雨天不会改动 DOM 结构，只叠加多层视觉元素，通过变量控制开关。

1. 环境压暗层：半透明渐变遮罩，受`--stormOpacity`变量控制
2. 雨丝背景：径向渐变模拟雨滴，两层雨层设置不同速度透明度营造景深，动画修改`background‑position`实现下落

```
@keyframes rain‑fall { to { background‑position: 0 calc(320 * var(--unit)); } }
```

3. 地面水洼涟漪：椭圆容器搭配圆环伪元素，执行缩放淡出动画模拟水纹扩散

```
@keyframes ripple { from {transform:scale(.25);opacity:.9;} to {transform:scale(1);opacity:0;} }
```

4. 闪电闪光：长周期关键帧，只在少数时间点设置不透明度，其余时刻完全透明

```
@keyframes lightning {
  0%,86%,90%,100% { opacity:0; }
  87%,89% { opacity:0.5; }
  88% { opacity:0.12; }
}
```

开启雨天同时自动降低太阳亮度、关闭水面波光、修改云层颜色，全部通过 CSS 变量完成切换。

### 9. 多角色复用：共用 DOM 结构，CSS 样式差异化覆写

鹈鹕、鹦鹉、猫头鹰**完全复用同一套 DOM 骨架**：尾巴、躯干、翅膀、脖颈、头部、喙、眼皮结构完全一致。角色区别全部依靠 CSS 背景渐变、颜色、尺寸覆写完成。

```
.bird‑parrot .body {
  background:
    radial‑gradient(58% 52% at 66% 64%, #ffd257 0 46%, transparent 47%),
    radial‑gradient(46% 42% at 26% 26%, #2aa5a0 0 42%, transparent 43%),
    linear‑gradient(150deg,#e8503a,#b83c28);
}
```

角色切换逻辑：默认全部隐藏，勾选对应单选框后显示目标鸟类。
微动画全部是关键帧实现：自动眨眼、鹈鹕喉囊呼吸起伏、喙部微动，鸟类点头摆动节拍和脚踏踩踏周期联动同步。

```
@keyframes blink { 0%,91%,100% {transform:scaleY(0);} 94%,96.5% {transform:scaleY(1);} }
.eye‑lid { animation: blink 4.6s infinite; }
```

### 10. 隐藏彩蛋：纯 CSS 实现 14 次点击解锁平行世界

#### 点击计数实现

鹈鹕角色上方堆叠 14 个透明`label`标签，分别对应一组复选框。

```
<label class="click‑layer c1" for="egg1"></label>
<label class="click‑layer c2" for="egg2"></label>
<!-- 一直到 c14 -->
```

初始状态只有第一层可以点击，每勾选一层就关闭当前层点击，开启下一层：

```
.click‑layer { pointer‑events: none; }
.click‑layer.c1 { pointer‑events: auto; }
#egg1:checked ~ .stage‑wrap .c1 { pointer‑events:none; }
#egg1:checked ~ .stage‑wrap .c2 { pointer‑events:auto; }
/* 链式传递至第14层 */
```

形成一条状态锁链，无法直接跳过中间步骤点到最后一层。

#### 交互反馈

- 右上角点阵进度指示器，每点击一次点亮对应点位
- `:active`点击状态，给鸟类施加轻微挤压缩放反馈

#### 触发反转剧情

当第 14 个复选框被勾选，彩蛋按钮解除隐藏，设置`pointer‑events:auto`允许点击。
点击按钮勾选总开关`#egg`，启动 7.5 秒白光闪白转场动画，在转场中段替换整套显示元素。
反转世界线场景中，鹈鹕放大，迷你缩小版自行车放到鸟背上，添加持续上下弹跳动画；右下角提供返回按钮，取消勾选恢复原始世界。

> 
> 彩蛋逻辑做了条件限制：只有选择鹈鹕 + 自行车时，点击层才开启响应；其他载具角色直接屏蔽全部点击。

### 11. 无障碍适配与性能优化方案

**无障碍处理**

- 隐藏表单控件保留 Tab 键盘导航，`:focus‑visible`给控制面板增加焦点外框提示。
- 主场景使用`<figure>`搭配`aria‑label`说明，重复装饰元素设置`aria‑hidden="true"`。
- 完整尊重系统减弱动画偏好设置：

```
@media (prefers‑reduced‑motion: reduce) {
  *,*::before,*::after { animation: none !important; }
}
```

**性能策略**

- 动画仅操作`transform`与`opacity`，少量使用`background‑position`，不会触发页面重排重计算布局。
- 无限滚动采用静态副本位移，运行时无 DOM 新增删除。
- 整个场景被`overflow:hidden`裁剪，绘制区域限制在舞台容器之内，减少多余渲染。
- 没有图片请求、没有图标库、没有 JS 解析开销。

**滚动渐进增强**
浏览器支持`animation‑timeline: view()`时，页面章节拥有随滚动入场动画；不支持该特性的浏览器直接忽略，内容正常展示，不会破坏基础功能。

---

## 仓库文件结构

```
20261022_v1.3.html      # 完整单文件页面，HTML、CSS全部内联，无JS
20260911_v1.2.html      # v1.2历史归档版本
README.md               # 本项目说明文档
```

## 核心参数速查表

表格

| CSS 变量 | 默认值 | 用途说明 |
| --- | --- | --- |
| `--unit` | `0.1cqw` | 全局设计缩放单位，1u 等价原始稿 1px |
| `--speed` | `1` | 全局动画速度倍率 |
| `--pedalCycle` | `2.1s / var(--speed)` | 脚踏完整踩踏一圈时长 |
| `--wheelCycle` | `1.12s / var(--speed)` | 车轮旋转一周时长 |
| `--bgMidCycle` | `8.60s / var(--speed)` | 中景景物传送带周期 |
| `--fgCycle` | `1.45s / var(--speed)` | 前景草丛滚动周期 |
| `--roadDash` | `0.35s / var(--speed)` | 路面虚线流动周期 |
| `--op‑dawn / --op‑dusk / --op‑night` | `0 / 1 / 0` | 三套天色叠加透明度权重 |
| `--lampBright` | `0/1` | 路灯发光强度开关 |
| `--rainOpacity / --stormOpacity` | `0` | 雨天、风暴遮罩透明度 |

## 项目局限与取舍说明

1. **依赖容器查询 cqw 单位**：老旧浏览器不支持时，页面退化为固定尺寸设计稿，小屏幕显示会偏大。
2. **腿部骨骼为预计算关键帧**：属于离线算好的动画，非实时逆运动解算；修改曲柄尺寸需要重新手动计算整套关节角度。
3. **彩蛋状态单向递进**：点击计数只能往 14 次递增，界面无法回退前面层级，可以依靠键盘选中输入框重置。
4. **DOM 顺序强约束**：大量依赖兄弟选择器`~`，所有隐藏 input 标签必须放在`.stage‑wrap`之前，改动 HTML 顺序会直接破坏全部交互。
5. **外部网络字体**：字体 CDN 加载失败会回退系统字体，页面排版会出现轻微差异。
6. **雷雨模式包含高频闪烁画面，光敏癫痫人群不建议使用。**

## 项目技术栈

表格

| 分类 | 详情 |
| --- | --- |
| HTML | HTML5 语义标签 figure、figcaption、label、input 表单控件 |
| CSS | CSS 自定义属性、容器查询、@supports、@keyframes 关键帧、多重渐变、clip‑path、通用兄弟选择器、view 滚动时间线 |
| JavaScript | **完全不使用** |
| 图片资源 | **无，全部 CSS 绘制生成** |
| 字体资源 | 站酷快乐体（标题）、Noto Sans SC 思源黑体（正文） |

> 
> 本项目为前端创意技术演示，仅供个人vibe coding学习研究，禁止直接商用。雷雨模式存在闪光风险，光敏人群请规避。
>
 **本网页由 Qwen3.8-Max 编写**

