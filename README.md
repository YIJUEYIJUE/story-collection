# 故事收集册 · 使用说明

## 目录结构

```
/home/z/my-project/stories/
├── data.json      # 故事数据库（持久化，不丢）
├── index.html     # 可浏览的网页（数据已内联，双击即可打开）
└── README.md      # 本说明
```

## 工作流

### 用户视角
1. 用户把故事发给我（直接贴文字、发文件、发链接均可）
2. 我负责：
   - 通读全文，理解主题和情绪
   - 自动归类到 15 个分类之一（情感/成长/亲情/爱情/友情/生活/励志/哲理/童年/奇幻/悬疑/旅途/职场/时代/其他）
   - 自动打 2-5 个细粒度标签
   - 写入 data.json + 重新生成 index.html（数据内联）
   - 回复确认：编号、分类、标签
3. 用户可以随时让我把最新版网页发过去查看

### 分类说明（15 类）
| ID | 名称 | 颜色 | 用途 |
|---|---|---|---|
| emotion  | 情感 | 粉 | 通用情绪类、复杂心境 |
| growth   | 成长 | 绿 | 成长觉醒、自我认知 |
| family   | 亲情 | 橙黄 | 父母子女、家庭关系 |
| love     | 爱情 | 红 | 恋爱、婚姻 |
| friend   | 友情 | 蓝 | 朋友、同窗 |
| life     | 生活 | 青绿 | 日常、烟火气 |
| inspire  | 励志 | 橙 | 奋斗、逆袭 |
| philosophy | 哲理 | 紫 | 哲思、寓言 |
| childhood | 童年 | 金黄 | 童年回忆 |
| fantasy  | 奇幻 | 靛蓝 | 虚构、奇幻 |
| mystery  | 悬疑 | 深灰 | 悬疑、推理 |
| travel   | 旅途 | 青蓝 | 旅行、远方 |
| workplace | 职场 | 天蓝 | 工作、职业 |
| war      | 时代 | 灰 | 时代叙事、历史背景 |
| other    | 其他 | 浅灰 | 兜底 |

### 标签规则
- 数量：2-5 个
- 风格：细粒度情绪或元素（如 `#治愈` `#遗憾` `#反转` `#金句`）
- 自动从故事内容中提炼

## 每次新增故事的流程（内部 SOP）

1. 读取 `/home/z/my-project/stories/data.json`
2. 生成新 ID：`st-001`, `st-002`, ... 递增
3. 填充字段：
   - id / title / content / category / tags / source / collected_at(YYYY-MM-DD) / note
4. push 到 stories 数组末尾
5. 重算 stats.total / by_category / by_tag
6. 更新 updated 字段
7. 用新 data.json 重新生成 index.html（把 `STORY_DATA = ` 那一段替换）
8. 在回复里告诉用户：编号、分类、标签 → 让用户确认是否需要调整

## 质量守则
- 一篇不漏：用户发过的每一段故事文字都必须入库
- 原汁原味：故事正文 100% 保留，不做改写
- 分类可调：用户觉得分得不对，随时改 category / tags，重新生成网页
- 备份：data.json 是唯一真源；index.html 可随时从 data.json 重建

## 技术注记
- 网页自包含，数据内联在 `<script>` 的 `STORY_DATA` 变量里，避免 CORS 问题，双击即可打开
- 字体优先 LXGW WenKai（已安装），其次 Noto Serif SC，回退到系统中文
- 移动端响应式，侧栏在窄屏会自动折叠到顶部
