# 文件批量重命名工具

一个基于 Java Swing 的桌面小工具，用于在 Windows 上批量重命名文件。支持正则筛选、多种重命名规则、预览、多步撤销等常用功能。

## 功能特性

- 正则表达式筛选文件（如只显示以"测试"开头的文件、只显示图片等）
- 多种重命名规则：
  - 查找替换
  - 添加前缀 / 后缀
  - 序号填充（如 `001_`、`002_`）
  - 修改扩展名
- 预览重命名效果（原文件名 → 新文件名）
- 多步撤销（可撤销 1 步、2 步、3 步或全部）
- 进度条显示处理进度

## 目录结构

```
FileRenamer/
├── src/                            # 源代码
│   ├── com/renamer/
│   │   ├── FileRenamerGUI.java     # GUI 主程序
│   │   └── RenameRule.java         # 重命名规则抽象
│   └── META-INF/MANIFEST.MF
├── .idea/artifacts/FileRenamer_jar.xml   # IDEA 打包配置
├── README.md
└── LICENSE
```

## 使用方法

### 方式一：直接下载 Release（推荐普通用户）

到 [Releases 页面](https://github.com/Auzztt/FileUtil/releases) 下载 `FileRenamer-vX.X.X-windows-amd64.zip`：

1. 解压 zip 到任意目录
2. 双击 `文件批量重命名工具.exe` 即可运行
3. 无需安装 Java，runtime 已内置

> 注意：整个文件夹需要保持完整，不要单独移动 exe 文件。

### 方式二：从源码构建

需要安装 JDK 21+。

```powershell
# 1. 编译
javac -d out src/com/renamer/*.java -cp src

# 2. 打包成 jar
jar cfm out/FileRenamer.jar src/META-INF/MANIFEST.MF -C out .

# 3.（可选）使用 jpackage 打包成免安装 exe
& "$env:JAVA_HOME\bin\jpackage.exe" `
    --type app-image `
    --name "文件批量重命名工具" `
    --input out `
    --main-jar FileRenamer.jar `
    --main-class com.renamer.FileRenamerGUI `
    --dest dist `
    --app-version 1.0.0 `
    --vendor FileRenamer `
    --java-options "-Dfile.encoding=UTF-8"
```

## 操作指南

1. **选择文件夹**：点击"选择文件夹"，找到要处理的目录
2. **筛选文件**（可选）：在"文件筛选"框输入正则，点击"应用筛选"
3. **选择重命名规则**：从下拉框选择规则并填入参数
4. **预览**：点击"预览重命名"查看效果
5. **执行**：确认无误后点击"执行重命名"
6. **撤销**（如需）：点击"撤销上次重命名"恢复

### 常用正则示例

| 正则 | 含义 |
|------|------|
| `^测试.*` | 以"测试"开头 |
| `.*\.txt$` | txt 文件 |
| `.*照片.*` | 包含"照片" |
| `^[0-9].*` | 以数字开头 |
| `.*\.(jpg\|png)$` | jpg 或 png 图片 |

## 系统要求

- Windows 7 / 8 / 10 / 11（64 位）
- 若使用 Release 包：无需额外环境
- 若从源码构建：JDK 21+

## 许可证

本项目采用 [MIT License](LICENSE)。

## 项目地址

- GitHub: [Auzztt/FileUtil](https://github.com/Auzztt/FileUtil)
