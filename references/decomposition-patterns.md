# Domain Decomposition Patterns

> Reference for Phase 2 of the domain-distiller methodology.
> Use this when designing the orthogonal decomposition of a new domain.

## The Orthogonality Principle

A good decomposition means each dimension contributes unique information. If two dimensions produce overlapping research results, they weren't truly orthogonal — re-split.

**Test**: Can you write a one-sentence description of what unique knowledge each dimension contributes, without mentioning any other dimension? If the descriptions overlap, rework the split.

## Pattern 1: Context × Action

Best for domains where the user's situation determines the right recommendation.

**Structure**: User context dimensions (who, what stage, what constraints) × Action dimensions (what to do, what to choose)

**Restaurant recommendation example**:
```
Context dimensions:
  - Diner type (单身/情侣/家庭/商务/朋友聚会)
  - Budget level (人均50/100/200/500/1000+)
  - Dietary constraints (忌口/过敏/素食)

Action dimensions:
  - Cuisine type (川菜/粤菜/日料/西餐...)
  - Scene (约会/商务/打卡/随便吃)
  - Location (city/district)
```

**Travel planning example**:
```
Context dimensions:
  - Traveler type (独旅/情侣/家庭/闺蜜/团建)
  - Budget level (穷游/舒适/轻奢/奢华)
  - Season (spring/summer/autumn/winter → 目的地适配)

Action dimensions:
  - Destination type (自然/城市/文化/海岛/雪山)
  - Trip duration (周末/3-5天/7天+/长期)
  - Purpose (放松/冒险/文化/购物/蜜月)
```

## Pattern 2: Rule × Resource

Best for domains with many constraints + many options to choose from.

**Structure**: Constraint/rule dimensions (what you can't/shouldn't do) × Resource/option dimensions (what you can choose from)

**Home renovation example**:
```
Rule dimensions:
  - Regulations & safety (承重墙/水电规范/消防)
  - Room-specific constraints (厨房防水/卫生间通风)
  - Common pitfalls (装修公司套路/材料环保标准)

Resource dimensions:
  - Material catalog (地板/墙面/橱柜/卫浴)
  - Style patterns (现代简约/北欧/日式/工业风)
  - Price bands (经济型/品质型/高端定制)
```

**Legal advice example**:
```
Rule dimensions:
  - Jurisdiction (法律适用地域)
  - Case type constraints (诉讼时效/举证责任)
  - Procedural rules (审理流程/上诉期限)

Resource dimensions:
  - Precedent cases (类似案例判决)
  - Legal remedies (赔偿/禁令/宣告)
  - Service providers (律所类型/费用结构)
```

## Pattern 3: Principle × Practice

Best for domains with theory + application layers.

**Structure**: Theory/principle dimensions × Application/technique dimensions

**Interview preparation example**:
```
Principle dimensions:
  - Evaluation criteria (公司想要什么品质)
  - Question taxonomy (行为题/案例题/技术题)
  - Interviewer psychology (面试官在想什么)

Practice dimensions:
  - Answer frameworks (STAR/金字塔/反向提问)
  - Industry-specific questions (互联网/咨询/金融)
  - Common pitfalls (常见错误答案分析)
```

**Fitness/health example**:
```
Principle dimensions:
  - Physiology basics (增肌/减脂/耐力原理)
  - Nutrition science (宏量营养素/代谢)
  - Recovery & injury prevention

Practice dimensions:
  - Exercise catalog (力量/有氧/柔韧)
  - Diet plans (减脂餐/增肌餐/维持餐)
  - Routine design (新手计划/进阶分化/平台突破)
```

## Pattern 4: Static × Dynamic

Best for domains with stable fundamentals + fast-changing surface.

**Structure**: Stable knowledge dimensions × Time-sensitive dimensions

**Investment/finance example**:
```
Static dimensions:
  - Asset class fundamentals (股票/债券/房产/黄金)
  - Risk management principles (分散/对冲/止损)
  - Behavioral finance biases (过度自信/损失厌恶)

Dynamic dimensions:
  - Current market conditions (指数/利率/板块轮动)
  - Policy changes (监管新规/税收调整)
  - Trending opportunities (热点行业/新兴资产)
```

## Pattern 5: Supply × Demand

Best for matching problems where both sides need independent modeling.

**Structure**: Supply/provider dimensions × Demand/consumer dimensions

**Pet care example**:
```
Supply (pet) dimensions:
  - Breed characteristics (犬种/猫种特性)
  - Life stage needs (幼年/成年/老年)
  - Health & behavior issues

Demand (owner) dimensions:
  - Owner lifestyle (工作时长/居住空间/活动量)
  - Budget (月均花费/医疗储备)
  - Experience level (新手/有经验/专业)
```

## Choosing the Right Pattern

| Domain characteristic | Best pattern |
|----------------------|--------------|
| "What should I choose given my situation?" | Context × Action |
| "What can I do within these constraints?" | Rule × Resource |
| "How do I learn/improve at X?" | Principle × Practice |
| "What's the latest on X?" with stable foundations | Static × Dynamic |
| "Match X to Y" problems | Supply × Demand |

## Common Decomposition Mistakes

1. **Too many dimensions** (>5) — scope creep. Merge related dimensions or split into sub-skills.
2. **Hierarchical instead of orthogonal** — dimensions that are subtypes of each other rather than independent. "Gift types" and "Gift prices" are independent; "Gifts" and "Flower gifts" are not.
3. **Missing the constraint dimension** — every domain has taboos, common mistakes, or things to avoid. This dimension is almost always worth including.
4. **Over-indexing on "things"** — product catalogs and resource lists are useful but not sufficient. Include the decision logic dimension too.
