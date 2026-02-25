# 恢复 `add uv virthural2` 内容并保留两条提交的操作记录

目标：只保留 `Initial commit` 与 `add uv virthural2` 两条提交，同时确保 `add uv virthural2` 的内容与原提交一致。

## 执行步骤

```bash
git reset --hard b9a8189
```
注释：将工作区恢复到原 `add uv virthural2`（`b9a8189`）的完整内容。

```bash
git reset --soft 9496399
```
注释：回到 `Initial commit`，但保留全部改动在暂存区。

```bash
git commit -m "add uv virthural2"
```
注释：重新生成第二个提交，内容与原 `add uv virthural2` 保持一致。

## 结果确认

```bash
git log --oneline --decorate -n 5
```
注释：确认只剩两条提交：

```
acdabde (HEAD -> main) add uv virthural2
9496399 Initial commit
```

## 远端更新（待确认）

```bash
git push --force-with-lease origin main
```
注释：因为历史被改写，推送需使用强推。
