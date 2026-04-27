# 参考模板与示例

## A. PRD 需求映射表示例

```markdown
| 需求ID | PRD原文摘要 | 原型实现模块 | 页面/路由 | 状态 |
|---|---|---|---|---|
| R01 | 用户可浏览产品列表 | 列表页 + ProductStore | /products | 已实现 |
| R02 | 用户可查看产品详情 | 详情页 + 详情卡片组件 | /products/:id | 已实现 |
| R03 | 用户可加入购物车 | 购物车状态管理 + 按钮交互 | /products, /cart | 已实现 |
| R04 | 用户可提交订单 | 提交流程页 + 表单校验 | /checkout | 降级实现 |
```

## B. 原型蓝图输出示例

```markdown
## 原型蓝图
- 路由：
  - /dashboard 概览页
  - /products 列表页
  - /products/:id 详情页
  - /checkout 提交流程页
- 页面：
  - DashboardPage
  - ProductListPage
  - ProductDetailPage
  - CheckoutPage
- 核心组件：
  - ProductCard
  - FilterPanel
  - CartSummary
  - CheckoutForm
- Pinia Store：
  - useProductStore
  - useCartStore
  - useCheckoutStore
- Mock 数据：
  - products.mock.js
  - user.mock.js
  - orders.mock.js
```

## C. 交付说明模板

```markdown
## 原型交付结果

### 1) 运行方式
- Node 版本：18+
- 安装：`npm install`
- 启动：`npm run dev`

### 2) 目录结构（简版）
src/
  pages/
  components/
  stores/
  mock/
  router/

### 3) 需求映射结果
| 需求ID | 实现说明 | 代码位置 | 状态 |
|---|---|---|---|
| R01 | 产品列表支持搜索和分页（前端模拟） | src/pages/ProductListPage.vue | 已实现 |

### 4) 未完成项
- R09：PRD 未给出字段定义，待确认后补齐

### 5) 演示路径
- 进入 `/products`
- 选择任一产品进入详情
- 加入购物车并前往 `/checkout`
- 提交后展示成功提示（Mock）
```

## D. PRD 缺口提问模板

当 PRD 信息不足，先用最小问题补齐：

```markdown
为保证原型可运行，请确认以下 3 点：
1. 关键实体字段：例如“订单”是否至少包含（id、状态、金额、创建时间）？
2. 关键流程分支：提交失败后是否需要“重试/取消”分支？
3. 验收口径：演示时以“页面可走通”还是“规则正确”作为通过标准？
```

## E. Mock CRUD 演示模板

```markdown
## CRUD 演示路径（以商品实体为例）

### 1) Create（新增）
- 入口：`/products` -> “新增商品”按钮
- 操作：填写名称、价格、库存 -> 提交
- 预期：列表出现新记录，提示“新增成功”

### 2) Read（查询）
- 列表查询：按关键词筛选
- 详情查询：点击行进入 `/products/:id`
- 预期：列表与详情字段一致

### 3) Update（修改）
- 入口：详情页或列表行“编辑”
- 操作：修改价格/库存 -> 保存
- 预期：返回列表后数据已更新，刷新页面仍可见（来自内存态 store/mock）

### 4) Delete（删除）
- 入口：列表行“删除”
- 操作：二次确认后删除
- 预期：列表移除该记录，提示“删除成功”
```

```markdown
## Mock Repo 接口约定（建议）
- `list(params)`：返回分页或全量列表
- `get(id)`：返回单条详情
- `create(payload)`：新增并返回新对象
- `update(id, payload)`：更新并返回对象
- `remove(id)`：删除并返回成功标记
```

## F. SenseCare PRD 解析映射模板

（`SenseCare-product-master` 技能产出的标准 PRD 与下列结构一一对应。）

```markdown
## SenseCare PRD 结构化拆解

### 输入章节识别（SenseCare 标准结构）
- 1. 项目背景：提取业务目标与成功口径，写入原型 README
- 2. 业务流程简述：提取主流程节点（用于路由顺序与导航主线）
- 3. 需求总览：直接复用 `R1/R2…` 编号、名称、类型、优先级作为映射表主键
- 4. 详细功能需求说明：作为核心实现输入
  - 模块标题下“用户故事”：演示主线、角色入口
  - 4.x.1 功能说明：位置 → 路由；目标 → 演示说明；输入输出 → 表单/Mock 字段
  - 4.x.2 业务流程说明：内嵌 Mermaid → Pinia 状态机与 actions
  - 4.x.3 界面说明（A/D 规范）：列表列、表单项、文案、空态、截断
  - 4.x.4 交互说明（B/C/F 规范）：按钮六步法、防抖/超时常量、表单校验时机
  - 4.x.5 异常处理与边界（E 规范）：降级、并发抢占、合规拦截、系统级中断
  - 4.x.6 产品上下文说明（可选）：模块归属、关联影响、明确不影响

### 模块到代码映射规则
- `4.x` -> `src/pages/<Module>Page.vue` + `src/router/index.js` 路由项（路径取自 4.x.1 的“位置”）
- 模块标题“用户故事” -> 演示路径与角色登录态默认值
- `4.x.1` 位置 -> 路由 path / 嵌套菜单层级
- `4.x.1` 目标/输入输出/关键规则 -> 页面 README、表单 schema、Mock 初始数据
- `4.x.2` Mermaid（stateDiagram-v2/sequenceDiagram/flowchart）-> `src/stores/<domain>.store.js` 的 state 与 actions（中文状态名映射稳定 key，注释保留原名）
- `4.x.3` -> 视图组件结构、列表列定义、空态组件、文案常量（双引号文案 1:1）
- `4.x.4` -> 按钮 disabled 条件 + loading 态 + 防抖时长、表单校验规则（数字常量统一放 `src/constants/`）
- `4.x.5` -> 异常分支组件（弱网提示、超时切人工、合规拦截弹窗、只读态）
- `4.x.6` -> 模块归属决定挂载壳子；“明确不影响”作为反向白名单约束实现范围
```

```markdown
## SenseCare 模式需求映射表（推荐）
| 需求ID | PRD定位 | 用户故事角色 | 原文摘要 | 页面/路由 | 组件 | Store/Action | Mock数据 | 关键常量 | 状态 |
|---|---|---|---|---|---|---|---|---|---|
| R1 | 4.1 | 患者 | 智能导诊会话主流程 | /triage | TriageChatPanel | useTriageStore/submitStep | triage.repo.js | DEBOUNCE_NEXT=800ms, MODEL_TIMEOUT=10s | 已实现 |
| R1 | 4.1.3 | 患者 | 导诊入口按钮 + 首屏提示卡片 | /triage | TriageEntryCard | useTriageStore/init | triage.mock.js | - | 已实现 |
| R1 | 4.1.5 | 患者 | 急危重症拦截 + 弱网降级 | /triage | TriageEmergencyModal, TriageFallbackTip | useTriageStore/handleRiskBlock | triage.repo.js | RETRY_MAX=3 | 已实现 |
```

```markdown
## Mermaid 状态映射示例（4.x.2 → Pinia store）

PRD 4.1.2 状态机：
- 待输入态 / 分析中态 / 风险中断态 / 异常兜底态 / 结果推荐态

对应 store 设计：

```js
// src/stores/triage.store.js
export const useTriageStore = defineStore('triage', {
  state: () => ({
    status: 'idle',
  }),
  actions: {
    submitStep() {  },
    handleRiskBlock() {  },
    handleFallback() {  },
    showResult() {  },
  },
})
```
```
