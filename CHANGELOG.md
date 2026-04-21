# Changelog

All notable changes to this project will be documented in this file.

## [1.7.0+18] - 2026-04-21

### Added
- **Feature: Missed Call Notifications**: Implemented an automated logging system where the caller's app sends a "Missed Call" or "Call Ended" message directly to the chat channel when a call is not answered or finished.
- **Feature: Voice Calling Restoration**: Re-enabled the Voice Call action button and optimized the Stream Video initialization lifecycle for immediate availability upon login.

### Fixed
- **Stability: Sticker Sending Pipeline**: Fixed a critical "Null check operator" crash occurring during sticker uploads. Refactored the system to bypass the SDK's file upload pipeline by leveraging `Message.extraData` for remote sticker assets.
- **Initialization: Stream Video Client**: Fixed a logic bug where the video client was not initializing during the user connection phase, preventing calls from being initiated.
- **UX: Zero-Width Validation**: Resolved a Stream SDK validation error ("Message is not valid") for stickers by implementing invisible zero-width space characters as message text.

### Changed
- **UI: Visual Harmony**: Updated the application CI and icon set to a cohesive Vibrant Blue/Purple aesthetic, ensuring consistent premium branding across all touchpoints.
- **UX: Sticker Bubble Rendering**: Updated Chat Bubbles to intelligently detect and render stickers from extraData while maintaining backward compatibility with legacy attachment-based stickers.

## [1.6.6+17] - 2026-04-17

### Added
- **Feature: Hard Account Delete**: Implemented a secure REST-based account deletion system (Hard Delete) that completely wipes user data, Firebase Auth, and local session for full privacy compliance.
- **Feature: Chat Deletion**: Added a "Delete Chat" option to the long-press channel menu, allowing users to permanently remove conversations with a safety confirmation dialog.
- **UX: Contact List Pull-to-Refresh**: Added RefreshIndicator support to the Contact screen, including the empty state, for a smoother user experience.

### Fixed
- **Audio: Focus Hijack Fix**: Resolved a critical issue where the app would stop background music (Spotify, etc.) and switch the system to "Call Mode" audio upon opening.
- **Sync: Message Read Status**: Permanently fixed the bug where messages were marked as "Read" automatically by disabling unstable offline persistence (Offline Storage).
- **UI: Realistic Splash Transitions**: Re-calibrated the atmospheric splash time engine to stay bright well into the late afternoon (5:30 PM), ensuring a better match with real-world lighting.
- **Bug: SDK API Compatibility**: Fixed multiple "method undefined" errors caused by recent Stream Chat SDK v9.23.0 updates.

### Changed
- **Architecture: Cloud-Only Sync**: Shifted to a purely real-time server-synced state to ensure 100% accurate read/unread status indicators.

## [1.6.5+16] - 2026-04-17

### Added
- **Feature: Dynamic Time Arc Animation**: The Splash screen now features a real-time Sun/Moon journey that maps precisely to your current hour (Sunrise 06:40).
- **UI: Atmospheric Splash Overhaul**: Redesigned the Splash screen with vibrant sky gradients and custom-layered, glowing celestial bodies (replaces standard system icons).
- **UI: Sleek Activity Indicator**: Replaced the standard circular loading with a premium, glowing Linear Progress Bar for a more modern feel.
- **Feature: Auto-Update Push Alerts**: Integrated an intelligent version monitoring system that triggers a local "Push Notification" whenever a new update is detected in the cloud.
- **UX: Smart Update Navigation**: Clicking the update notification now takes you directly to the Settings screen for one-tap downloading.

### Changed
- **Performance: Snappy Splash Transitions**: Optimized the splash animation lifecycle to be 25% faster and snappier on all devices.

## [1.6.4+15] - 2026-04-17

### Added
- **Feature: QR-Based Contact Discovery**: Overhauled the QR social experience with a premium, redesigned "My QR Code" profile card and an intuitive scanning interface.
- **UI: QR Access Points**: Integrated persistent QR action buttons into the main headers of both Channel List and Contact screens for instant access.
- **UX: Communicative QR Design**: Enhanced the QR display with clear, descriptive instructions ("Scan to add friend") to clearly communicate the feature's purpose.
- **UX: Seamless QR Navigation**: Added contextual shortcuts between QR Display and Scanner screens to ensure a fluid user journey.

## [1.6.3+14] - 2026-04-17

### Fixed
- **Stability: R8/ProGuard Runtime Fix**: Resolved `ClassNotFoundException: io.flutter.util.PathUtils` by adding explicit keep-rules for Flutter engine and Stream SDKs.
- **Build: Compilation Stability**: Fixed R8 build failures by ignoring non-critical library warnings during the minify process.

### Changed
- **UX: Intelligent Update Button**: Enhanced the Settings screen to disable the "Update" button when the app is already on the latest version, providing visual feedback via Snackbar.


## [1.6.2+13] - 2026-04-17

### Added
- **Security: APK Obfuscation**: Enabled Dart code obfuscation and R8/Proguard minification during build to prevent reverse-engineering.
- **Distribution: Public Release Repo**: Migrated binary distribution to a dedicated public repository (`ma_kui_releases`) to keep source code private while allowing public downloads.
- **Automation: Fully Automated Pipeline**: Finalized `deploy.py` to handle Build, GitHub Release, and Firebase Remote Config sync in one step.

### Fixed
- **Deployment: Storage Quota Issues**: Resolved Firebase Storage/Hosting quota and restriction issues by leveraging GitHub Releases CDN.


## [1.6.0+11] - 2026-04-17

