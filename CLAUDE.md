# CLAUDE.md

## 项目概述

Flutter NFC Manager (`nfc_manager`) — 一个提供 Android 和 iOS NFC 功能的 Flutter 插件。
- 起始版本：4.1.1
- 原始仓库：[okadan/flutter-nfc-manager](https://github.com/okadan/flutter-nfc-manager)
- 许可证：MIT

## 项目结构

```
flutter-nfc-manager/
├── lib/                  # Dart 库代码
│   ├── nfc_manager.dart              # 主入口（跨平台）
│   ├── nfc_manager_android.dart      # Android 专属 API
│   ├── nfc_manager_ios.dart          # iOS 专属 API
│   ├── ndef_record.dart              # NDEF 支持
│   └── src/
│       ├── nfc_manager/              # 抽象基类和平台工厂
│       ├── nfc_manager_android/      # Android 实现 + 10 种标签类型
│       └── nfc_manager_ios/          # iOS 实现 + 5 种标签类型
├── android/              # Android 原生代码（Kotlin）
├── ios/                  # iOS 原生代码（Swift）
├── pigeon/               # 平台通道定义（Pigeon 代码生成）
│   ├── android.dart
│   └── ios.dart
├── example/              # 示例 Flutter 应用
└── user-temp/            # 临时文件（不纳入版本控制）
```

## 技术栈

| 层级 | 技术 | 版本要求 |
|------|------|----------|
| Dart/Flutter | Flutter SDK | >=3.3.0, Dart ^3.9.2 |
| Android | Kotlin 2.1.0, Gradle 8.9.1 | compileSdk 36, minSdk 24 |
| iOS | Swift 5.0, CocoaPods | iOS 13.0+ |
| 代码生成 | Pigeon | ^26.0.1 |
| 依赖 | ndef_record | ^1.3.3 |
| 代码检查 | flutter_lints | ^5.0.0 |

## Git 配置

### 远程仓库

| 名称 | 地址 | 用途 |
|------|------|------|
| **ali**（主要） | `git@codeup.aliyun.com:623ea833581fc62661c91d9e/srhome/nfc/flutter-nfc-manager.git` | **主远程仓库，推送目标** |
| origin | `git@github.com:maginawin/flutter-nfc-manager.git` | GitHub fork |
| upstream | `https://github.com/okadan/flutter-nfc-manager.git` | 上游原始仓库 |

### 分支

- `master` — 主分支，跟踪 `ali/master`
- 推送时默认使用 `ali` 远程

## 常用命令

```bash
# Pigeon 代码生成（修改 pigeon/*.dart 后执行）
dart run pigeon --input pigeon/android.dart
dart run pigeon --input pigeon/ios.dart

# Dart 代码分析
dart analyze

# 运行示例应用
cd example && flutter run

# 推送到主远程
git push ali master
```

## 代码规范

### 命名约定

- Android 专属类：`*Android` 后缀（如 `NfcAAndroid`, `MifareClassicAndroid`）
- iOS 专属类：`*Ios` 后缀（如 `FeliCaIos`, `MiFareIos`, `Iso15693Ios`）
- Pigeon 生成文件：`*.g.dart`（Dart）、`Pigeon.kt`（Kotlin）、`Pigeon.swift`（Swift）

### 代码风格

- 遵循 `flutter_lints` 规则（`analysis_options.yaml`）
- 平台特定代码通过 Pigeon 定义类型安全的平台通道

### 提交信息风格

参考现有提交记录：简洁描述变更内容，无需前缀标签。

## 平台通道架构

使用 [Pigeon](https://pub.dev/packages/pigeon) 生成类型安全的平台通道绑定：

- `pigeon/android.dart` → 生成 `lib/src/nfc_manager_android/pigeon.g.dart` + `android/.../Pigeon.kt`
- `pigeon/ios.dart` → 生成 `lib/src/nfc_manager_ios/pigeon.g.dart` + `ios/Classes/Pigeon.swift`

**不要手动编辑 `*.g.dart`、`Pigeon.kt`、`Pigeon.swift` 文件** — 它们由 Pigeon 自动生成。

---

### Claude Code Notes

- 所有回复和 Markdown 文件使用**简体中文**，但 UI 原型和流程图文字使用**英文**
- 将重要的分析/计划保存到 `docs/` 目录，文件名格式：`yyMMdd_HHmm_[description].md`
  - 注意当前年份为 2026 年
- 不要处理 `user-temp/` 目录
- 除非明确要求，回复中不要包含代码
- Git 提交中不要添加 `Co-Authored-By` 行
