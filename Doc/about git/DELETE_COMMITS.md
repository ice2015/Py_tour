# 删除红框内提交的操作记录

以下为更稳妥、可一次性达到最终效果的流程：仅保留 `Initial commit` 与 `add uv virthural2` 两条提交，且确保 `add uv virthural2` 的内容与原提交 `b9a8189` 完全一致。此流程避免了 `rebase -i` 可能引入的内容丢失问题。

## 前置检查

```bash
pwd
```
注释：确认当前工作目录。

```bash
git status -sb
```
注释：确认工作区干净且当前分支为 `main`。

```bash
git log --oneline --decorate -n 20
```
注释：确认需要删除的提交范围（红框内）。

## 删除中间提交（推荐做法）

```bash
git reset --hard b9a8189
```
注释：先回到原 `add uv virthural2` 的完整内容快照。

```bash
git reset --soft 9496399
```
注释：回到 `Initial commit`，但保留所有改动在暂存区。

```bash
git commit -m "add uv virthural2"
```
注释：重新生成第二个提交，内容与 `b9a8189` 完全一致。

## 结果确认

```bash
git log --oneline --decorate -n 10
```
注释：确认只剩两条提交（提交哈希会变化）：

```
<new_hash> (HEAD -> main) add uv virthural2
9496399 Initial commit
```

## 推送远端（需强推）

```bash
git push --force-with-lease origin main
```
注释：历史被改写，远端需要强推更新。
