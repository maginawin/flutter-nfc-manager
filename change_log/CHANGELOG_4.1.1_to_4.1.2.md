# 更新日志：4.1.1 → 4.1.2

## 概述

修复 iOS 端标签发现流程中自动执行 NDEF 探测导致密码保护标签（如 FM11NT081D）无法正常使用的问题。移除标签发现时的 `queryNDEFStatus` 和 `readNDEF` 自动调用，避免破坏标签连接。

## 修复

- 移除 iOS 标签发现时自动调用 `queryNDEFStatus()` 的逻辑，密码保护标签不再因 NDEF 探测失败而丢失连接（NfcManagerPlugin.swift）

## 修改的文件

| 文件 | 变更类型 | 说明 |
|------|----------|------|
| ios/Classes/NfcManagerPlugin.swift | 修改 | 移除 `convert(_:NFCNDEFTag)` 中的 `queryNDEFStatus` 和 `readNDEF` 自动调用 |

## 提交记录
- `d55d1eb` add claude and fix auth issue
