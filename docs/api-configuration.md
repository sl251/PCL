# 第三方分支的登录与 Mod 下载配置

此分支移除了每次启动时显示的“开源版本说明”弹窗。移除弹窗不会自动获得服务端 API 权限，也不会开启原本未实现的功能。

## 配置入口

| 功能 | 本机环境变量 | GitHub Actions Secret |
| --- | --- | --- |
| 微软登录 | `PCL_MS_CLIENT_ID` | `CLIENT_ID` |
| CurseForge 官方 API | `PCL_CURSEFORGE_API_KEY` | `CURSEFORGE_API_KEY` |

本机环境变量优先于构建时注入的默认值。微软登录仍需配置可访问 Minecraft 服务且允许用于本项目的应用 ID；配置入口不会绕过服务端审核。

CurseForge 官方按应用发放 Key，没有官方通用共享 Key。不要把个人 Key 或其他项目的 Key 提交到公开源码；用环境变量或仓库 Secret 配置自己的 Key。

## 未配置 CurseForge Key 时

- Modrinth 的公开搜索、版本查询和下载仍可使用。
- CurseForge 请求仅尝试代码中已有的 MCIM 镜像，不再重复请求需要 Key 的官方 API。
- 镜像不可用时会明确提示。混合搜索仍可显示成功返回的 Modrinth 结果。
- 仅在 CurseForge 发布的 Mod、依赖其文件信息的整合包安装、版本查询及更新检查可能无法自动完成。可从项目网站下载文件后手动导入。
- 已安装的本地 Mod 不会因为缺少 API Key 而无法加载。

镜像是第三方服务，其可用性、覆盖范围和缓存时效不能保证。即使配置了官方 Key，作者关闭第三方分发的项目仍可能需要通过网站或官方客户端下载。

## 参考

- [CurseForge API 与 Key 申请](https://support.curseforge.com/en/support/solutions/articles/9000208346-about-the-curseforge-api-and-how-to-apply-for-a-key)
- [CurseForge API 使用条款](https://support.curseforge.com/en/support/solutions/articles/9000207405-curse-forge-3rd-party-api-terms-and-conditions)
- [CurseForge 第三方分发设置](https://support.curseforge.com/support/solutions/articles/9000207877)
- [Modrinth API 身份认证说明](https://docs.modrinth.com/api/)
- [MCIM 文档](https://docs.mcimirror.top/)