### Added
- **Feature: App Update System**: Integrated Firebase Remote Config to monitor the latest version. User is now notified via a "NEW" badge in Settings when an update is available.
- **Feature: In-App Download Manager**: Implemented a premium download dialog that tracks and displays download progress/percentage directly within the app using `Dio`.
- **Feature: Auto-Installation**: Added `open_filex` integration to automatically trigger APK installation once the update download is verified and completed.
- **UI: Settings Screen**: Developed a dedicated Settings page accessible from the Profile screen for app management and account settings.
- **UI: Navigation Enhancements**: Re-designed the Floating Navigation Bar to a light, elegant glassmorphic style with improved visibility and overlap prevention for action buttons.
- **DevExp: Automated Deployment Script**: Created a Python-based deployment tool (`scripts/deploy.py`) that synchronizes Flutter builds with Firebase Remote Config updates in a single command.

### Changed
- **UX: Logout Migration**: Moved the "Logout" functionality from the Profile screen to the Settings screen for better information hierarchy, including a new confirmation safety dialog.

## [1.5.0+10] - 2026-04-17

### Added
- **UI: Floating Navigation Bar**: Overhauled main navigation with a premium, glassmorphic floating bar hosting three core tabs: **Chat**, **Contact**, and **Profile**.
- **Feature: Contacts Tab**: Added a dedicated `ContactScreen` powered by Stream's native user querying, enabling quick lookup and instant chat initiation with common contacts.
- **UI: Unified Tab Layout**: Consolidated historical standalone screens into a fluid `TabsScreen` architecture for improved multitasking and modern UX flow.
- **Feature: Voice & Video Calling**: Seamlessly integrated `stream_video_flutter`, enabling high-quality WebRTC-based 1-on-1 audio and video calls directly from the chat interface.
- **Feature: Call History Logging**: Implemented automated Call Logs dropped into the chat channel! Now records timestamps, duration, and whether a call was successfully connected, missed, or declined.
- **Feature: Offline Persistence**: Activated `stream_chat_persistence`. Users can now read historical messages offline, significantly accelerating app startup time via intelligent local SQLite caching.
- **Feature: Chat Pinning**: Users can now forcefully stick priority channels to the absolute top of their inbox lists using local `SharedPreferences` caching.
- **Feature: Mute / Unmute Channels**: Fully integrated Stream's native muting engine. Users can now sever push notifications dynamically per-channel without deleting chat arrays.
- **UI: Channel Options Modal**: Built a highly dynamic, glassy bottom sheet providing an intuitive visual interface when users "Long Press" a chat in the Channel List. Includes instant UI rebuilds and haptic feedback.
- **Feature: Background "Call Alerts" Channel**: Deployed a dedicated Max Importance notification channel (`call_alerts`) to display visible banner heads-up notifications (even outside the app) for incoming calls over Android & iOS.
- **UI: Dual-State Call Interfaces**: Separated Voice constraint and Video constraint UX. Voice calls now gracefully replace video previews with the contact's avatar, hiding extraneous video controls.
- **UI: Premium Connecting Screen**: Designed sleek, visually impressive Accept/Decline screens leveraging dynamic shadows, modern Google Fonts, and deep space gradients.

### Fixed
- **Bug: Double-Pop Navigation Crash**: Resolved a critical lifecycle navigation bug that previously dumped users into a black screen upon declining a call by locking downstream state emitters.
- **Bug: "Unknown Channel ID" Metadata Crash**: Fixed issue where the receiver failed to establish an active chat channel context when attempting to acknowledge a declined local call.
- **Bug: Stream Client Premature Wakeup**: Implemented Future-based delayed checks handling notification clicks to prevent calls from launching before the app core auth was fully initialized.
- **Bug: Notification Payload Collisions**: Prevented standard messages and call ringing events from cannibalizing each other in background-handler space.

## [1.4.0+9] - 2026-04-16

### Added
- **Feature: Swipe to Reply**: Integrated `swipe_to` functionality, allowing users to quickly reply by swiping right on any message bubble.
- **Feature: Quoted Messaging**: Added support for displaying quoted messages within chat bubbles to provide context for replies.
- **Feature: Multi-Image Sending**: Users can now select and send multiple images at once using a custom attachment picker.
- **Feature: Image Resizing**: Implemented automatic image resizing and compression (`maxWidth: 1600`, `imageQuality: 75`) during selection to optimize upload speed and data usage.
- **Feature: Fullscreen Image Viewer**: Integrated `photo_view` and `gal` to allow pinch-to-zoom viewing and saving downloaded images directly to the device gallery.
- **Hero Animations**: Added fluid Hero transitions between chat bubbles and the fullscreen image viewer.

### Changed
- **UI: Premium Dark CI**: Completely overhauled the Corporate Identity (CI) to a Premium Dark theme (`Deep Space Indigo` & `Neon Teal`), supporting dark mode across all screens.
- **UI: Glassmorphism Upgrades**: Upgraded the Login Screen and Chat Inputs to feature frosted glass effects (`1A162F`) over a deep dark background.
- **UI: App Icon v2**: Upgraded the launcher icon to a modern 3D Glassmorphic design and updated the Android adaptive background color.
- **Bug Fix (RenderBox)**: Fixed a layout crash when loading images with unrestricted heights by applying constraints and natural aspect ratios (`BoxFit.contain`).
- **UI: Gallery-Style Bubbles**: Enhanced message bubbles to support a grid-based image layout with premium shimmer effects during loading.

## [1.3.4+8] - 2026-04-10

### Added
- Implementation of modular feature-driven architecture (Auth, Chat, Profile).
- Dark/Light mode theme switching support.
- Firebase FCM notification integration for background messaging.
- Premium Splash Screen and brand-specific assets.

## [1.0.0] - 2026-04-01

- Initial project setup with `stream_chat_flutter_core`.
- Custom implementation of MakuiBubble and MakuiInput.
- Basic real-time messaging functionality.
