# Changelog

All notable changes to this project will be documented in this file.

## [2.4.0+27] - 2026-04-30

### Added
- **Feature: Widget Screenshot Share**: Replaced standard image sharing with a high-resolution widget capture system. Users can now share a complete screenshot of the post card (including user header, text, and media) as a single PNG image.
- **System: Soft Delete Filtering**: Implemented a comprehensive filtering system that excludes posts marked with `isDeleted: true` from the Feed datasource and Profile stream.

### Fixed
- **Bug: Post Deletion Sync**: Fixed a critical issue where deleted posts remained visible on the Feed and Profile pages.
- **Bloc: Instant Feed UI Update**: Added `RemovePostEvent` to `FeedBloc` for immediate UI removal of posts upon successful soft deletion.
- **Model: Entity Flag Integration**: Added `isDeleted` persistence to the `Post` entity and `PostModel` to ensure consistent state across app sessions.

## [2.3.0+26] - 2026-04-29

### Added
- **Feature: High-Performance Profile Stats**: Overhauled the profile statistics system (Posts, Friends, Likes) to use a high-performance counter-based approach stored directly in the `users` collection.
- **Feature: Auto-Recalculation Engine**: Implemented a post-update synchronization system that automatically recalculates and migrates user stats from Firestore sub-collections and Stream Chat channels upon the first launch of a new version.
- **System: Real-Time Stats Sync**: Integrated real-time increments for post counts, friend counts, and total likes across the feed and chat systems.

### Fixed
- **UI: Image Cropper Overlap**: Resolved a critical layout issue where the image cropper overlapped the Android status bar by implementing a custom `Theme.UCrop` and `AndroidUiSettings` configuration.
- **UI: Profile Sync Stability**: Added a stats reload trigger after profile updates to ensure the UI immediately reflects name, bio, and image changes.
- **Architecture: Profile Stat Protection**: Implemented a filter in `updateFirestoreUser` to prevent accidental overwriting of statistical counters with stale metadata from external sources.

## [2.2.0+25] - 2026-04-29

### Added
- **Feature: Friend Relationship Persistence**: Automatically stores newly added friends' metadata (Name, ID, Avatar, Timestamp) in Firestore for persistent tracking.
- **Feature: Legacy Friend Synchronization**: Implemented a "Sync All Friends" engine that automatically migrates existing Stream Chat contacts to Firestore upon app update, ensuring full cross-device consistency.
- **System: Version-Aware Sync**: Optimized background synchronization to run once per version update, leveraging both local and cloud flags (Firebase) to minimize resource usage.

### Changed
- **UX: Swipe-to-Reply Refinement**: Fine-tuned swipe sensitivity (`swipeSensitivity: 15`) to prevent accidental triggers.
- **UI: Reply Preview Overhaul**: Redesigned the reply preview UI for a more compact, premium aesthetic with frosted glass effects (`BackdropFilter`) and gradient borders.

### Fixed
- **Bug: Undefined Name 'widget'**: Resolved a scope issue in `ContactScreen` by moving the QR menu into the State class.
- **Bug: DI Dependency Chain**: Fixed an "Undefined name 'addFriendUseCase'" error in `main.dart` by correctly injecting the UseCase into the application root.

## [2.1.0+24] - 2026-04-28

### Added
- **Feature: Global Message Search**: Implemented a powerful search engine allowing users to search across all conversations from the home screen.
- **Feature: In-Chat Search**: Added a dedicated search button within chat rooms to find specific messages in that conversation.
- **UI: Messenger-Style Input Bar**: Overhauled the message input with:
    - Dedicated **Camera** and **Gallery** icons on the left for faster media sharing.
    - Vibrant, diverse color palette for action icons (Blue/Pink/Purple).
    - Intelligent **Sticker Picker** with auto-focus management (closes when typing).
- **UI: Glassmorphism 2.0**: Applied high-end glass effects (BackdropFilter) to the AppBar and Message Input for a seamless blend with the dynamic background.
- **Security: Secure Account Deletion**: Added a re-authentication step (password check) before hard-deleting an account for enhanced security.
- **UI: Opponent User Profile**: Added an "info" button in the Chat Room AppBar to view the other person's profile details in a premium bottom sheet.

### Fixed
- **Stability: Stream Search SDK Integration**: Fixed positional argument and pagination parameter errors in the `client.search` method.
- **Bug: Type Mismatch in Search Results**: Resolved a `ChannelModel` vs `Channel` type conflict when navigating from search results to a chat room.
- **UX: Input Focus**: Fixed an issue where the sticker picker wouldn't close when tapping the text field.

## [2.0.1+23] - 2026-04-28

### Added
- **System: FCM Broadcast Support**: Integrated `app_updates` topic subscription for global update notifications.
- **System: Admin Broadcast Tool**: Created `scripts/broadcast_admin.py` to send direct update links to all users via a "MaKui Admin" chat persona.
- **UI: Clickable Links in Chat**: Implemented `flutter_linkify` in `MakuiBubble` to automatically detect and open URLs in the system browser.
- **UI: Reaction Update**: Changed the heart reaction from black to a vibrant red emoji (`❤️`) for consistent branding.
- **UX: Update Fallback**: Added a "Open in Browser" option to the update download dialog for manual installation if the in-app downloader fails.

