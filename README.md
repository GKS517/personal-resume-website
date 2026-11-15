# 高楷松 · 个人简历网站

单文件静态站点：`index.html`（CSS / JS 全部内联，无外部依赖，双击即可在浏览器打开）。
内容依据本人《生涯发展报告》（2026.11），结构为：首屏 → 目标职业 → 教育背景 → 能力结构 → 行动与交付物 → 四年路线 → 行业判断 → 联系方式。
配套素材：`avatar.jpg`（首屏头像）。

---

## 一、还需要你填的（就这一处）

联系方式目前是占位符，`index.html` 里搜这四个词替换：

| 搜索 | 替换为 |
|---|---|
| `your@email.com` | 邮箱（出现 2 次：`data-copy` 属性 + 显示文字，都要改） |
| `your_wechat` | 微信号 |
| `13800000000` / `138 0000 0000` | 手机号（同上，两处） |
| `your-github` | GitHub 主页 |

---

## 二、以后要更新的地方

| 改什么 | 搜索 | 怎么改 |
|---|---|---|
| 头像 | `avatar.jpg` | 直接覆盖同名文件，建议正方形、≥600px |
| 能力自评 | `abi-row` | 共 6 行，每行改三处：数字 `<b>1.5</b>`、`--w`（当前值 ÷ 5）、`--t`（目标值 ÷ 5） |
| 交付物 | `交付物 01` ~ `交付物 04` | 标题、描述、标签、状态徽章（`pill` = 进行中，`pill plan` = 计划中） |
| 四年路线 | `PLAN 01` ~ `PLAN 04` | 每学年改 `<li>` 列表；底部 `KEY` 行是关键节点 |
| 行业数据 | `data-num` | 四个数字 + 说明 + 来源 |

改完注意：**能力自评均值写在首屏统计和 03 节底部（1.3 → 3.5）**，如果改了六项分数，这两处要一起重算。

---

## 三、让别人能访问（GitHub Pages）

> 前提：GitHub 账号 + 仓库设为 **Public**（免费账号的 Pages 只支持公开仓库）。

### 方式 A：网页上传（不用装任何东西）

1. 登录 GitHub → 右上角 `+` → **New repository**
2. Repository name 填 `resume`，选 **Public**，不要勾 Add README → Create
3. 进入仓库 → **Add file → Upload files** → 把 `index.html` 和 `avatar.jpg` 一起拖进去 → **Commit changes**
4. **Settings** → 左侧 **Pages** → Source 选 `Deploy from a branch` → Branch 选 **main** + **/ (root)** → **Save**
5. 等 1–2 分钟，地址是：

```
https://<你的用户名>.github.io/resume/
```

之后改内容重新上传覆盖，1 分钟左右自动更新。

### 方式 B：命令行（本机已配置好，直接用）

本机 `github.com:443`（HTTPS）被网络阻断，所以 remote 走 SSH：

```bash
cd "C:/Users/Admin1/Desktop/个人简历网站"
git add -A
git commit -m "改了什么"
git push
```

SSH 通过 `ssh.github.com:443` 出网（见 `~/.ssh/config`），已用本机公钥登记为仓库 **Deploy Key**，只对这个仓库有效。

> 换电脑 / 重装系统后若要重新配置：把 `~/.ssh/id_ed25519.pub` 内容加到仓库
> **Settings → Deploy keys → Add deploy key**，勾选 *Allow write access*。

### 方式 C：HTTPS 全断时的备用推送

`git push` 仍失败（比如公司网络连 22/443 都封）时，走 GitHub REST API 推送，脚本已放在 `.workbuddy/tools/`：

```bash
node .workbuddy/tools/push-via-api.mjs
```

原理是用 Git Data API 复刻本地提交对象，生成的新提交 SHA 与本地完全一致，不会造成历史分叉。

---

## 四、容易踩的坑

- **文件名必须叫 `index.html`** 且在仓库根目录，否则 404。
- **图片用相对路径**（`avatar.jpg`，不能 `C:\...` 或 `file:///`），否则线上不显示。
- **改了没生效**：等 1–2 分钟；不行去 **Actions** 看部署记录，或 `Ctrl + F5` 强制刷新。
- **国内访问 GitHub Pages 偏慢**（2–5 秒），嫌慢就绑自定义域名挂 Cloudflare，或换 Cloudflare Pages（同样连 GitHub 仓库，国内可达性更好）。
