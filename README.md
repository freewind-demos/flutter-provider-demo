# Flutter Provider（ChangeNotifier）

## 简介

用 `ChangeNotifier` 保存计数，`ChangeNotifierProvider` 挂到树根，`Consumer` 精确重建依赖计数的子树，`context.read` 在回调里调用 `increment`。

## 快速开始

### 环境要求

Flutter SDK，`flutter doctor` 正常。

### 运行

```bash
flutter pub get
flutter run
```

## 概念讲解

### 第一部分：`ChangeNotifier` 与 `notifyListeners`

模型类继承 `ChangeNotifier`，内部字段变化后调用 `notifyListeners()`，Provider 会通知监听者刷新。比把变量散落在 `State` 里更容易抽离成独立类。

### 第二部分：`Consumer` vs `Provider.of`

`Consumer<Counter>` 只重建 `builder` 里那一小块；若整页包在 `Provider.of` 且 `listen: true`，容易造成无谓大范围重建。计数器 Demo 里用 `Consumer` 已足够直观。

## 完整示例

逻辑与 UI 见 `lib/main.dart`，含 `MultiProvider` 扩展前的最小形态。

## 注意事项

- 若状态树变大，可拆分多个 `ChangeNotifier` 或使用 `ProxyProvider` 组合。
- 与 Riverpod、Bloc 选型属于团队约定，本 Demo 只展示 Provider 典型用法。

## 完整讲解（中文）

Provider 家族在 Flutter 里像「官方入门推荐」：**概念少、和 Widget 树贴合紧**。`ChangeNotifier` 就是「带广播的小模型」，`Consumer` 帮你避免整页跟着抖。缺点是大应用里若没有清晰分层，容易出现「Notifier 越来越胖」。但对中小型功能、或作为其它架构的补充，它仍然非常实用。
