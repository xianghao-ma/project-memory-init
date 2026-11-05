# project-memory-init

为 Codex 项目建立一套可持续维护的长期记忆：记录关键决定、当前进展和产出结果，将详细报告集中到 `docs/reports/`，并按日期与目标归档结果图。

适用于新项目初始化，也可为已有项目补齐结构、整理已授权迁移的报告。默认正文中文，目录及文件名英文。

## 项目结构

```text
项目/
├── AGENTS.md                         # 项目规则与记忆读取入口
└── docs/
    ├── decisions.md                  # 关键决定、原因与来源
    ├── status.md                     # 当前进展、问题与下一步
    ├── results.md                    # 结果摘要、验证情况与索引
    ├── reports/                      # 详细报告统一放在这里
    │   └── 专题报告.md
    ├── figures/                      # 结果图归档
    │   ├── YYYY-MM-DD_goal-a/
    │   │   ├── README.md             # 目标、配置、图解、结论与局限
    │   │   └── figure-01.png
    │   └── YYYY-MM-DD_goal-b/
    │       ├── README.md
    │       └── figure-01.png
    └── history/                      # 可选：保留既有历史记忆档案
```

初始化时没有成果就不创建示例报告或日期目录。`history/` 仅在已有或确需归档时保留或建立。

### 文档归类

| 内容 | 位置 |
|---|---|
| 项目约定、工作入口及维护规则 | `AGENTS.md` |
| 为什么做出某个决定 | `docs/decisions.md` |
| 项目做到哪里、下一步做什么 | `docs/status.md` |
| 得到了什么结果、证据在哪里 | `docs/results.md` |
| 调研、技术说明、实验分析、性能测试、审计等详细报告 | `docs/reports/` |
| 某组图片的解释与来源 | 对应图片文件夹内的 `README.md` |

根目录 README、AGENTS、skill 文档和实验原始说明不属于全仓库 Markdown 搬迁对象。已有 `figures/` 和 `history/` 保持各自用途。

## 安装

本仓库为私有仓库，安装环境需有相应 GitHub 访问权限。以下命令使用 SSH，需先配置 GitHub SSH 认证：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone git@github.com:xianghao-ma/project-memory-init.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/project-memory-init"
```

也可以下载仓库，将整个目录放入上述 skills 目录，确保 `project-memory-init/SKILL.md` 位于正确位置。已有同名目录时先检查其内容，不直接覆盖。不同主机需分别安装。

## 使用

在目标项目的 Codex 聊天中调用：

```text
使用 $project-memory-init 初始化当前项目的长期记忆和文档结构。
```

为已有项目补录关键历史：

```text
使用 $project-memory-init 为当前项目补齐长期记忆，结合可访问的历史聊天和
现有文件整理关键决定、当前状态与代表性结果，保留已有内容。
```

明确要求整理旧报告时：

```text
使用 $project-memory-init 整理当前项目 docs：三份长期记忆文件保留在顶层，
其余专题报告移入 reports，并更新受影响的引用；保留 figures 和 history。
```

没有明确项目上下文时，请指定目标项目路径。仅要求初始化不会自动迁移旧报告；迁移需要在请求中说明。

## 维护与归档规则

- 开始工作先读取 `AGENTS.md` 和 `status.md`，按需查阅决定、结果和原始证据。
- 有重要决定、进展变化或新结果时更新相关文档；无实质变化不增加流水账。
- 区分用户决定、已核实事实、历史报告与待验证假设。重要疑义交由用户决定。
- 结果图按北京时间（`Asia/Shanghai`）的产出日期和英文短目标名分组。同日不同目标分别建目录，跨日产出新建对应日期目录。
- 历史产出日期无法核实时使用归档日，并注明原日期未知；不单凭文件修改时间推断产出日期。
- 每组图都有说明文档和结果索引入口。复制代表图时保留原件，用 SHA256 核对；不同内容保留版本，相同内容避免重复收录。
- FITS、大型采样链等留在原处，通过文档链接追溯。报告迁移保留未提交内容，并检查没有新增失效链接。

## 能力边界

这是由 Codex 执行的文档工作流，**不是创建 Project 时自动触发的后台服务**。安装后可显式调用，也允许 Codex 按匹配的任务请求选择使用；它不会仅因新建了 Project 就自动配置文件。

长期记忆保存提炼后的项目知识，不是完整聊天备份，也不能恢复不可访问或已删除的聊天。初始化不会自动运行科研计算、操作作业、提交 Git 或创建自动化。

## 仓库内容

- [SKILL.md](SKILL.md)：触发范围、初始化流程、报告迁移及验收要求。
- [agents/openai.yaml](agents/openai.yaml)：skill 显示名称和默认调用提示。
- [assets/AGENTS.memory.md](assets/AGENTS.memory.md)：合并到项目 AGENTS.md 的可复用维护条款。
