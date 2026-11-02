# 镜像说明 / Mirror Notice

本仓库是 **[YuJunZhiXue/dsh-purge](https://github.com/YuJunZhiXue/dsh-purge)** 的**全量镜像（mirror）**，
由 [@mmparko](https://github.com/mmparko) 在上游宣布删库前完整备份，用于存档与分发。

---

## 一、署名 / Attribution

| 项 | 内容 |
| --- | --- |
| 原项目 | **dsh-purge — DeepSeek Harness 破甲**（让所有模型都能破甲，不同模型可换不同提示词） |
| 原作者 | **YuJunZhiXue**（[@YuJunZhiXue](https://github.com/YuJunZhiXue)） |
| 原仓库 | <https://github.com/YuJunZhiXue/dsh-purge> |
| 原许可证 | MIT License（本仓库 `LICENSE` 原样保留，未做任何改动） |

**本项目的名称、思路、代码、提示词的一切权利与署名均归原作者。**
本镜像不主张任何原创性，仅承担存档与分发职责，未对原作者内容做任何修改或再授权。

按原 README「[署名要求](https://github.com/YuJunZhiXue/dsh-purge#署名要求)」章节的明确要求：
**借用本项目的名称、思路、代码或提示词，必须署名，并写明来源仓库。** 任何基于本镜像的二开、
分发、集成，都必须保留本说明与原仓库链接。原项目的非盈利条款同样沿用：**不得用于卖课、
卖插件、卖 token、倒卖等收费行为。**

---

## 二、备份内容 / What's included

| 项目 | 内容 |
| --- | --- |
| 分支 | `master`、`fix/restart-sticky` |
| 原版 Tag | 73 个：`v1.1.1` … `v1.1.71`（含各 `-beta.N` 预发布）+ `restore-issue-25` |
| PR 归档 Tag | 26 个：`archive/pr-<N>-head`、`archive/pr-<N>-merge` |
| 上游快照 Tag | `upstream-snapshot-6c1d638` — 备份时刻上游 `master` 的原始 commit |
| Issue/PR 存档 | 分支 `upstream-archive`：`upstream-archive/` 目录下的 JSON 与可读摘要 |
| Issue 规模 | 91 个 issue + 24 个 PR，共 135 条评论 |

> 说明：GitHub 禁止向 `refs/pull/*` 推送（`deny updating a hidden ref`），
> 因此上游的 26 个 PR ref 已转换为同 SHA 的 `archive/pr-*` tag，commit 对象一个不少。

### 相对上游的差异

`master` 比上游 `master` 多两个提交：

1. 本文件 `MIRROR-NOTICE.md`（备份说明，上游原始内容此时零改动）；
2. **`v1.1.72` 下游修复**——上游 `1.1.71` 在 DSH `0.2.1-rc.5` 上跑不起来，本仓库在其基础上做了兼容性修补，
   详见 [第六节](#downstream) 与 `release-notes.md`。

想拿上游原始状态：`git diff upstream-snapshot-6c1d638`。

---

## 三、备份记录 / Capture record

- 备份时间：2026-10-13
- 上游 `master`：`6c1d638d1bdcc45ede50fc30249c753d58122a51`
- 上游 `fix/restart-sticky`：`1f5c2ff6e29346ff1b2b6a4f7b8faa7fa431eac4`
- 最新原版 tag `v1.1.71`：`5e757260a0be055892b48ec520d451cc82e1c191`
- 备份时刻上游星标 **4,995**、fork **612**
- 上游仓库元数据、issues、PR、评论、标签的完整 JSON 见 `upstream-archive` 分支
- 上游 Wiki：未启用（`*.wiki.git` 返回 `Repository not found`），无内容可备份

### 完整性校验结果（备份时刻实跑）

| 校验项 | 结果 |
| --- | --- |
| ref 逐条 SHA 比对 | **101 / 101 完全一致**，0 缺失、0 差异 |
| `master` 源码包 SHA256 | 上游与镜像**逐字节相同**：`4acda024330d43b7beaf220f308e10eb27cf253fd4135942e3e5930b1dace106` |
| 文件级 blob SHA | **121 / 121 完全一致**（Github Trees API recursive 比对） |
| `git fsck --full` | 通过，无损坏、无悬挂对象缺失 |

---

## 四、自行校验 / Verify

```bash
git clone https://github.com/mmparko/dsh-purge.git
cd dsh-purge

# 1. 备份时刻的上游原始状态
git log --oneline -1 upstream-snapshot-6c1d638
#    → 6c1d638 上游 master 原样

# 2. 本镜像与上游原始状态的差异（应只有 MIRROR-NOTICE.md 一个文件）
git diff --stat upstream-snapshot-6c1d638 master

# 3. 分支与 tag 清点
git branch -a            # master / fix/restart-sticky
git tag | wc -l          # 99 = 73 原版 + 26 PR 归档
git tag | grep '^archive/pr-'

# 4. 对照上游快照做一次完整 hash 校验
git rev-parse master^{tree}
git rev-parse upstream-snapshot-6c1d638^{tree}
```

```bash
# 5. 与上游（若仍在线）逐 ref 比对
git ls-remote https://github.com/YuJunZhiXue/dsh-purge.git | sort > /tmp/up.txt
git ls-remote https://github.com/mmparko/dsh-purge.git | sort > /tmp/mine.txt
diff /tmp/up.txt /tmp/mine.txt
```

---

## 五、上游 README 中的原生状态说明（保留告知）

上游 README 在备份时载明：**项目暂停更新**，作者因工作安排暂停维护、不再发版、暂不收
issue / PR，也不保证跟进新版 dsh；仓库仍可自用。该状态与「违规商用公示」章节一并完整保留在
`README.md` / `README.zh-CN.md` 中，本镜像不修改其任何字句。

---

<a id="downstream"></a>
## 六、下游修复：v1.1.72（本仓库新增）/ Downstream fixes

上游最后一次发版是 `1.1.71`（`dshTarget: 0.2.0-rc.2`）。DSH 升到 `0.2.1-rc.5` 后它有三个硬故障，
本仓库在其基础上修好，发为 `1.1.72`：

| 故障 | 现象 | 原因 | 修法 |
| --- | --- | --- | --- |
| 提示词渲染失败 | 发消息直接报 `unknown prompt variable "{{cwd}}"`，一条都发不出去 | 0.2.1 起提示词变量只注册 `provider` / `model` | persona suffix 不再写 `{{cwd}}`，并把 `cwd` 移出插值白名单 |
| 宿主 exit 1 | 解包修补后进程直接退出 | 同步函数里 fire-and-forget 的异步 `atomicCopyFile`，rejection 无人接管 | 改成同步 `copyFileSync` |
| 备份全失败 | 82 个补丁写进宿主，一份 `.bak` 都没有，回滚无从恢复 | `hostFs` 没转发 `closeSync`，占位 fd 悬空，Windows 上 `rename` 覆盖 `.bak` 报 `EPERM` | 补上 `closeSync`，占位改用 `writeFile(..., {flag:"wx"})`；0 字节 `.bak` 在 apply 时重建、revert 时丢弃 |

另外两个健壮性修复：临时文件名加进程内序号 + 随机段（同毫秒双写导致的 `rename ENOENT`）；
`atomicWriteSync` / `atomicWriteFile` / `atomicCopyFile` 共用同一套临时名生成。

**这些修改只动 `lib/` 与 `cordis.patch.yml` 的兼容层，不涉及原作者的提示词与思路。**
原始提示词、预设、技能目录、许可协议全部沿用，署名与「不得商用」条款照旧适用。

### 怎么装

```sh
git clone https://github.com/745184532/dsh-purge.git
cd dsh-purge
dsh plugin --profile desktop add .   # 官方桌面 EXE
dsh plugin --profile web     add .   # 官方 dsh web
```

写进 profile 之后，还要在该宿主的会话标题旁点 **dsh-purge → 清洗 → 应用**，成功会重启一次。

> `npm` 上并没有 `dsh-purge` 这个包（`add dsh-purge` 会 404），所以只能用上面的路径或 tarball 安装。