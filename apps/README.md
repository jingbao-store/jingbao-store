# 镜宝应用商店 - 应用列表

这个目录包含了镜宝应用商店的所有应用和游戏的元数据。

## 目录结构

```
apps/
├── games/                    # 游戏大分类
│   ├── action/              # 动作游戏
│   │   ├── home.json        # 分类索引
│   │   └── bee/             # 小蜜蜂游戏
│   │       ├── home.json    # 应用信息
│   │       └── rokid-bee-game.apk
│   ├── arcade/              # 街机游戏
│   ├── puzzle/              # 解谜游戏
│   └── casual/              # 休闲游戏
└── applications/            # 应用大分类
    ├── utilities/           # 工具
    │   ├── home.json        # 分类索引
    │   └── ar-recorder/     # AR录像应用
    │       ├── home.json    # 应用信息
    │       └── app.apk
    ├── photo-video/         # 摄影与录像
    ├── productivity/        # 效率
    ├── entertainment/       # 娱乐
    ├── social/              # 社交
    └── education/           # 教育
```

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
  "downloadUrl": "下载链接",
  "localPath": "apps/applications/utilities/ar-recorder/app.apk",
  "fileSize": "文件大小",
  "developer": "开发者",
  "rating": 4.5,
  "downloads": 1000,
  "lastUpdated": "2025-10-27",
  "minAndroidVersion": "8.0",
  "permissions": ["权限1", "权限2"],
  "features": ["特性1", "特性2"]
}
```

### 3. 放置应用安装包

将 APK 文件放在应用目录下：

```
/apps/applications/utilities/ar-recorder/app.apk
```

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
    ├── home.json          # 应用信息
    └── rokid-bee-game.apk # 安装包
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
  "localPath": "apps/games/action/bee/rokid-bee-game.apk",
  ...
}
```

## 优势

这种目录结构的优势：

1. **模块化**：每个应用独立目录，便于管理
2. **清晰**：应用信息、资源文件、安装包都在同一目录
3. **可扩展**：可以轻松添加图标、截图等资源文件
4. **版本管理**：可以在应用目录下维护多个版本

