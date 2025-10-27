# APK 托管待办事项

## 📦 需要上传到 GitHub Releases 的 APK 文件

目前本地有以下 APK 文件需要托管：

### 1. 小蜜蜂游戏
- **文件**: `apps/games/action/bee/rokid-bee-game.apk`
- **大小**: 13 MB (13,631,488 字节)
- **目标版本**: v1.0.0
- **当前配置的下载链接**: 
  ```
  https://github.com/jingbao-store/jingbao-store/releases/download/v1.0.0/rokid-bee-game.apk
  ```

## 🚀 操作步骤

### 方法 1: 使用 GitHub 网页界面

1. 打开仓库：https://github.com/jingbao-store/jingbao-store
2. 点击右侧的 "Releases" → "Create a new release"
3. 填写信息：
   - **Tag version**: `v1.0.0`
   - **Release title**: `v1.0.0 - 小蜜蜂游戏首发`
   - **Description**: 描述这个版本包含的内容
4. 拖拽 `rokid-bee-game.apk` 到 "Attach binaries" 区域
5. 点击 "Publish release"

### 方法 2: 使用 GitHub CLI

```bash
cd /Users/nicholasmac/Documents/code/jingbao-store

# 创建 release 并上传 APK
gh release create v1.0.0 \
  apps/games/action/bee/rokid-bee-game.apk \
  --title "v1.0.0 - 小蜜蜂游戏首发" \
  --notes "包含小蜜蜂游戏 APK 文件"
```

## ✅ 完成后

1. 验证下载链接是否可访问
2. 删除本地的 APK 文件（已被 .gitignore 排除）:
   ```bash
   rm apps/games/action/bee/rokid-bee-game.apk
   ```
3. 删除这个待办文件:
   ```bash
   rm APK_HOSTING_TODO.md
   ```

## 📝 注意事项

- Release 创建后，APK 文件将永久托管在 GitHub 上
- 下载链接格式：`https://github.com/用户名/仓库名/releases/download/标签/文件名`
- GitHub 对单个文件大小限制为 2GB，对于大多数 APK 来说足够了
- 建议为每个新版本创建对应的 Release 标签（如 v1.0.0, v1.1.0 等）

