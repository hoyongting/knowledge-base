# 专题：Git 与 GitHub 实战

> 把日常用到的 Git 操作集中在这里，随查随用。

- **标签**：#Git #GitHub #工具
- **创建**：2026-11-20

## 常用命令速查

```bash
# 初始化与提交
git init
git add .
git commit -m "说明"

# 分支
git checkout -b feature/xxx       # 新建并切换分支
git branch -M main                # 重命名当前分支
git push -u origin main           # 首次推送并设上游

# 同步
git pull origin main
git fetch --all

# 撤销
git restore <file>                # 丢弃工作区改动
git reset --soft HEAD~1           # 撤销上次提交但保留改动
```

## 完整 PR 工作流

1. 从 `main` 切出新分支 `feature/xxx`
2. 在分支上做修改、提交
3. 推送分支到远程
4. 在 GitHub 上发起 Pull Request
5. 审阅、合并回 `main`

> 本知识库的第一次 PR 就是走这个流程完成的——详见 [[2026-11-20-GitHub连接排障记]]。

## 踩坑记录

- **域名解析被污染**：GitHub 连不上时，优先用 `curl --resolve` 测试各官方 IP 的真实 HTTPS 握手，找出能用的节点钉进 hosts。
- **令牌推送**：`git -c http.extraHeader` 方式可能返回 406，改用 URL 内嵌令牌 `https://user:token@github.com/...` 更可靠。
- **浏览器 DoH**：Firefox 默认开启加密 DNS 会绕过 hosts，需在 `user.js` 写入 `network.trr.mode=5` 关闭。
