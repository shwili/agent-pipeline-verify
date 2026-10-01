# agent-pipeline-verify · 多代理流水线与验收协议

> 一个 agent 干大活容易翻车（自己写自己验＝橡皮图章），多代理并行又容易打架（同文件冲突、任务重叠、互相覆盖）。
> 本 skill 把「**子代理流水线 + 独立验收**」沉淀为一套可执行协议。

Running batches through subagents is powerful but risky: agents edit the same file, tasks overlap, and self-verification becomes a rubber stamp. This skill formalizes role separation (builder != verifier), pre-dispatch de-confliction, tiered pipelines by risk, layered verification, and mandatory fix-reverify-release loops.

## 它回答三个问题

| 问题 | 方案 |
|---|---|
| **批次怎么切（不打架）** | 交集去重（一物一拍）＋ 单写者（同文件同区域只给一个写者；并行靠"副本＋重放合并"，三重判据：忠实性/重放性/组合性） |
| **代理怎么派（不糊弄）** | 角色分离（干活的≠验活的≠发布的）＋ 提示词四纪律（四要件自足／数字来源／临时件纪律／落盘回执） |
| **验收怎么收（不失控）** | 分层验收（全量探针归验收代理；调度方抓证据链与裁决）＋ 「与自验差异清单」强制节 ＋ 发现即闭环（返工→定向复验→放行） |

## 核心内容

- **第一原则**：角色分离——实施代理自验＝第一层 QA（必要不充分），独立验收代理（≠实施）＝第二层 QA
- **关卡分级（A/B/C 三档）**：大规模/高风险走全链（侦察→实施→独立验收→合并复核→发布→发布后复核）；单点微修走短链——**分级不是降标准，是不浪费**
- **派单前两查**：交集去重 / 单写者（附真实事故教训：任务重叠→双份实现→静默覆盖）
- **提示词四纪律**：四要件自足、数字来源、临时件纪律单列、落盘回执（防"空完成"）
- **证据纪律**：双证据制（声明出处＋实现出处）、计数断言用"恰 N"、固定种子、行为验证 ≠ 日志出现
- **断点恢复**：通信中断用 resume 续跑；故障断流走"盘点现场→断点续跑/承前确认"；长任务代理"结段回报"
- **反模式清单**：11 条踩过的坑与对策
- **落地检查清单**：每批照抄

完整方法详见 [SKILL.md](./SKILL.md)。

## 安装

**方式一：SkillHub（社区源）**

```bash
skillhub install agent-pipeline-verify --dir ~/.workbuddy/skills
```

**方式二：手动安装**

把 `SKILL.md` 放入目标平台的 skills 目录，例如：

```
~/.workbuddy/skills/agent-pipeline-verify/SKILL.md
```

**方式三：当方法论阅读**

协议逻辑层与工具无关——即使不用任何 agent 平台，`SKILL.md` 也可以直接作为"多代理协作流程规范"参考使用。

## 适合谁

- 用子代理/多代理并行跑大工程的开发者与团队
- 需要"独立验收"保证质量、防止自验橡皮图章的自动化工作流
- 任何具备「子代理 / 隔离工作区 / 异步通知」能力的 agent 平台用户

## 来源

源自一项大型工程（30+ 子代理、数十批次：全量检查 → 多批修复 → 合并重放 → 独立复核 → 发布）的实战教训沉淀。

## License

[MIT](./LICENSE)
