# 鹈鹕专送 · Pelican Express

> 一只海鸟骑着自行车，沿着海风一号公路一路向前。
> 日落、夜骑、雨天、冲刺——全部由 **纯 HTML + CSS** 完成。
> 没有一行 JavaScript，没有一张图片。

---

## 目录

- [项目简介](#项目简介)
- [功能一览](#功能一览)
- [技术总览](#技术总览)
  - [1. 用表单控件当状态机](#1-用表单控件当状态机)
  - [2. 自适应舞台：容器查询 + 单位变量](#2-自适应舞台容器查询--单位变量)
  - [3. 天色系统：变量驱动的交叉淡入](#3-天色系统变量驱动的交叉淡入)
  - [4. 速度系统：一个 --spd 驱动全部节拍](#4-速度系统一个--spd-驱动全部节拍)
  - [5. 自行车：全是 border 和渐变](#5-自行车全是-border-和渐变)
  - [6. 两条腿：余弦定理解出的 12 帧骨骼](#6-两条腿余弦定理解出的-12-帧骨骼)
  - [7. 三层视差：传送带 + 复制粘贴](#7-三层视差传送带--复制粘贴)
  - [8. 天气：雨、水洼、闪电](#8-天气雨水洼闪电)
  - [9. 三只鸟：共享零件 + 覆写](#9-三只鸟共享零件--覆写)
  - [10. 彩蛋：纯 CSS 的「点 14 次」](#10-彩蛋纯-css-的点-14-次)
  - [11. 无障碍与性能](#11-无障碍与性能)
- [文件结构](#文件结构)
- [设计取值速查](#设计取值速查)
- [已知取舍](#已知取舍)
- [技术栈](#技术栈)

---

## 项目简介

**鹈鹕专送**是一个单文件、零依赖的 CSS 动画演示页面。整个场景——天空、海面、沙滩、公路、自行车、骑手——全部由 `div`、`border`、渐变和关键帧拼成，不含任何位图素材，也没有任何脚本逻辑。

它同时是一份「CSS 能做什么」的技术演示：

- 3 种天色 × 3 种节奏 × 3 种坐骑 × 3 种座驾 × 2 种天气
- 一个隐藏 14 次点击的彩蛋世界线
- 页面下方附带可折叠的「维修手册」，用 4 张迷你动画卡片讲解核心实现

---

## 功能一览

| 维度 | 可选项                       | 说明                                 |
| ---- | ---------------------------- | ------------------------------------ |
| 天色 | ☀️ 清晨 / 🌇 黄昏 / 🌙 夜骑     | 全场景配色、太阳位置、星空、路灯联动 |
| 节奏 | 🚶 散步 / 🚲 巡航 / 🔥 冲刺     | 全局动画速度倍率                     |
| 坐骑 | 🪽 鹈鹕 / 🦜 鹦鹉 / 🦉 猫头鹰   | 共享骨架，CSS 覆写外观               |
| 座驾 | 🚲 自行车 / 🛹 滑板 / 🛵 电动车 | 复用同一套腿部骨骼                   |
| 天气 | ☀️ 晴天 / 🌧️ 雨天              | 雨丝、水洼涟漪、闪电、压暗           |
| 画面 | ⏸ 暂停细看                   | 一行 `animation-play-state` 冻结全场 |
| 彩蛋 | 鹈鹕 × 自行车，连点 14 次    | 白幕过场 → 世界线反转                |

## 

### 1. 用表单控件当状态机

整个页面没有任何脚本，所有状态都靠隐藏的 `radio` / `checkbox` 承载。

html

```
<input class="vh" type="radio" name="theme" id="th-day">
<input class="vh" type="radio" name="theme" id="th-dusk" checked>
<input class="vh" type="radio" name="theme" id="th-night">
...
<div class="stagewrap">
  <figure class="stage">...</figure>
</div>
```



这些 `input` 全部放在 `.stagewrap` **之前**，因此可以用通用兄弟选择器一路命中舞台内部：

css

```
#th-night:checked ~ .stagewrap .stage { --oNight:1; --starsO:1; ... }
#vh-skate:checked ~ .stagewrap .veh-skate { display:block }
#hold:checked ~ .stagewrap .stage,
#hold:checked ~ .stagewrap .stage * { animation-play-state: paused !important }
```



| 需求     | 手段                                |
| :------- | :---------------------------------- |
| 互斥切换 | `type="radio"` + 相同 `name`        |
| 开关量   | `type="checkbox"`                   |
| 视觉按钮 | `<label for="xxx">`，样式完全自定义 |

`.vh` 类把真实控件缩成 1×1 px 并透明化，但保留键盘可聚焦性（配合 `:focus-visible` 给控制台描边）。

------

### 2. 自适应舞台：容器查询 + 单位变量

舞台保持 5:3 比例：

css

```
.stage{
  --u:1px;                 /* 回退值 */
  aspect-ratio:5/3;
  width:100%;
  overflow:hidden;
}
@supports (width:1cqw){ .stage{ --u:.1cqw } }
```



设计稿按 **1000 × 600 单位**绘制，所有尺寸都写成 `calc(N * var(--u))`：

css

```
.wheel{ width:calc(96*var(--u)); height:calc(96*var(--u)) }
.rig  { left:calc(460*var(--u)); top:calc(482*var(--u)) }
```



在支持容器查询单位的浏览器里，`1cqw = 舞台宽度的 1%`，于是 `--u = 舞台宽度的 0.1%`，**整个场景随容器等比缩放**——不依赖视口宽度，也不写一条媒体查询。旧浏览器则退回固定像素设计稿。

技术手册里的 4 张演示卡片也各自是 `container-type:inline-size`，用不同的 `--u` 系数（`.42cqw / .3cqw / .55cqw`）把同一套零件缩进卡片里复用。

------

### 3. 天色系统：变量驱动的交叉淡入

天空、海面各有三份叠在一起，用不透明度变量互斥显示：

css

```
.sky.day  { opacity: var(--oDay) }
.sky.dusk { opacity: var(--oDusk) }
.sky.night{ opacity: var(--oNight) }
```



切换主题时，改的是 `.stage` 上的一整组自定义属性——太阳位置/大小/颜色、云的配色、沙滩、人行道、马路、剪影、灌木、路灯发光、星星月亮透明度……

css

```
#th-night:checked ~ .stagewrap .stage{
  --oNight:1; --starsO:1; --moonO:1; --sunO:0; --rayO:0;
  --sand:#5b5470; --road:#2b2836; --silh:#191430; --lampO:1;
}
```



由于这些变量被几十个元素共享，**一次勾选 = 全场景换装**。所有相关属性都带 `transition`，于是天色是平滑过渡而非硬切。

------

### 4. 速度系统：一个 `--spd` 驱动全部节拍

css

```
#sp-stroll:checked ~ .stagewrap .stage{ --spd:.55 }
#sp-rush:checked   ~ .stagewrap .stage{ --spd:1.75 }

.stage{
  --wheel: calc(1.12s / var(--spd));   /* 车轮 */
  --pedal: calc(2.10s / var(--spd));   /* 踩踏一圈 */
  --belt : calc(8.60s / var(--spd));   /* 中景传送带 */
  --fgT  : calc(1.45s / var(--spd));   /* 前景草丛 */
  --dash : calc(0.35s / var(--spd));   /* 车道虚线 */
}
```



云、海浪、船、飞鸟的 `animation-duration` 也都除以 `--spd`。于是「散步 / 巡航 / 冲刺」只需改一个数，**整个世界同步加速**，且各层速度比例恒定。

冲刺时还会浮出三道速度线——用算术代替条件判断：

css

```
.zip{ opacity: calc((var(--spd) - 1.3) * 1.3); }
```



低于阈值时表达式为负，`opacity` 被自动钳到 0，速度线隐形。

------

### 5. 自行车：全是 border 和渐变

| 部件 | 实现                                                         |
| :--- | :----------------------------------------------------------- |
| 轮胎 | `border: 7u solid #2c2a35` + `border-radius:50%`             |
| 辐条 | `repeating-conic-gradient(from 0deg, #cfd3dc 0deg 2.4deg, transparent 2.4deg 45deg)` |
| 花鼓 | `::after` 一个小圆                                           |
| 齿盘 | 虚线边框圆环 + `::after` 的 `repeating` 虚线环               |

css

```
@keyframes kSpin{ to{ transform:rotate(360deg) } }
.wheel{ animation:kSpin var(--wheel) linear infinite }
```



车架的各根管件（上管、下管、头管、前叉、后上叉、后下叉、座管……）都是同一个 `.bar` 元素，靠 `width + rotate` 拼出三角结构：

css

```
.bar{ height:calc(5*var(--u)); transform-origin:0 50%; background:#1f9d8c }
.downtube{ width:calc(77*var(--u)); transform:rotate(-35.4deg) }
.seatstay{ width:calc(94*var(--u)); transform:rotate(-43.3deg) }
```



车铃、车筐、两条鱼、挡泥板同理，全靠 `clip-path`、渐变和伪元素堆出来。

------

### 6. 两条腿：余弦定理解出的 12 帧骨骼

这是整个页面最「硬核」的部分。

大腿 / 小腿 / 脚掌是三个嵌套的盒子，各自以一端为 `transform-origin`：

html

```
<div class="leg near">
  <div class="thigh"><div class="shin"><div class="foot"></div></div></div>
</div>
```



每一帧先由曲柄角确定踏板坐标，再用**余弦定理**反解大腿与小腿的转角，共取 12 帧（每帧 8.33%）写进关键帧：

css

```
@keyframes kThigh{
  0%    { transform:rotate(-5.1deg) }
  8.33% { transform:rotate(-8.4deg) }
  16.67%{ transform:rotate( 1.5deg) }
  25%   { transform:rotate(17.8deg) }
  ...
  100%  { transform:rotate(-5.1deg) }
}
```



脚掌另外跑一组**反向关键帧**（`kFoot`），让脚底始终大致保持水平，不会跟着小腿乱翻。远侧那条腿只需要一个负延迟：

css

```
.leg.far :is(.thigh,.shin,.foot){ animation-delay:calc(var(--pedal) / -2) }
```



#### 踏板也要保持水平

曲柄在转，但踏板面必须始终水平。做法是「外层跟着转、内层反向转」，两段旋转正好抵消：

css

```
.pwrap.pn{ transform:rotate(90deg) }          /* 挂点随曲柄 */
.pn .pedal{ animation:kPedalA var(--pedal) linear infinite }
@keyframes kPedalA{ from{transform:rotate(90deg)} to{transform:rotate(-270deg)} }
```



#### 换成滑板 / 电动车时怎么办？

不需要重写骨骼——只要**关掉关键帧、改成静态站姿角度**：

css

```
.veh-skate .leg :is(.thigh,.shin,.foot){ animation:none }
.veh-skate .leg.ln .thigh{ transform:rotate(73.6deg) }
.veh-skate .leg.ln .shin { transform:rotate(1.5deg) }
```



同时 `.rider` 整体微调平移，让鸟身对齐新的踏板高度：

css

```
#vh-skate:checked   ~ .stagewrap .rider{ transform:translate(calc(26*var(--u)),calc(18*var(--u))) }
#vh-escooter:checked~ .stagewrap .rider{ transform:translate(calc(18*var(--u)),calc(14*var(--u))) }
```



------

### 7. 三层视差：传送带 + 复制粘贴

「前进」的错觉来自**多层速度不同的无限滚动**：

| 层   | 内容                         | 单周期位移    | 相对速度 |
| :--- | :--------------------------- | :------------ | :------- |
| 远景 | 云、船、飞鸟                 | 1080u → -260u | 最慢     |
| 中景 | 路灯、长椅、站牌、浮标、礁石 | -1000u        | 中速     |
| 前景 | 草丛                         | -500u         | 最快     |

无缝循环的诀窍是**每组内容复制两份**，各占一个周期宽度，滚完一整份刚好接上：

html

```
<div class="belt">
  <div class="bgroup">…9 个道具…</div>
  <div class="bgroup" aria-hidden="true">…同样 9 个道具…</div>
</div>
```



css

```
@keyframes kBelt{ to{ transform:translateX(calc(-1000*var(--u))) } }
.bgroup + .bgroup{ left:calc(1000*var(--u)) }
```



车道虚线则不用复制，直接动 `background-position`：

css

```
@keyframes kDash{ to{ background-position:calc(-90*var(--u)) 0 } }
```



海浪是四条不同速度、不同透明度、带虚线渐变的横条在反向平移；太阳下方的海面波光则用 `repeating-linear-gradient` + `radial-gradient` 遮罩做出来，并随 `--sunX` 一起左右移动。

------

### 8. 天气：雨、水洼、闪电

雨天不改结构，只叠几样东西：

1. **压暗层** `.storm`——一层半透明渐变，`opacity:var(--stormO)`

2. **雨丝**——用两个 `radial-gradient` 当「雨滴形状」平铺成背景，滚动 `background-position`：

   css

   ```
   @keyframes kRain { to{ background-position:0 calc(320*var(--u)) } }
   ```

   

   两层雨（`.r1` / `.r2`）速度与透明度不同，形成景深。

3. **水洼涟漪**——椭圆容器 + `::after` 圆环做扩散淡出：

   css

   ```
   @keyframes kRip{ from{transform:scale(.25);opacity:.9} to{transform:scale(1);opacity:0} }
   ```

   

4. **闪电**——7 秒长循环里只闪三下（87% / 88% / 89%），其余时间 `opacity:0`：

   css

   ```
   @keyframes kFlash{ 0%,86%,90%,100%{opacity:0} 87%,89%{opacity:.5} 88%{opacity:.12} }
   ```

   

同时雨天会把太阳调暗（`--sunO:.3`）、关掉波光（`--glitO:0`）、把云染灰。切换仍然只是变量。

------

### 9. 三只鸟：共享零件 + 覆写

鹈鹕、鹦鹉、猫头鹰共用同一套 DOM 骨架（`.tail / .body / .wing / .neckgrp / .neck / .head / .beak / .eye / .lid`），差异全靠 CSS 覆写：

css

```
.bird-parrot .body{
  background:
    radial-gradient(58% 52% at 66% 64%, #ffd257 0 46%, transparent 47%),
    radial-gradient(46% 42% at 26% 26%, #2aa5a0 0 42%, transparent 43%),
    linear-gradient(150deg,#e8503a,#b83c28);
}
```



切换逻辑是「先全隐藏，再显示被选中的那只」：

css

```
.bird-parrot, .bird-owl{ display:none }
#bd-owl:checked ~ .stagewrap .bird-pelican{ display:none }
#bd-owl:checked ~ .stagewrap .bird-owl    { display:block }
```



微表情同样是纯关键帧：

css

```
@keyframes kBlink{ 0%,91%,100%{transform:scaleY(0)} 94%,96.5%{transform:scaleY(1)} }
.lid     { animation:kBlink 4.6s infinite }               /* 眨眼 */
.pouch   { animation:kPouch 2.6s ease-in-out infinite alternate } /* 喉囊晃动 */
.beak    { animation:kChomp 2.1s ease-in-out infinite }   /* 喙轻微开合 */
.neckgrp { animation:kBob calc(var(--pedal)/2) ease-in-out infinite alternate }
```



注意 `kBob` 的周期是 `--pedal/2`——**鸟的点头和踩踏是同一套节拍**。

------

### 10. 彩蛋：纯 CSS 的「点 14 次」

#### 计数

鹈鹕身上叠了 **14 层完全透明、尺寸相同的 label**，每层对应一个 checkbox：

html

```
<label class="clk c1" for="e1"></label> ... <label class="clk c14" for="e14"></label>
```



初始只有 `.c1` 可点，其余 `pointer-events:none`：

css

```
.clk{ pointer-events:none }
.clk.c1{ pointer-events:auto }
#e1:checked ~ .stagewrap .c1{ pointer-events:none }
#e1:checked ~ .stagewrap .c2{ pointer-events:auto }
#e2:checked ~ .stagewrap .c2{ pointer-events:none }
#e2:checked ~ .stagewrap .c3{ pointer-events:auto }
/* …一路链到 e14… */
```



于是「必须点满 14 次」被编码成了一条**状态链**——想直接点最后一层是点不到的。

#### 反馈

- 右上角的进度点阵：`#e1:checked ~ .stagewrap .eggprog{opacity:1}`，第 N 个点高亮。

- 点击瞬间用 `:active` 给鸟一个 squash：

  css

  ```
  .clk:active ~ .rig .rider{ scale:.97 .95 }
  ```

  

#### 触发

第 14 个 checkbox 亮起后，神秘按钮出现：

css

```
#e14:checked ~ .stagewrap .eggbtn{ opacity:1; scale:1; pointer-events:auto }
```



点击它勾选 `#egg`，触发 7.5 秒白幕过场，中段全白时完成场景替换：

css

```
#egg:checked ~ .stagewrap .whiteout{ animation:kWhite 7.5s ease both }
#egg:checked ~ .stagewrap :is(.veh-bike,.veh-skate,.veh-escooter,.bird-pelican,...){ display:none }
#egg:checked ~ .stagewrap .invert{ display:block }
```



#### 世界线反转

反转场景里，鹈鹕被放大 1.55 倍，一辆缩小 0.8 倍、歪 7° 的迷你自行车放在它背上，整体加一个上下弹跳：

css

```
@keyframes kHop{ from{transform:translateY(0)} to{transform:translateY(calc(-7*var(--u)))} }
```



右下角出现「↩ 回到原世界线」按钮，取消勾选即可复原。

> 彩蛋只在「鹈鹕 × 自行车」组合下生效，其它组合会把所有 `.clk` 一刀切成 `pointer-events:none`。

------

### 11. 无障碍与性能

**无障碍**

- 隐藏控件保留在 tab 序列里，`:focus-visible` 会在控制台上画出虚线焦点框。

- 舞台用 `<figure aria-label="…">`，装饰性副本标了 `aria-hidden="true"`。

- 全站尊重系统设置：

  css

  ```
  @media (prefers-reduced-motion: reduce){
    *,*::before,*::after{ animation:none !important }
  }
  ```

  

**性能**

- 所有动画只碰 `transform` / `opacity`（以及少量 `background-position`），不触发重排。
- 多层视差通过「复制两份 + 位移一个周期」实现，没有 DOM 增删。
- 场景是单个 `.stage` 的子树，`overflow:hidden` 把绘制范围钉死在舞台内。
- 无网络图片请求，无字体图标，无脚本解析开销。

**滚动叙事**（渐进增强）

css

```
@supports (animation-timeline: view()){
  .reveal{ animation:rise .8s both; animation-timeline:view(); animation-range:entry 5% entry 42% }
}
```



不支持滚动驱动动画的浏览器直接忽略，内容照常显示。

------

## 文件结构

text

```
20260911_v1.2.html        # 单文件页面（HTML + CSS 内联，无 JS）
README.md                 # 本文件
```



------

## 设计取值速查

| 变量                                 | 默认值        | 作用                            |
| :----------------------------------- | :------------ | :------------------------------ |
| `--u`                                | `.1cqw`       | 场景缩放单位（1u = 设计稿 1px） |
| `--spd`                              | `1`           | 全局速度倍率                    |
| `--pedal`                            | `2.1s / spd`  | 踩踏一圈                        |
| `--wheel`                            | `1.12s / spd` | 车轮一圈                        |
| `--belt`                             | `8.6s / spd`  | 中景传送带周期                  |
| `--fgT`                              | `1.45s / spd` | 前景草丛周期                    |
| `--dash`                             | `0.35s / spd` | 车道虚线周期                    |
| `--sunX` / `--sunY` / `--sunS`       | 随主题        | 太阳位置与大小                  |
| `--oDay` / `--oDusk` / `--oNight`    | `0 / 1 / 0`   | 三套天色叠加权重                |
| `--lampO`                            | `0`           | 路灯发光（夜晚为 1）            |
| `--rainO` / `--stormO` / `--puddleO` | `0`           | 雨天三件套                      |

------

## 已知取舍

- **单位依赖容器查询**：不支持 `cqw` 时退化为固定 1000px 设计稿，小屏上会偏大。
- **腿部是离线手算的 12 帧关键帧**，不是运行时 IK；改变曲柄几何需要重算角度表。
- **彩蛋计数器单调递增**：一旦点到第 N 层，前面的层级无法再从界面点回去（可用键盘操作 checkbox）。
- **强依赖 DOM 顺序**：大量使用通用兄弟选择器 `~`，隐藏 `input` 必须严格位于 `.stagewrap` 之前，调整结构会破坏所有状态联动。
- **字体需联网**：Google Fonts 加载失败时回退系统字体，版式略有差异。

------

## 技术栈

| 项目 | 说明                                                         |
| :--- | :----------------------------------------------------------- |
| 标记 | HTML5（语义化 `figure` / `figcaption` / `label`）            |
| 样式 | CSS3：自定义属性 · 容器查询 · 关键帧 · 渐变 · `clip-path` · 兄弟选择器 · `@supports` |
| 脚本 | **无**                                                       |
| 图片 | **无**（全为 CSS 绘制）                                      |
| 字体 | 站酷快乐体（标题）× 思源黑体（正文）                         |

------

本网页由Qwen3.8-Max编写
