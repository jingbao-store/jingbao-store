# 镜宝应用商店 - 应用列表

这个目录包含了镜宝应用商店的所有应用和游戏的元数据。

## ⚠️ 重要规则

**APK 文件管理：**

1. **禁止将 APK 文件提交到 Git 仓库**
   - APK 文件通常较大（数 MB 到数百 MB），会导致仓库体积膨胀
   - Git 不适合存储二进制文件，每次更新都会保留完整副本
   - 推送大文件可能导致 `HTTP 400` 或 `RPC failed` 错误

2. **推荐的 APK 托管方案：**
   - 📦 **GitHub Releases**：为每个版本创建 Release 并上传 APK
   - 🌐 **CDN/对象存储**：使用阿里云 OSS、七牛云、腾讯云 COS 等
   - 🔗 **直链托管**：使用 jsdelivr、unpkg 等 CDN 服务

3. **在仓库中只保存：**
   - 应用元数据（JSON 文件）
   - 图标和截图的 URL 链接
   - APK 的下载 URL
   - 版本信息和描述

## 目录结构

```
apps/
├── games/                    # 游戏大分类
│   ├── action/              # 动作游戏
│   │   ├── home.json        # 分类索引
│   │   └── bee/             # 小蜜蜂游戏
│   │       └── home.json    # 应用信息（包含下载URL）
│   ├── arcade/              # 街机游戏
│   ├── puzzle/              # 解谜游戏
│   └── casual/              # 休闲游戏
└── applications/            # 应用大分类
    ├── utilities/           # 工具
    │   ├── home.json        # 分类索引
    │   └── ar-recorder/     # AR录像应用
    │       └── home.json    # 应用信息（包含下载URL）
    ├── photo-video/         # 摄影与录像
    ├── productivity/        # 效率
    ├── entertainment/       # 娱乐
    ├── social/              # 社交
    └── education/           # 教育
```

**注意**：APK 文件不在 Git 仓库中，而是通过 `downloadUrl` 字段指向外部托管地址。

## 如何添加新应用

### 1. 创建应用目录

在相应的分类目录下创建一个以应用名称命名的子目录。例如：

```
/apps/applications/utilities/ar-recorder/
```

### 2. 创建应用信息文件

在应用目录下创建 `home.json` 文件，包含应用的完整信息：

**路径示例**：`/apps/applications/utilities/ar-recorder/home.json`

**文件格式**：

```json
{
  "id": "com.example.app",
  "name": "应用名称",
  "displayName": "显示名称",
  "version": "1.0.0",
  "description": "应用描述",
  "category": "utilities",
  "icon": "图标URL",
  "screenshots": ["截图URL1", "截图URL2"],
  "packageName": "包名",
  "downloadUrl": "https://github.com/jingbao-store/releases/download/v1.0.0/app.apk",
  "fileSize": "12.5 MB",
  "fileSizeBytes": 13107200,
  "developer": "开发者",
  "rating": 4.5,
  "downloads": 1000,
  "lastUpdated": "2025-10-27",
  "minAndroidVersion": "8.0",
  "permissions": ["权限1", "权限2"],
  "features": ["特性1", "特性2"]
}
```

**重要字段说明：**
- `downloadUrl`: APK 的外部托管地址（必需）
- `fileSize`: 人类可读的文件大小
- `fileSizeBytes`: 精确的字节数，用于下载进度显示

### 3. 托管 APK 文件

**不要将 APK 文件放在 Git 仓库中！** 选择以下托管方案之一：

#### 方案 A：GitHub Releases（推荐）

1. 在 GitHub 仓库创建新 Release
2. 上传 APK 文件作为 Release Asset
3. 获取下载链接，格式如：
   ```
   https://github.com/用户名/仓库名/releases/download/v1.0.0/app.apk
   ```

#### 方案 B：CDN/对象存储

1. 上传到阿里云 OSS、腾讯云 COS 或七牛云
2. 配置公开访问权限
3. 获取 CDN 加速链接

#### 方案 C：其他托管服务

- 使用专门的 APK 托管服务
- 自建文件服务器

### 4. 更新分类索引

在相应分类的 `home.json` 文件中添加应用目录的引用：

**路径**：`/apps/applications/utilities/home.json`

```json
{
  "category": "utilities",
  "displayName": "工具",
  "apps": [
    "ar-recorder/home.json"
  ]
}
```

## 支持的分类

### 游戏分类
- `action` - 动作游戏
- `arcade` - 街机游戏
- `puzzle` - 解谜游戏
- `casual` - 休闲游戏

可根据需要添加更多分类：
- `adventure` - 冒险
- `racing` - 竞速
- `sports` - 体育
- `strategy` - 策略
等

### 应用分类
- `utilities` - 工具
- `photo-video` - 摄影与录像
- `productivity` - 效率
- `entertainment` - 娱乐
- `social` - 社交
- `education` - 教育

可根据需要添加更多分类：
- `business` - 商务
- `health-fitness` - 健康健美
- `lifestyle` - 生活
- `news` - 新闻
- `shopping` - 购物
- `travel` - 旅游
- `weather` - 天气
等

## 完整示例

参考 `/apps/games/action/bee/` 小蜜蜂游戏作为完整示例。

**目录结构**：
```
apps/games/action/
├── home.json              # 分类索引文件
└── bee/                   # 小蜜蜂游戏目录
    └── home.json          # 应用信息（包含下载URL）
```

**分类索引** (`apps/games/action/home.json`)：
```json
{
  "category": "action",
  "displayName": "动作游戏",
  "apps": [
    "bee/home.json"
  ]
}
```

**应用信息** (`apps/games/action/bee/home.json`)：
```json
{
  "id": "com.rokid.bee.game",
  "name": "小蜜蜂",
  "displayName": "小蜜蜂游戏",
  "version": "1.0.0",
  "description": "经典的小蜜蜂射击游戏...",
  "category": "action",
  "downloadUrl": "https://github.com/jingbao-store/releases/download/v1.0.0/rokid-bee-game.apk",
  "fileSize": "13 MB",
  "fileSizeBytes": 13631488,
  "developer": "Rokid",
  ...
}
```

**注意**：`rokid-bee-game.apk` 文件托管在 GitHub Releases 或 CDN 上，不在 Git 仓库中。

## 优势

这种架构的优势：

1. **模块化**：每个应用独立目录，便于管理
2. **轻量级仓库**：APK 托管在外部，Git 仓库保持轻量
3. **快速克隆**：开发者克隆仓库只需几秒，不用下载大量 APK
4. **灵活托管**：可以使用 CDN 加速，提升全球用户下载速度
5. **版本管理**：通过 GitHub Releases 管理不同版本的 APK
6. **节省成本**：避免 Git LFS 的额外成本
7. **推送无忧**：不会因文件过大导致推送失败

## 最佳实践

1. ✅ 始终使用外部托管存储 APK
2. ✅ 在 `home.json` 中提供准确的 `downloadUrl`
3. ✅ 记录 `fileSize` 和 `fileSizeBytes` 以便显示下载进度
4. ✅ 使用语义化版本号（如 v1.0.0）
5. ❌ 永远不要将 `.apk` 文件提交到 Git
6. ❌ 不要使用 Git LFS（成本高且非必要）

