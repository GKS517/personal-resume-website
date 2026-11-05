# 个人简历网站 · 使用与部署说明

单文件静态站点：`index.html`（CSS / JS 全部内联，无任何外部依赖，双击即可在浏览器打开）。

---

## 一、怎么改成自己的内容

打开 `index.html`，用编辑器（VS Code / 记事本都可）搜索下列关键字替换：

| 搜索这个词 | 替换为 |
|---|---|
| `你的名字` | 你的姓名（共 6 处：标题、导航、首屏、页脚） |
| `一句话介绍自己。把交通当作可优化的系统。` | 你的一句话标语 |
| `这里是 2–3 行的自我介绍` | 自我介绍正文 |
| `XX 大学` / `XX 中学` | 学校名称 |
| `3.8 / 4.0（或专业前 10%）` | 你的 GPA |
| `项目 01 · 项目名称` | 项目名（共 3 个） |
| `your@email.com` / `your_wechat` / `138 0000 0000` / `your-github` | 联系方式（每处两行：显示值 + `data-copy` 复制值） |

### 换头像
1. 把照片命名为 `avatar.jpg` 放到本目录；
2. 搜索 `AVATAR`，把这段：

```html
<div class="avatar-ph">
  <strong>◍</strong>
  AVATAR
</div>
```

替换为：

```html
<img src="avatar.jpg" alt="头像">
```

### 换作品图
搜索 `IMAGE 01`，在 `<figure>` 里把 `<div class="g-ph">...</div>` 换成 `<img src="work1.jpg" alt="作品 01">`（图片放同目录，或用 `images/work1.jpg` 这样建子目录）。

### 调技能条长度
每个进度条是 `<i style="--w:85%; ...">`，改 `--w` 的百分比即可。

---

## 二、让别人能访问（GitHub Pages，项目仓库方式）

> 前提：GitHub 账号 + 仓库设为 **Public**（免费账号的 Pages 只支持公开仓库）。

### 方式 A：网页上传（最简单，不用装任何东西）

1. 登录 GitHub → 右上角 `+` → **New repository**
2. Repository name 填 `resume`（或任意名），选 **Public**，**不要**勾 Add README → Create
3. 进入仓库 → **Add file → Upload files** → 把 `index.html` 和图片一起拖进去 → **Commit changes**
4. 仓库顶部 **Settings** → 左侧 **Pages**
5. Source 选 **Deploy from a branch**，Branch 选 **main** + **/ (root)** → **Save**
6. 等 1–2 分钟刷新，页面顶部出现地址：

```
https://<你的用户名>.github.io/resume/
```

把这个链接发给别人就能看。之后每次改内容，重新上传 `index.html` 覆盖，1 分钟左右自动更新。

### 方式 B：命令行（适合反复改动）

```bash
cd "C:/Users/Admin1/Desktop/个人简历网站"
git init -b main
git add .
git commit -m "init resume site"
git remote add origin https://github.com/<用户名>/resume.git
git push -u origin main
```

推送后按方式 A 的第 4–5 步开启 Pages 即可。

---

## 三、几个容易踩的坑

- **文件名必须是 `index.html`**，且放在仓库根目录，否则打开是 404。
- **图片用相对路径**（`avatar.jpg`，不要 `C:\...` 或 `file:///`），否则线上不显示。
- **首字母大写的仓库名不影响访问**，但地址区分大小写。
- **改了没生效**：等 1–2 分钟；仍不行就去 **Actions** 看部署记录，或强制刷新 `Ctrl + F5`。
- **国内访问 GitHub Pages 偏慢**（首屏 2–5 秒），可接受就先这样；要更快就绑自定义域名挂 Cloudflare 代理，或改用 Cloudflare Pages 部署（同样是连 GitHub 仓库，国内可达性更好）。

---

## 四、当前站点结构

```
index.html      单页：首屏 / 关于 / 教育背景 / 项目与竞赛 / 技能 / 作品区 / 联系方式
README.md       本文件（不需要上传到 GitHub 也能正常访问）
```

交互：滚动渐入、卡片悬停发光、技能条进入视口后生长、作品点击灯箱放大、联系方式点击复制、移动端汉堡菜单、光斑鼠标视差。
