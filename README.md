# mrite-模板

数学建模论文模板 — mrite skill 配套资源

## 仓库信息

- 远程地址：`https://github.com/lsllsl123/mrite--`
- 默认分支：`main`

## 后续上传步骤

### 1. 配置认证

将 GitHub Personal Access Token 保存到凭据管理器：

```powershell
git credential reject https://github.com
$cred = "protocol=https`nhost=github.com`nusername=lsllsl123`npassword=你的_TOKEN`n"
$cred | git credential approve
```

> 请勿将 token 直接写入此文件或提交到仓库。

### 2. 修改/添加文件后推送

```powershell
git add -A
git commit -m "提交说明"
git -c http.sslBackend=schannel push origin main
```

> 末尾的 `-c http.sslBackend=schannel` 是必要的，因为在此环境下 OpenSSL 网络被沙箱限制，需改用 Windows 原生 SSL（SChannel）才能正常连接 GitHub。

### 3. 拉取最新更新

```powershell
git -c http.sslBackend=schannel pull origin main
```

## 项目结构

```
.
├── SKILL.md              # mrite 技能核心配置
├── agents/
│   └── openai.yaml       # OpenAI 代理配置
├── assets/
│   └── template/         # 模板资源
│       ├── 解题要求/      # 解题要求说明
│       ├── 论文/          # LaTeX 论文模板
│       │   ├── 0.摘要.tex ~ 10.附录.tex
│       │   ├── format.cls
│       │   └── fonts/     # 思源宋体字库
│       ├── 数据/          # 数据（待填充）
│       ├── 求解/          # 求解代码（待填充）
│       └── 题目/          # 题目（待填充）
└── references/
    └── mrite-guidelines.md  # 详细使用指南
```
