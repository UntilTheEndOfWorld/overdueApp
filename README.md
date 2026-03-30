<<<<<<< HEAD
# overdue SwiftUI 子项目

与 `overdue-miniUI`（uni-app）功能对齐的 **iOS 原生架构骨架**：业务逻辑在 **OverdueKit**（Swift Package），入口在 **OverdueApp**。

## 目录结构

```
overdue-swiftui/
├── OverdueKit/                    # SPM 库：路由、网络、会话、各 Feature 占位视图
│   ├── Package.swift
│   └── Sources/OverdueKit/
│       ├── App/                   # AppRootView（登录 / 主 Tab）
│       ├── Navigation/            # AppRoute、MainTab、MainTabView
│       ├── Core/
│       │   ├── Networking/        # APIConfig、APIClient（对齐 api.js）
│       │   ├── Session/           # SessionStore（对齐 auth + 本地用户）
│       │   └── Theme/             # AppTheme（对齐全局色）
│       ├── Features/              # 按业务域拆分，对应 pages.json
│       └── Components/            # 公共组件（待补 item-card 等）
└── OverdueApp/
    └── OverdueApp.swift           # @main，注入 SessionStore
```

## 与 uni-app 的对应关系

| uni-app | SwiftUI |
|---------|---------|
| `tabBar` 五页 | `MainTab` + `MainTabView` |
| `pages/*` | `Features/*` + 后续 `NavigationPath` / `AppRoute` |
| `api.js` | `APIClient` + `APIConfig` |
| `auth.js` / 存储 | `SessionStore`（后续 Keychain） |
| `easycom` 组件 | `Components/` |

## Sign in with Apple（已接入）

1. 在 Xcode 选中 **App Target** → **Signing & Capabilities** → **+ Capability** → 添加 **Sign in with Apple**。
2. 将仓库内 `OverdueApp/OverdueApp.entitlements` 合并进工程（或确保其中包含 `com.apple.developer.applesignin` = `Default`）。
3. **Apple Developer** 后台为该 App ID 勾选 **Sign in with Apple**。
4. 登录流程：`LoginView` 使用 `SignInWithAppleButton` → `AppleSignInPayload` → `SessionStore.signInWithApple` → `exchangeAppleTokenWithBackend`（**请在服务端用 `identityToken` 校验并返回业务 JWT**，替换当前 DEBUG 占位 `accessToken`）。

## 在 Xcode 中打开（macOS）

1. 打开 Xcode → **File → New → Project** → **App**，Interface：**SwiftUI**，命名如 **Overdue**，保存到本目录旁或 `overdue-swiftui/` 下。
2. 删除 Xcode 生成的 `ContentView.swift`，将 **OverdueApp** 中的 `OverdueApp.swift` 合并进工程的 App 目标（或直接把 `OverdueApp` 文件夹加入目标）。
3. **File → Add Package Dependencies…** → **Add Local…** → 选择 `OverdueKit` 目录。
4. 在 App 目标的 **Frameworks** 中链接 **OverdueKit**；确保 **Deployment Target ≥ iOS 17**（`@Observable` / Observation）。
5. 将 `OverdueApp.swift` 中的 `@main` 保留 **唯一**（删除模板里重复的 `@main`）。

若希望 **单仓库内零图形界面创建**：也可仅用命令行 `swift build` 编译 `OverdueKit`（无法编译完整 iOS App Bundle，App 仍需 Xcode）。

## 后续迭代建议

1. 在 `OverdueKit` 中按 `api.js` 方法逐条增加 `*Service`（异步 + DTO）。
2. 用 `NavigationPath` + `AppRoute` 替换 Feature 内占位 `NavigationLink` 文案。
3. 深链：对齐小程序 `inviteCode` → `SessionStore.pendingInviteCode` + `onOpenURL`。
4. 主题：用 `preferredColorScheme` 与 `AppStorage` 对齐 `theme.js`。
=======
# overdueApp
>>>>>>> be569f0ab5bf850f6c57e45a5fcd167f7ce42335
