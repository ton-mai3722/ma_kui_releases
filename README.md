# MaKui (มาคุย) 💬

**MaKui** is a premium, highly-customized real-time messaging application built with Flutter. The project mission is to provide a "Friendly & Fluid Connection" experience, bypassing standard UI kits to create a unique, brand-specific interface using the Stream Chat engine.

---

## 📦 Download & Distribution

Official APK releases are maintained in a dedicated public repository for easy access:
🔗 **[MaKui Official Releases](https://github.com/ton-mai3722/ma_kui_releases)**

---

## 🎯 Implemented Features

### 1. 💬 Premium Messaging Experience
- **Real-time Chat**: Powered by Stream Chat Core for ultra-fast delivery.
- **Custom UI**: 100% custom-built message bubbles and input fields (No pre-built widgets).
- **Premium Stickers**: Tabbed sticker packs with transparent, bubble-less rendering and local caching for stability.
- **Media Support**: Seamlessly send images, files, and attachments with a built-in image viewer.
- **Rich Link Preview**: Automatic parsing and beautiful rendering of shared URLs with images and descriptions.
- **Interactions**: Custom reaction picker, typing indicators, and read receipts.

### 2. 📞 Communication & Social
- **Voice Calling**: Integrated voice calls via Stream Video SDK.
- **Smart Notifications**: Built-in "Missed Call" notification messages sent directly to the chat channel.
- **Active Status**: Real-time "Online" indicator (Green Dot) with a glowing effect on the channel list.
- **QR Profile**: Scan QR codes to add friends instantly or display your own profile code.

### 3. 🔐 Security & Account Management
- **Authentication**: Secure login via Google Account or Email/Password.
- **Legacy Migration**: Smart migration system for users transitioning from old username-only accounts.
- **Hard Delete**: Secure account and data removal functionality (Self-service).
- **Session Security**: Proactive session verification on app launch via Splash Screen.

### 4. 🎨 Advanced UI/UX
- **Premium Toast System**: Top-aligned, state-aware notifications (Success, Info, Warning, Error) with smooth animations.
- **Atmospheric Splash**: Dynamic loading experience with time-based transitions.
- **Pull-to-Refresh**: Modern interaction on contact and channel lists.
- **Customization**: Dark-mode ready palette (Teal & Coral) and typography using the `Prompt` font.

### 5. ⚙️ Settings & Management
- **Notification Controls**: Master toggle for notifications and "Quiet Hours" (DND) with customizable times.
- **Cloud Sync**: Local settings are automatically synchronized with Firebase Cloud Firestore.
- **Hybrid Update System**: 
    - **In-App Checker**: Proactive version verification on launch.
    - **FCM Topics**: Global push notifications for new releases.
    - **Admin Broadcast**: Emergency "MaKui Admin" messages for manual update delivery.
    - **Fallback UI**: "Open in Browser" option for failure-proof installation.

---

## 🛠 Admin & Management Tools

We have a suite of administrative tools to manage app updates and user engagement directly from the terminal.

### 1. Update Notification (FCM)
Send a system-wide push notification to all users notifying them of a new version.
```bash
python3 scripts/notify_update.py 2.0.1
```
*Note: This targets the `app_updates` topic.*

### 2. Admin Broadcast (Chat)
For emergency updates or users on older versions (e.g., 1.9.0) where the auto-update link might be broken, use this to send a direct message with the download link from a "MaKui Admin" account.
```bash
# Requirements: pip install stream-chat python-dotenv
python3 scripts/broadcast_admin.py 2.0.1 https://bit.ly/your-link
```

### 3. Firebase Remote Config Keys
Ensure these keys are configured in the Firebase Console:
- `latest_version`: The current version string (e.g., `2.0.1+23`).
- `force_update`: Set to `true` to block app usage until updated.
- `update_url`: (Optional) Overrides the default GitHub download link if needed.

---

## 🏗 Directory Structure (Clean Architecture)
```text
lib/
 ├── core/              # Global themes, constants, utilities, and DI
 ├── features/
 │    ├── auth/         # Authentication, Migration, and Session logic
 │    ├── chat/         # Chat rooms, Channels, Stickers, and QR
 │    └── profile/      # User profile, Settings, and Notifications
 ├── main.dart          # App entry point and global DI initialization
```

---

## 🚀 Automated Deployment (CI/CD)

We use a custom Python deployment pipeline to handle the entire release lifecycle.

### 1. Usage
Ensure you have the required Python libraries, then run:
```bash
python3 scripts/deploy.py
```

### 2. What the Script Does:
1. **Version Sync**: Automatically reads versioning from `pubspec.yaml`.
2. **Secure Build**: Builds a release APK with **R8/ProGuard obfuscation** enabled.
3. **Smart Naming**: Renames the output to `App-Makui-[version].apk`.
4. **GitHub Release**: Automatically creates a new Release on GitHub and uploads the APK.
5. **Changelog Sync**: Syncs the latest `CHANGELOG.md` notes to the release body.
6. **Firebase Sync**: Updates the `latest_version` in **Firebase Remote Config**.
7. **Portfolio Sync**: Automatically updates the changelog on the official Portfolio website.

---

Developed with ❤️ by Tonmai & Sommai (AI Assistant)