# 应用更新配置指南

本指南说明如何配置和发布 jingbao-app 的版本更新。

## 配置文件位置

更新配置文件位于仓库根目录：`app-update.json`

## 配置文件格式

```json
{
  "appId": "com.jingbao.store",
  "latestVersion": "1.0.0",
  "versionCode": 1,
  "versionName": "1.0.0",
  "updateTime": "2025-10-30",
  "downloadUrl": "https://gitee.com/jingbao-store/jingbao-app/releases/download/v1.0.0/jingbao-store-v1.0.0.apk",
  "fileSize": "15 MB",
  "fileSizeBytes": 15728640,
  "minAndroidVersion": "7.0",
  "releaseNotes": [
    "更新说明 1",
    "更新说明 2",
    "更新说明 3"
  ],
  "forceUpdate": false,
  "changelog": "详细的更新日志内容"
}
```

## 字段说明

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `appId` | string | ✅ | 应用包名，必须为 `com.jingbao.store` |
| `latestVersion` | string | ✅ | 最新版本号（显示用） |
| `versionCode` | number | ✅ | 版本代码（用于版本比较，必须递增） |
| `versionName` | string | ✅ | 版本名称 |
| `updateTime` | string | ✅ | 更新日期，格式：YYYY-MM-DD |
| `downloadUrl` | string | ✅ | APK 下载地址 |
| `fileSize` | string | ✅ | 文件大小（显示用） |
| `fileSizeBytes` | number | ✅ | 文件字节数（精确值） |
| `minAndroidVersion` | string | ✅ | 最低 Android 版本要求 |
| `releaseNotes` | array | ✅ | 更新说明列表 |
| `forceUpdate` | boolean | ✅ | 是否强制更新 |
| `changelog` | string | ❌ | 详细更新日志（可选） |

## 发布新版本流程

### 1. 构建新版本 APK

在 `jingbao-app` 项目中：

```bash
cd jingbao-app
./gradlew assembleRelease
```

生成的 APK 位于：`app/build/outputs/apk/release/app-release.apk`

### 2. 更新版本号

在 `jingbao-app/app/build.gradle.kts` 中更新：

```kotlin
defaultConfig {
    applicationId = "com.jingbao.store"
    minSdk = 24
    targetSdk = 36
    versionCode = 2  // 递增版本代码
    versionName = "1.1.0"  // 更新版本名称
    
    testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
}
```

### 3. 上传 APK 到发布平台

将构建好的 APK 上传到：
- GitHub Releases
- Gitee Releases
- 或其他文件托管服务

### 4. 更新配置文件

修改 `jingbao-store/app-update.json`：

```json
{
  "appId": "com.jingbao.store",
  "latestVersion": "1.1.0",
  "versionCode": 2,  // ⚠️ 必须大于之前的版本
  "versionName": "1.1.0",
  "updateTime": "2025-11-01",
  "downloadUrl": "https://gitee.com/jingbao-store/jingbao-app/releases/download/v1.1.0/jingbao-store-v1.1.0.apk",
  "fileSize": "16 MB",
  "fileSizeBytes": 16777216,
  "minAndroidVersion": "7.0",
  "releaseNotes": [
    "新增自动更新功能",
    "优化应用性能",
    "修复已知问题"
  ],
  "forceUpdate": false
}
```

### 5. 提交更改

```bash
cd jingbao-store
git add app-update.json
git commit -m "发布 v1.1.0 版本更新"
git push origin main
```

### 6. 验证更新

在安装了旧版本的设备上：
1. 打开 jingbao-app
2. 点击顶部栏的 🔄 按钮
3. 应该会显示更新提示

## 强制更新

如果发现严重 bug 需要强制用户更新，设置：

```json
{
  "forceUpdate": true
}
```

强制更新时，用户无法点击"稍后更新"按钮，必须下载安装新版本。

## 注意事项

1. **版本代码必须递增**：`versionCode` 必须比之前的版本大，否则不会触发更新提示
2. **下载地址要可访问**：确保 `downloadUrl` 在国内外都能访问，建议使用 Gitee 或 jsDelivr CDN
3. **文件大小要准确**：`fileSizeBytes` 应该是 APK 文件的真实大小
4. **测试更新流程**：发布前先用测试设备验证更新流程是否正常

## 获取文件大小

### Linux/macOS:
```bash
ls -l app-release.apk | awk '{print $5}'
```

### Windows (PowerShell):
```powershell
(Get-Item app-release.apk).Length
```

## CDN 加速

为了提高国内访问速度，建议使用以下 CDN：

- jsDelivr: `https://cdn.jsdelivr.net/gh/用户名/仓库名@分支/文件路径`
- Gitee: `https://gitee.com/用户名/仓库名/releases/download/标签/文件名`

## 常见问题

### Q: 用户点击检查更新后没有反应？
A: 检查网络连接和 `downloadUrl` 是否可访问。

### Q: 提示有更新但版本号一样？
A: 检查 `versionCode` 是否正确递增。

### Q: 下载完成后无法安装？
A: 确保用户授予了"安装未知应用"权限。

### Q: 如何回滚到旧版本？
A: 不推荐回滚，但可以通过降低 `versionCode` 实现（不建议）。

## 版本命名建议

- 主版本号：重大功能更新或架构变更（如 1.0.0 → 2.0.0）
- 次版本号：新增功能（如 1.0.0 → 1.1.0）
- 修订号：bug 修复（如 1.0.0 → 1.0.1）

versionCode 应该持续递增，不受版本命名影响。