### Fixed
- **Navigation: Notification Priority**: Refactored `NotificationService` to ensure update notifications take precedence over chat navigation, resolving "no-op" clicks.
- **Build: Pubspec Integrity**: Resolved duplicate mapping key errors in `pubspec.yaml` to ensure stable dependency resolution.

## [2.0.0+22] - 2026-04-28

### Added
- **UI: Message Reaction System**: Implemented a high-end, glassmorphic reaction picker with:
    - 6 core emotional reactions (Love, Like, Haha, Wow, Sad, Angry).
    - Smooth entry animations (Elastic Out) and staggered micro-animations for icons.
    - Glassmorphism design with BackdropFilter blur and semi-transparent borders.
    - Integrated Haptic Feedback for a premium tactile feel.
- **UI: Message Quick Actions**: Added a "Copy" shortcut directly within the reaction picker for improved message management.

### Fixed
- **Stability: Call Connectivity Overhaul**: Resolved persistent call rejection errors by:
    - Optimizing the Stream Video initialization lifecycle.
    - Moving media hardware configuration before the join handshake to prevent contention.
    - Refactoring the call lifecycle to handle UI state transitions more robustly.
- **UI: Splash Screen Branding**: Updated the splash screen icon to align with the latest premium design system.


## [1.9.0+21] - 2026-04-24

### Added
- **Architecture: Clean Architecture Migration**: Complete overhaul of the Authentication module into a robust Clean Architecture (Data, Domain, Presentation Layers).
- **Bloc: Event-Driven Authentication**: Transitioned from Cubit to BLoC for superior state management, predictability, and improved error handling.
- **Security: Session Verification**: Implemented a mandatory Firebase session check in the Splash Screen to ensure user validity before entering the app.
- **UX: Improved Success Flow**: Success redirects (Login/Register) now pass through the Splash Screen for a premium entrance animation and final data synchronization.
- **UI: Active Status Indicator**: Added real-time "Green Dot" (Online) indicators to the chat list, including a smooth glow effect.
- **UI: Premium Toast System**: Replaced all default snackbars with a custom, high-end notification system:
    - 4 state-aware designs (Success, Info, Warning, Error).
    - **Top-aligned positioning** (slides down from top) for better visibility and non-intrusive UX.
    - Floating layout with glassmorphism shadows and smooth animations.
    - Matches the new brand aesthetic with icon circles and structured typography.
- **UI: Rich Link Preview**: Integrated automatic URL metadata parsing and rendering in chat bubbles.
- **Features: Notification Management**: Implemented a comprehensive notification settings screen with:
    - Master switch for app-wide notifications.
    - "Quiet Hours" (DND) mode with customizable start/end times.
    - Dual synchronization (Local storage + Firebase Cloud Sync).
- **Localization: Friendly Error Messages**: Integrated `ErrorMapper` to translate technical Firebase exceptions into user-friendly Thai messages.
- **DevOps: Smart APK Naming**: Implemented automatic APK renaming during the build process. Output files are now named `App-Makui-[version].apk` for better version tracking.
- **DevOps: Deployment Script Update**: Enhanced `scripts/deploy.py` to support dynamic filenames and improved asset management on GitHub Releases.

### Changed
- **Codebase: Repository Pattern**: Encapsulated business logic into UseCases (Login, Register, Logout, etc.) for better testability and reuse.
- **Cleanup**: Removed obsolete `AuthCubit` and `AuthState` files to reduce technical debt.


## [1.8.0+20] - 2026-04-23

### Added
- **Feature: In-Splash Update Checker**: Integrated a proactive version verification system directly into the Splash Screen. Users are now instantly notified of new updates upon app launch.
- **UI: Premium Update Modal**: Designed a high-end, brand-consistent update dialog with "Update Now" and "Later" options, supporting both optional and mandatory (force) updates.
- **UX: Smart Force Update**: Implemented a security-first "Force Update" mode that locks the app until critical updates are installed, ensuring all users stay on safe and compatible versions.

## [1.7.1+19] - 2026-04-21

### Fixed
- **UX: Channel List Sticker Preview**: Resolved an issue where stickers sent via the new metadata system appeared invisible in the conversation list. The preview now correctly shows `🎨 [สติ๊กเกอร์]`.
- **UX: Message Preview Reliability**: Updated the `_preview` logic to explicitly identify stickers and call logs from message metadata for consistent display across the app.

### Changed
- **Maintenance**: Refined the sticker message payload text to ensure valid message synchronization while remaining hidden in the chat bubble UI.
- **UI: Feature Cleanup**: Temporarily disabled voice call buttons in the chat room and removed unused typing indicator imports to reduce technical debt.

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
