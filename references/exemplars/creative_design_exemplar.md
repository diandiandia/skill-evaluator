# 官方顶级标杆 1：创意与生成类 (Creative & Generative)
> **对标来源**：Claude 官方 `algorithmic-art` 与 `canvas-design`
> **核心启示**：拔高天花板、双阶段结构（哲学先行）、概念种子入参数、FIXED/VARIABLE解耦、做乘法不做加法。

---

## 标杆结构骨架与关键实现

```markdown
---
name: algorithmic-art
description: >-
  使用 p5.js 通过种子随机性与物理交互参数创建原创算法艺术流派及其实体作品。
  当用户要求使用代码生成视觉艺术、算法艺术、流场或粒子系统时使用。
  不用于常规的网页 UI 布局绘制或普通静态图表制作；严禁直接抄袭现有商业作品。
---

# Algorithmic Art — 算法艺术生成体系

## 核心设计哲学 (Algorithmic Philosophies)

Algorithmic philosophies are computational aesthetic movements that are then expressed through code.
我们不是在生成一张孤立的“视觉图案”，而是在确立一个**具有自洽数学逻辑的美学流派**。

### 理念与代码映射原则
每个算法流派必须具备以下维度的系统性表达，而非零散调参：
1. **数学关系与计算过程**：严密的几何规律、向量场方程；
2. **噪声函数与随机模式**：多层 Perlin/Simplex 噪声，区分宏观趋势与微观扰动；
3. **粒子行为与动力学**：质量、阻尼、吸引力、斥力与生命周期；
4. **时间演化与状态涌现**：系统如何随时间从微小扰动涌现出宏观秩序。

---

## 阶段工作流 (Two-Phase Workflow)

### Phase 1: 算法哲学确立 (Algorithmic Philosophy Creation)
在动手写一行代码之前，必须先输出独立的概念与规范文档：
- **哲学命名**：确立美学主题（如 *“Organic Turbulence / 有机湍流”*、*“Geometric Silence / 几何静默”*）；
- **概念种子 (Concept Seed)**：
  - 将用户的主题视为“隐式概念 DNA”，**严禁把文字直接印在画面上**；
  - 像爵士乐手借用旋律一样，将概念隐晦地映射为算法物理量（如把“焦虑”映射为高频微振动与高排斥力，把“平静”映射为阻尼收敛）；
- **参数架构设计**：列出驱动该流派的核心物理阈值、衰减率与色彩梯度。

### Phase 2: 代码实现 (P5.js Expression)
基于 Phase 1 确立的规范生成最终的单文件网页作品：

#### STEP 0: 必须先读取模板 (Read Template First)
绝不从零手写 HTML，必须读取 `assets/viewer.html`，严格划分边界：
- **FIXED（固定底线，严禁改动）**：视口响应容器、全屏按钮、Seed 控制面板、FPS 监控组件；
- **VARIABLE（自由发挥变量区）**：核心 p5.js `setup()` 与 `draw()` 算法、参数控制滑块绑定。

#### 核心工艺硬约束 (Craftsmanship Checklist)
- [ ] **确定性复现**：必须使用 `randomSeed(seed)` 与 `noiseSeed(seed)`，相同种子必须完全复现同一画面；
- [ ] **物理量命名**：参数必须以物理量命名（如 `viscosity`、`damping`、`forceThreshold`），严禁使用靠近结果的伪参数；
- [ ] **版面与安全边距**：文字或主要视觉焦点绝不出血，组件之间 zero-overlap（绝对零重叠）；
- [ ] **性能底线**：在 60 FPS 下粒子数量控制在 3000 以内，避免掉帧。

---

## 终审精修守卫：做乘法不做加法 (FINAL STEP Refinement Guard)

> 🛑 **精修阻断令 (STOP Rule)**：
> 当生成完初版代码后，模型的第一本能往往是“再加个特效、再画个星星、再加一层循环”。
> **立刻停止！此时严禁添加任何新元素或新图形！**
> 
> **精修阶段只允许做三件事**：
> 1. 删掉画面中视觉权重冲突的冗余元素；
> 2. 微调已有元素的位置、间距、线条粗细与透明度；
> 3. 增强主要形态与背景的层次对比度。
```
